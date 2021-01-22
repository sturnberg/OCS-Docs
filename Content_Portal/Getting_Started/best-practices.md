## Namespace Best Practices

OSIsoft recommends using one of the following strategies when creating namespaces:

- Strategy 1 -- Create a separate namespace for each environment, for example, Production, Development, Staging, and so on.
- Strategy 2 -- Create a separate namespace for each end-user customer.

The first strategy is recommended for accounts where all the data belongs to one organization. Generally, it is not good practice to create separate namespaces for data that will later need to be used together.  

The second strategy may be preferable if you are providing a service to multiple end-user customers that use OSIsoft Cloud Services as a backend. This strategy makes it easier to avoid naming conflicts for end-users. It can also make it easier to manage security and assign permissions. However, it is important to note that security on a namespace is not automatically inherited by the objects and collections within it. If your organization has internal data that does not belong to an end-user customer, you may want to consider combining both strategies. Create separate namespaces for each customer and one namespace for internal use that includes your Production, Development, and Staging environments.

### Best Practices for PI System Connections

There can only be one PI to OCS Agent per connection transferring data from one PI Data Archive to an OCS namespace. This restriction prevents multiple PI to OCS Agents from pulling data from a single PI Data Archive and creating an excessive load on the server. 

Follow these best practices for setting up your PI to OCS Agents:

- Install the PI to OCS Agent on a host computer that is separate from your PI Data Archive deployment, so it does not add to the load on the host computer.
- Keep the PI to OCS Agent software version up to date for the best performance. The OCS Portal indicates when an agent is out of date and must be updated. 

### Best Practices for OMF Connections

The most important considerations with OMF connections are to ensure applications use the correct client credentials and security is correctly configured for OMF connections.

- Each type of application or system that sends OMF data to OCS should have its own defined OMF connection, with the name and description referencing the data source.
- Each application instance or each device that sends OSIsoft Message Format (OMF) data to OCS should have its own client credentials client and its own secret. Connections allow a list of clients to be defined. When each application instance or device has its own client, security is improved because secrets can be managed at a granular level.
- Ensure that the client credentials client has the minimum roles and access in OCS. For example, a client may be granted access to write data, but it does not have permissions to delete data.
- For use cases that involve a large number of source applications or source devices, the OCS API can be used to automatically assign a new client credentials client and secret whenever a new device is brought online.

## Best Practices for Creating Types

The following are best practices OSIsoft recommends for creating types and streams.

- When you create SDS types, the most important consideration to be aware of is that types are immutable. Once created, additional properties or information cannot be added and existing properties cannot be deleted.

- An SDS type  can include multiple data measurements of different data types. Each data measurement is a property of the type. In the  "Get Started with Types" procedure below, the SDS type, QuickStart.PumpState, has two measurements represented by the Temperature and Pressure properties. Each property describes the data attributes. The user interface allows you to define the following attributes for each property: Id, Name, Description, Type, and Key. At least one property in the SDS type must be an index, most commonly a timestamp. In the example below, the Timestamp property is the index. Each property is a value in each event of this type. Therefore, in an event of the QuickStart.PumpState type, there is a value for Timestamp, Temperature, and Pressure. 

  Note: You may use the REST API or client libraries to define additional optional attributes, including Value, Order, InterpolationMode, and UOM for each property. Therefore, it may be preferable to create types programmatically. 

  Ensure that each property is defined completely. A common error is to try to add Unit of Measure to the type definition after it has been created, but UOM must be defined when the type is created.  InterpolationMode and UOM on the type are inherited by the stream; however, these attributes can be overridden. If they are not defined on the type, they can be added on the stream.  <!-- Please confirm that "attributes" is the term we want to use. --> <!-- DB: It looks like existing documentation calls them "Fields" of the property, which is likely more appropriate. --><!-- "Field" is generally used to refer to a UI element, for example, it refers to the label for a text box, as in "the Id field" or "the Value field." But Id and Value, when discussed apart from the  UI, are not "fields." I'll bring this up with Ji Won who is the writer for the SDS types content. -->

