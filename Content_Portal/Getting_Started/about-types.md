---
uid: designConsiderationsSDSTypes
---
# Design considerations when creating SDS types

- Where possible, include multiple value properties that use the same index in one SDS type. This is a more efficient way to manage your data and to transfer data into and out of OCS. In the following example, both Pressure and Temperature value properties use the DateTime index and the data values are read at the same time or index. <!-- Note: This diagram doesn't match what they're creating in the Getting Started because they can't set UOM through the UI, right? That may be okay, as long as we clarify that UOM must be set programmatically. -->
    ![](images\types-1.png)

    Do not include value properties that are read at different times or indices in the same SDS type. For example, if a device measures temperature every 30 seconds and pressure every 45 seconds, OSIsoft recommends that you define two types, one for temperature and one for pressure. Note: In this example, UOM is defined on each type and is inherited by the stream. 

    ![](images\types-2.png)
    An alternative is to create a generic type with timestamp and value and use separate streams for temperature and pressure. The generic type is recommended in the following situations:
    - PI to OCS data or data transferred using the PI Adapters
    - When time intervals and the UOMs for the streams are unknown 
    ![](images\types-3.png)
    In this instance, UOM is not defined on the type; it is added on the stream. 

- If you expect that different devices will have different sets of properties at different points in time, OSIsoft recommends that you use separate streams for each measurement. For example, you may have an instrument that currently measures temperature and pressure, but it may later also measure humidity. In this example, use separate streams for temperature and pressure. Later, if you add humidity, this data will be in its own stream. Using separate streams for each measurement simplifies managing the measurements in multiple devices over time.

- If properties are added to a type later, you must create a new type that includes all the properties of the original type, plus the new properties. Use a stream view to convert the existing streams to the new stream type and migrate the data. There are no values for the new properties for the existing streams, and null values are assigned. Before you migrate your data, be sure to consider the effect of the null values on your application and ensure that the application will not break if it encounters null values.

- For custom applications using the SDS client libraries or OSIsoft Messaging Format (OMF) OSIsoft recommends that you use the client libraries to define the type rather than defining them in the OSIsoft portal. This ensures that the type the application expects matches the type in the Sequential Data Store. You can also take advantage of the custom property fields such as UOM when defining a property using the .NET client libraries methods.

## Inherited Attributes

<! -- We might want to add some general discussion about inheritance of attributes and why/when you want to define these attributes on the type. -->