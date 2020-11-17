# Data

The SDS REST APIs provide programmatic access to read and write SDS data. This section describes 
things to note when writing to an SdsStream.

When working in .NET, convenient SDS Client libraries are available. The `ISdsDataService` interface, accessed using the
``SdsService.GetDataService()`` helper, defines the available functions.

All writes rely on a stream’s key or primary index. The primary index determines the order of events in the stream. Secondary indexes are updated, but they do not contribute 
to the request. All references to indexes are to the primary index.

**\*Notes:** Use the ISO 8601 representation of dates and times in SDS, `2020-02-20T08:30:00-08:00` for February 20, 2020 at 8:30 AM PST, for example.
SDS returns timestamps in UTC if the timestamp is of property `DateTime` and in local time if it is of `DateTimeOffset`. 

The .NET and REST APIs provide programmatic access to read and write data. This section identifies and describes 
the APIs used to read [SdsStreams](xref:sdsStreams) data. Results are influenced by [SdsTypes](xref:sdsTypes), [SdsStreamViews](xref:sdsStreamViews), [filter expressions](xref:sdsFilterExpressions), and [table format](xref:sdsTableFormat).

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
