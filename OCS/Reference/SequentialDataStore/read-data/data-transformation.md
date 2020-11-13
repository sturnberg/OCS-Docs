# Transforming Data

SDS provides the ability to transform data upon reads. The supported data transformations are:
* [Reading with SdsStreamViews](#reading-with-sdsstreamviews): Changing the shape of the returned data
* [Unit of Measure Conversions](#unit-conversion-of-data): Converting the unit of measure of the data  

Data transformations are supported for all single stream reads, but transformations have specific endpoints. The following are the base URIs for the tranformation endpoints:
```text
    api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/Transform/First
    api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/Transform/Last
    api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/Transform
    api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/Transform/Interpolated
    api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/Transform/Summaries
    api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/Transform/Sampled
```

### Reading with SdsStreamViews
When transforming data with an SdsStreamView, the data read is converted to the *target type* specified in the SdsStreamView. Working with stream views is covered in detail in the [Stream Views](xref:sdsStreamViews) section.

All stream view transformations are HTTP GET requests. Specify the stream view ID (`streamViewId={streamViewId}`) at the end of the transformation endpoint in the request as shown below. For example, the following request returns the first event of the stream *transformed* to the target type (per stream view definition specified by `streamViewId`):
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/Transform/First?streamViewId={streamViewId}
 ```



All single stream data reads support stream view transformations.

When data is requested with an SdsStreamView, the read characteristics defined by the *target type* of the SdsStreamView 
determine what is returned. The read characteristics are discussed in the code samples.


### Unit conversion of data
SDS supports assigning [Units of Measure](xref:unitsOfMeasure) (UOM) to stream data. If stream data has UOM information associated, SDS supports reading data with unit conversions applied. On each read data request, unit conversions are specified by a user defined collection of `SdsStreamPropertyOverride` objects in read requests. The `SdsStreamPropertyOverride` object has the following structure:

| Property          | Type                 | Optionality | Details                                               |
| ----------------- | -------------------- | ----------- | ----------------------------------------------------  |
| SdsTypePropertyId | String               | Required    | Identifier for an SdsTypeProperty with a UOM assigned |
| Uom               | String               | Required    | Target unit of measure                                |
| InterpolationMode | SdsInterpolationMode | N/A         | Currently not supported in context of data reads      |

This is supported in the .NET client libraries methods via overloads that accept a collection of `SdsStreamPropertyOverride` objects, and in the REST API via HTTP POST calls with a request body containing a collection of `SdsStreamPropertyOverride` objects.  

All unit conversions are POST HTTP requests. The unit conversion transformation URI is as follows:
 ```text
    POST api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/Transform
 ```

**Request body**  
The Request Body contains a collection of `SdsStreamPropertyOverride` objects. 

The following code defines a `Simple Type` with one index, `Time`, and one additional property, `Measurement`. `Measurement` has an assigned unit of measure, meter.

```csharp
public class SimpleType
{
   [SdsMember(IsKey = true, Order = 0) ]
   public DateTime Time { get; set; }
   [SdsMember(Uom = "meter")]
   public Double Measurement { get; set; }
}
```

This type is assigned to a stream, and the example request body below requests SDS to convert the `Measurement` property of the returned data from meter to centimeter.

```json
[
  {
    "SdsTypePropertyId" : "Measurement",
    "Uom" : "centimeter" 
  }
]
```

All single stream data reads with streams that have specified UOMs support UOM conversions.

***********************