- Where possible, include multiple value properties that use the same index in one SDS type. This is a more efficient way to manage your data and to transfer data into and out of OCS. For example, in the "Get Started with Types" procedure, both value properties use the DateTime index. Use a [stream view](xref:DataStorageConcepts#sds-stream-views) to view a subset of the type's properties.

- Define all of the properties of the SDS type at the time it is created. If you anticipate adding properties to the stream later, OSIsoft recommends that you create a separate stream for each property. <!-- 

For more information about best practices to consider when creating your types, see [Design considerations when creating SDS types](xref:designConsiderationsSDSTypes).

<!-- REVIEWERS: The following is a continuation of the discussion of best practices for SDS types. -->

The following are guidelines to use when creating SDS types:

- Where possible, include multiple value properties that use the same index in one SDS type. This is a more efficient way to manage your data and to transfer data into and out of OCS. In the following example, both Pressure and Temperature value properties use the DateTime index and the data values are read at the same time or index. <!-- Note: This diagram doesn't match what they're creating in the Getting Started because they can't set UOM through the UI, right? That may be okay, as long as we clarify that UOM must be set programmatically. -->

  <!-- Reviewers: These are a rough draft of the graphics. Final versions are being created. -->
  ![](C:/Users/lasato/source/repos/OCS-DOCS/lasato-ocs-get-start-doc/Content_Portal/Getting_Started/images/types-1.png)

  Do not include value properties that are read at different times or indices in the same SDS type. For example, if a device measures temperature every 30 seconds and pressure every 45 seconds, OSIsoft recommends that you define two types, one for temperature and one for pressure. Note: In this example, UOM is defined on each type and is inherited by the stream. 

  ![](C:/Users/lasato/source/repos/OCS-DOCS/lasato-ocs-get-start-doc/Content_Portal/Getting_Started/images/types-2.png)
  An alternative is to create a generic type with timestamp and value and use separate streams for temperature and pressure. The generic type is recommended in the following situations:

  - PI to OCS data or data transferred using the PI Adapters
  - When time intervals and the UOMs for the streams are unknown 
    ![](C:/Users/lasato/source/repos/OCS-DOCS/lasato-ocs-get-start-doc/Content_Portal/Getting_Started/images/types-3.png)
    In this instance, UOM is not defined on the type; it is added on the stream. 

- If you expect that different devices will have different sets of properties at different points in time, OSIsoft recommends that you use separate streams for each measurement. For example, you may have an instrument that currently measures temperature and pressure, but it may later also measure humidity. In this example, use separate streams for temperature and pressure. Later, if you add humidity, this data will be in its own stream. Using separate streams for each measurement simplifies managing the measurements in multiple devices over time.

- If properties are added to a type later, you must create a new type that includes all the properties of the original type, plus the new properties. Use a stream view to convert the existing streams to the new stream type and migrate the data. There are no values for the new properties for the existing streams, and null values are assigned. Before you migrate your data, be sure to consider the effect of the null values on your application and ensure that the application will not break if it encounters null values.

- For custom applications using the SDS client libraries or OSIsoft Messaging Format (OMF) OSIsoft recommends that you use the client libraries to define the type rather than defining them in the OSIsoft portal. This ensures that the type the application expects matches the type in the Sequential Data Store. You can also take advantage of the custom property fields such as UOM when defining a property using the .NET client libraries methods.

## Best Practices for Creating Streams

- Ensure that the default stream permissions are configured before you begin creating streams. While you can later do a bulk update of stream permissions, it is easier to configure the default permissions before the streams are created. Permissions that vary from the default are configured on the individual streams. 

- OSIsoft recommends you use a meaningful pattern when naming your streams. For example, a naming pattern might be "QuickStart.{Region}.{Site}.{Equipment}". This makes it possible for OCS tools, such as metadata rules, to use this naming schema to find relevant data. Metadata like this can also be stored as key-value pairs on the stream, but a well-defined naming pattern allows metadata to be generated automatically. 

- Use the stream description field, metadata, and tags to capture any other relevant information about the stream. This information is useful for searching for specific streams in the system, especially as systems become large. If possible, use consistent patterns in description, metadata, and tags.
  - Use metadata for information that follows a specific or consistent pattern, such as the location, manufacturer, and site. 
  - Use tags for simple information about the stream that doesn't adhere to any particular pattern.
  - Use the description field for longer descriptions of the stream and what it represents.