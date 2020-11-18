# Data

The SDS REST APIs provide programmatic access to read and write SDS data. This section identifies and describes 
things to note when reading and writing to an SdsStream. 
Results are influenced by [SdsTypes](xref:sdsTypes), [SdsStreamViews](xref:sdsStreamViews), [filter expressions](xref:sdsFilterExpressions), and [table format](xref:sdsTableFormat).


When working in .NET, convenient SDS Client libraries are available. The `ISdsDataService` interface, accessed using the
``SdsService.GetDataService()`` helper, defines the available functions.

All writes rely on a stream's key or primary index. The primary index determines the order of events in the stream. Secondary indexes are updated, but they do not contribute 
to the request. All references to indexes are to the primary index.

**\*Notes:** Use the ISO 8601 representation of dates and times in SDS, `2020-02-20T08:30:00-08:00` for February 20, 2020 at 8:30 AM PST, for example.
SDS returns timestamps in UTC if the timestamp is of property `DateTime` and in local time if it is of `DateTimeOffset`. 


If you are working in a .NET environment, convenient SDS Client Libraries are available. 
The `ISdsDataService` interface, which is accessed using the ``SdsService.GetDataService()`` helper, 
defines the functions that are available.

## Bulk Reads   
 
SDS supports reading from multiple streams in one request. The following method for reading data from multiple streams is available:
* [Join Values](xref:sdsReadingDataApi#join-values) retrieves a collection of events across multiple streams and joins the results based on the request parameters.

Multi-stream reads can be HTTP GET or POST actions. The base reading URI for reading from multiple streams is as follows:
 ```text
    api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Bulk/Streams/Data
 ```

**Parameters**  
``string tenantId``  
The tenant identifier

``string namespaceId``  
The namespace identifier

### Indexes
Writing to the SDS relies on the primary index for positioning within the streams and locating existing events. 
Most writes use the index as specified by the value. Deletes are the exception to this rule. When deleting, 
indexes are specified as strings in the URI, or, when using the SDS Client Libraries, the index may be 
passed as-is to DELETE methods that take the index type as a generic argument. For more information on working 
with indexes, see [Indexes](xref:sdsIndexes). For information on compound indexes, see [Compound indexes](xref:sdsIndexes#compound-indexes).

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