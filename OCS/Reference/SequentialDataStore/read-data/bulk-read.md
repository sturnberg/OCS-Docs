# Bulk Reads   
 
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
