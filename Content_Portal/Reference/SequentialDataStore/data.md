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

## Single Stream Reads  
The following methods for reading a single value are available:

* [Get First Value](xref:sdsReadingDataApi#get-first-value) returns the first value in the stream.
* [Get Last Value](xref:sdsReadingDataApi#get-last-value) returns the last value in the stream.
* [Find Distinct Value](xref:sdsReadingDataApi#find-distinct-value) returns a value based on a starting index and search criteria.

In addition, the following methods support reading multiple values:

* [Get Values](xref:sdsReadingDataApi#get-values) retrieves a collection of stored values based on the request parameters.
* [Get Interpolated Values](xref:sdsReadingDataApi#get-interpolated-values) retrieves a collection of stored or calculated values based on the request parameters.
* [Get Summaries](xref:sdsReadingDataApi#get-summaries) retrieves a collection of evenly spaced summary intervals based on a count 
  and specified start and end indexes.
* [Get Sampled Values](xref:sdsReadingDataApi#get-sampled-values) retrieves a collection of sampled data based on the request parameters.

All single stream reads are HTTP GET actions. Reading data involves getting events from streams. The base reading URI from a single stream is as follows:
 ```text
	api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data
 ```

**Parameters**  

``string tenantId``  
The tenant identifier

``string namespaceId``  
The namespace identifier

``string streamId``  
The stream identifier

## Single Stream Writes   

The following methods support writing a single or multiple values:
* [Insert Values](xref:sdsWritingDataApi#insert-values) inserts a collection of events.
* [Patch Values](xref:sdsWritingDataApi#patch-values) updates specific fields for a collection of events.
* [Replace Values](xref:sdsWritingDataApi#remove-values) replaces a collection of events.
* [Remove Values](xref:sdsWritingDataApi#remove-values) deletes the events based on the request parameters.
* [Update Values](xref:sdsWritingDataApi#update-values) add or replaces a collection of events.

The base URI for writing SDS data to a single stream is:
 ```text
      api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data  
 ```
 
### Parameters
``string tenantId``  
The tenant identifier  
  
``string namespaceId``  
The namespace identifier  
  
``string streamId``  
The stream identifier  
 
### Request Body Format
With the exception of Remove Values, all single stream write calls require a request body containing the events to insert or modify.

The events must be formatted as a serialized JSON array of the stream's type. JSON arrays are comma-delimited lists of a type enclosed within square brackets. The following code shows a list of three WaveData events that are properly formatted for insertion. See the [OCS-Samples](https://github.com/osisoft/OCS-Samples) for the complete example.

```json
[
    {
        "Order":2,
        "Tau":0.25722883666666846,
        "Radians":1.6162164471269089,
        "Sin":1.9979373673043652,
        "Cos":-0.090809010174665111,
        "Tan":-44.003064529862513,
        "Sinh":4.8353589272389,
        "Cosh":5.2326566823391856,
        "Tanh":1.8481468289554672
    }, 
    {
        "Order":4,
        "Tau":0.25724560000002383,
        "Radians":1.6163217742567466,
        "Sin":1.9979277915696148,
        "Cos":-0.091019446679060964,
        "Tan":-43.901119254534827,
        "Sinh":4.8359100947709592,
        "Cosh":5.233166005842703,
        "Tanh":1.8481776000882766
    }, 
    {
        "Order":6,
        "Tau":0.25724560000002383,
        "Radians":1.6163217742567466,
        "Sin":1.9979277915696148,
        "Cos":-0.091019446679060964,
        "Tan":-43.901119254534827,
        "Sinh":4.8359100947709592,
        "Cosh":5.233166005842703,
        "Tanh":1.8481776000882766
    }
]
```

You can serialize your data using one of many available JSON serializers available at [Introducing JSON](http://json.org/index.html). 


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

### Response Format
Supported response formats include JSON, verbose JSON, and SDS. 

The default response format for SDS is JSON, which is used in all examples in this document. 
Default JSON responses do not include any values that are equal to the default value for their type.

Verbose JSON responses include all values in the returned JSON payload, including defaults.
To specify verbose JSON return, add the header ``Accept-Verbosity`` with a value of ``verbose`` to the request. 

Verbose has no impact on writes; writes return only error messages.

To specify SDS format, set the ``Accept`` header in the request to ``application/sds``.

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