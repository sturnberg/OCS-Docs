---
uid: GSTypes
---

# Types

Sequential Data Store (SDS) types define the shape and structure of events and how to associate events within a stream of data. An SDS type is comprised of at least two properties. One property serves as the primary index, most commonly a timestamp or DateTime. In addition, it has one or more additional properties called value properties which describes the data in each stream event. Each value property can have a different property type. For example, In the "Get Started with Types" procedure below, you create two value properties with Ids called Temperature and Pressure. A wide variety of property types are supported. For a list of the supported property types, see [Supported Types](xref:sdsTypes#supported-types). Note: You can also create complex secondary indexes. SDS types are immutable. Once created, they cannot be updated. Therefore, it is important to determine the correct type definition before you begin building streams and data in the Sequential Data Store.

For more information on SDS Types, see <!-- add xref.-->

### PI Core Counterpart

An SDS type is comparable to PI point type in PI Data Archive. For example, a PI point of type float32 is comparable to an SDS type with a DateTime index property and a float32 value property. Because they are similar, if you use PI to OCS to import data into SDS, some "PI-\*" types are created automatically in SDS that map to existing PI point types. PI Data Archive has a predefined list of supported PI point types. The data structure of the Sequential Data Store is more flexible because SDS types can include multiple data measurements of different data types, and data can be indexed using a non-time-series index or multiple indexes. 

## Best Practices for Creating Types

<!-- This list is getting pretty long and a little "in the weeds." I'm wondering if for the new customer, we should keep it simple and point them to a longer discussion on Best Practices. For example, we could keep the first three bullets and part of #5 here. And put the rest in the "Design considerations when creating SDS types" topic that we link to. -->

The following are best practices OSIsoft recommends for creating types and streams.

- When you create SDS types, the most important consideration to be aware of is that types are immutable. Once created, additional properties or information cannot be added and existing properties cannot be deleted.

- An SDS type  can include multiple data measurements of different data types. Each data measurement is a property of the type. In the  "Get Started with Types" procedure below, the SDS type, QuickStart.PumpState, has two measurements represented by the Temperature and Pressure properties. Each property describes the data attributes. The user interface allows you to define the following attributes for each property: Id, Name, Description, Type, and Key. At least one property in the SDS type must be an index, most commonly a timestamp. In the example below, the Timestamp property is the index. Each property is a value in each event of this type. Therefore, in an event of the QuickStart.PumpState type, there is a value for Timestamp, Temperature, and Pressure. 

   Note: You may use the REST API or client libraries to define additional optional attributes, including Value, Order, InterpolationMode, and UOM for each property. Therefore, it may be preferable to create types programmatically. 

   Ensure that each property is defined completely. A common error is to try to add Unit of Measure to the type definition after it has been created, but UOM must be defined when the type is created.  InterpolationMode and UOM on the type are inherited by the stream; however, these attributes can be overridden. If they are not defined on the type, they can be added on the stream.  <!-- Please confirm that "attributes" is the term we want to use. --> <!-- DB: It looks like existing documentation calls them "Fields" of the property, which is likely more appropriate. --><!-- "Field" is generally used to refer to a UI element, for example, it refers to the label for a text box, as in "the Id field" or "the Value field." But Id and Value, when discussed apart from the  UI, are not "fields." I'll bring this up with Ji Won who is the writer for the SDS types content. -->

- Where possible, include multiple value properties that use the same index in one SDS type. This is a more efficient way to manage your data and to transfer data into and out of OCS. For example, in the "Get Started with Types" procedure, both value properties use the DateTime index. Use a [stream view](xref:DataStorageConcepts#sds-stream-views) to view a subset of the type's properties.

  <!--  I moved #4 to the "Design considerations when creating SDS types" topic.  --><!-- 4. Do not include value properties that are read at different times or indices in the same SDS type. For example, if a device measures temperature every 30 seconds and pressure every 45 seconds, OSIsoft recommends that you define two types, one for temperature and one for pressure. For a more extended discussion on creating SDS types, see [Design considerations when creating SDS types](xref:DesignConsiderationsSDSTypes). -->

- Define all of the properties of the SDS type at the time it is created. If you anticipate adding properties to the stream later, OSIsoft recommends that you create a separate stream for each property. <!-- This was #5. Keep this in the Best Practices here. -->

   <!-- I moved the rest of the content to the more detailed discussion. --><!-- If you expect that different devices will have different sets of properties at different points in time, OSIsoft recommends that you use separate streams for each measurement. For example, you may have an instrument that currently measures temperature and pressure, but it may later also measure humidity. In this example, use separate streams for temperature and pressure. Later, if you add humidity, this data will be in its own stream. Using separate streams for each measurement simplifies managing the measurements in multiple devices over time. -->

   <!-- 6. If properties are added to a type later, you must create a new type that includes all the properties of the original type, plus the new properties. Use a stream view to convert the existing streams to the new stream type and migrate the data. There are no values for the new properties for the existing streams, and null values are assigned. Before you migrate your data, be sure to consider the effect of the null values on your application and ensure that the application will not break if it encounters null values. -->

   <!-- 7. For custom applications using the SDS client libraries or OSIsoft Messaging Format (OMF) OSIsoft recommends that you use the client libraries to define the type rather than defining them in the OSIsoft portal. This ensures that the type the application expects matches the type in the Sequential Data Store. You can also take advantage of the custom property fields such as UOM when defining a property using the .NET client libraries methods. -->

For more information about best practices to consider when creating your types, see [Design considerations when creating SDS types](xref:designConsiderationsSDSTypes).
## Get Started with Types

1. Click the ![Menu icon](images\menu-icon.png) icon and click **Sequential Data Store** (under Data Management).

1. Click **Types**. From the **Namespace** drop-down list, select QuickStart.

1. Click the ![Manage Default Type Permissions icon](Images\ManageDefaultIcon.png) icon above the tree on the left. 
   This opens the Manage Default Permissions for New Types window where default permissions for new types are specified. 

   Note: By default, you must be assigned the Account Administrator role to change the default permissions. Any changes only affect new types that are created. It does not change the permissions on already existing types. 

   When you are done, click **Cancel** to continue.

1. Click **Add Type**.

1. In the Add Type window, enter the following:

   - Id &ndash; QuickStart.PumpState
   - Name &ndash; QuickStart.PumpState
   - Description &ndash; SDS Type used by OCS Quick Start

1. Click the ![Properties icon](Images\PropertiesPlusIcon.png)icon next to **Properties** to add a property.

1. Complete the following fields for the first property:
   - Id &ndash; Enter **Timestamp**.
   - Type &ndash; Select **DateTime**. 
   - Key &ndash; Select the checkbox.
   
1. Click the ![Properties icon](Images\PropertiesPlusIcon.png)icon to add a second property and complete the fields:
   - Id &ndash; Enter **Temperature**
   - Type &ndash; Select **Double**.
   
1. Click the ![Properties icon](Images\PropertiesPlusIcon.png)icon to add a third property and complete the fields:

   - Id &ndash; Enter **Pressure**.
   - Type &ndash; Select **Double**.

1. Click **Save**.

1. Click the checkbox to select the QuickStart.PumpState type in the list and click the ![Manage Permissions icon](C:/Users/lasato/Desktop/OCS Getting Started/Images/manage-permissions-icon.png) icon.

    This opens the Manage Permissions for QuickStart.PumpState window where you can override the default permissions and set permissions for the specific type. By default, you must be assigned the Account Administrator role to configure the type permissions.

    Review the permissions for the QuickStart.PumpState type, and when you are done exploring this window, click **Cancel** to continue. 

1. Click **View Type**.

   This window shows the type details which you entered in the dialog window when you added the type. Click **Cancel** to continue.

1. Click **Get Type Streams**.

   This takes you to the Streams list and, by default, it uses the _*typeId:QuickStart.PumpState* query to filter for any streams with the QuickStart.PumpState type. The list is empty because no streams have yet been created with this type.
   
