# Stream API

The REST APIs provide programmatic access to read and write SDS data. The API in this 
section interacts with SdsStreams. When working in .NET framework, convenient SDS client libraries are 
available. The ``ISdsMetadataService`` interface, accessed using the ``SdsService.GetMetadataService( )`` helper, 
defines the available functions. See [Streams](#streams) above for general 
information related to SdsStream. 

**********************
## `Get Stream`
Returns the specified stream.

### Request
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}
 ```

### Parameters
`string tenantId`  
The tenant identifier

`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier


### Response
The response includes a status code and a response body.

#### Response body 
The requested SdsStream

#### Example response body
```json
HTTP/1.1 200
Content-Type: application/json

{  
   "Id":"Simple",
   "Name":"Simple",
   "TypeId":"Simple",
}
```

### .NET client libraries method
```csharp
   Task<SdsStream> GetStreamAsync(string streamId);
```

***********************
## `Get Streams` 
Returns a list of streams.

If specifying the optional search query parameter, the list of streams returned will match 
the search criteria. If the search query parameter is not specified, the list will include 
all streams in the namespace. See [Search in SDS](xref:sdsSearching#search-for-streams) 
for information about specifying those respective parameters.


### Request
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams?query={query}&skip={skip}&count={count}&orderby={orderby}
 ```

### Parameters

`string tenantId`  
The tenant identifier

`string namespaceId`  
The namespace identifier

`string query`  
[Optional] Parameter representing a string search. 
See [Search in SDS](xref:sdsSearching) for information about specifying the search parameter.

`int skip`  
[Optional] Parameter representing the zero-based offset of the first SdsStream to retrieve. 
If not specified, a default value of 0 is used.

`int count`  
[Optional] Parameter representing the maximum number of SdsStreams to retrieve. 
If not specified, a default value of 100 is used.

`string orderby`  
[Optional] Parameter representing sorted order which SdsStreams will be returned. A field name is required. The sorting is based on the stored values for the given field (of type string). For example, ``orderby=name`` would sort the returned results by the ``name`` values (ascending by default). Additionally, a value can be provided along with the field name to identify whether to sort ascending or descending, by using values ``asc`` or ``desc``, respectively. For example, ``orderby=name desc`` would sort the returned results by the ``name`` values, descending. If no value is specified, there is no sorting of results.

### Response
The response includes a status code and a response body.

#### Response body 
A collection of zero or more SdsStreams

#### Example response body
```json
HTTP/1.1 200
Content-Type: application/json

[  
   {  
      "Id":"Simple",
      "TypeId":"Simple"
   },
   {  
      "Id":"Simple with Secondary",
      "TypeId":"Simple",
      "Indexes":[  
         {  
            "SdsTypePropertyId":"Measurement"
         }
      ]
   },
   {  
      "Id":"Compound",
      "TypeId":"Compound"
   },
   ...
]
```

### .NET client libraries method  
```csharp
   Task<IEnumerable<SdsStream>> GetStreamsAsync(string query = "", int skip = 0, 
      int count = 100);
```

***********************

## `Get Stream Type`
Returns the type definition that is associated with a given stream.

### Request
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Type
 ```

### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

### Response
The response includes a status code and a response body.

#### Response body 
The requested SdsType.

### .NET client libraries method
```csharp
   Task<SdsType> GetStreamTypeAsync(string streamId);
```

***********************

## `Get or Create Stream`
Creates the specified stream. If an SdsStream with a matching identifier already exists, SDS compares the 
existing stream with the stream that was sent. If the streams are identical, a ``Found`` (302) error 
is returned with the Location header set to the URI where the stream may be retrieved using a Get function. 
If the streams do not match, a ``Conflict`` (409) error is returned.

For a matching stream (Found), clients that are capable of performing a redirect that includes the 
authorization header can automatically redirect to retrieve the stream. However, most clients, 
including the .NET HttpClient, consider redirecting with the authorization token to be a security vulnerability.

When a client performs a redirect and strips the authorization header, SDS cannot authorize the request and 
returns ``Unauthorized`` (401). For this reason, it is recommended that when using clients that do not 
redirect with the authorization header, you should disable automatic redirect.

### Request
 ```text
	POST api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}
 ```

### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier. The stream identifier must match the identifier in content. 

#### Request body  
The request content is the serialized SdsStream.

### Response
The response includes a status code and a response body.

#### Response body 
The newly created SdsStream.


### .NET client libraries method
```csharp
      Task<SdsStream> GetOrCreateStreamAsync(SdsStream SdsStream);
```

If a stream with a matching identifier already exists and it matches the stream in the request body, 
the client redirects a GET to the Location header. If the existing stream does not match the stream 
in the request body, a Conflict error response is returned and the client library method throws an exception. 

***********************

## `Create or Update Stream`

Creates the specified stream. If a stream with the same `Id` already exists, the definition of the stream is updated. 
The following changes are permitted:  

- Name  
- Description  
- Indexes  
- InterpolationMode  
- ExtrapolationMode  
- PropertyOverrides  

Note that modifying indexes will result in re-indexing all of the stream's data for each additional secondary index.

For more information on secondary indexes, see [Indexes](#indexes).

Changes that are not permitted result in an error.

### Request
 ```text
	PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}
 ```

### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

#### Request body  
The request content is the serialized SdsStream.

### Response
The response includes a status code.


### .NET client libraries method
```csharp
   Task CreateOrUpdateStreamAsync(SdsStream SdsStream);
```
***********************

## `Update Stream Type`

Updates a stream’s type. The type is modified to match the specified stream view. 
Defined Indexes and PropertyOverrides are removed when updating a stream type. 

### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Type?streamViewId={streamViewId}
 ```

### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  
  
`string streamViewId`  
The stream view identifier  

#### Request body  
The request content is the serialized SdsStream.

### Response
The response includes a status code.

#### Response body 
On failure, the content contains a message describing the issue.

### .NET client libraries method
```csharp
   Task UpdateStreamTypeAsync(string streamId, string streamViewId);
```

***********************

## `Delete Stream`

Deletes a stream. 

### Request
 ```text
    DELETE api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}
 ```

### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

### Response
The response includes a status code.

### .NET client libraries method
```csharp
   Task DeleteStreamAsync(string streamId);
```

***********************

