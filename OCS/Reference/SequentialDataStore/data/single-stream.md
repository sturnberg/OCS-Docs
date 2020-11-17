# Single Stream Reads  
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
