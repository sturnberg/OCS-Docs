# Search in SDS

You can search for objects using texts, phrases and fields in Sequential Data Store (SDS). The REST APIs (or .NET client libraries methods ``GetStreamsAsync``, ``GetTypesAsync``, and ``GetStreamViewsAsync``) return items that match the search criteria within a given namespace. By default, the ``query`` parameter applies to all searchable object fields.

For example, a namespace contains the following SdsStreams:

**streamId** | **Name**  | **Description**
------------ | --------- | ----------------
stream1      | tempA     | Temperature from DeviceA
stream2      | pressureA | Pressure from DeviceA
stream3      | calcA     | Calculation from DeviceA values

A ``GetStreamsAsync`` call with different queries will return below:

**Query string**     | **Returns**
------------------  | ----------------------------------------
``temperature``  | stream1
``calc*``        | stream3
``DeviceA*``     | stream1, stream2, stream3
``humidity*``    | nothing

#### Requests
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams?query=name:pump name:pressure&orderby=name

	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams?query=name:pump name:pressure&orderby=id asc

	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams?query=name:pump name:pressure&orderby=name desc

	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams?query=name:pump name:pressure&orderby=name desc&skip=10&count=20
 ```
#### Parameters
`string query`  
[Optional] Parameter representing the search criteria. If unspecified, returns all values. Can be used with `skip`, `count` and `orderby`.

`int skip`  
[Optional] Parameter representing the zero-based offset of the first SdsStream to retrieve. The number of matched items to skip over before returning. If unspecified, a default value of 0 is used. Use when more items match the search criteria than can be returned in a single call.

`int count`  
[Optional] Parameter representing the maximum number of SdsStreams to retrieve. If unspecified, a default value of 100 is used. The maximum value is 1,000. 

`string orderby`  
[Optional] Parameter representing the sorted order in which SdsStreams are returned. Requires a field name (``orderby=name``, for example). Default order is ascending (``asc``). Add ``desc`` for descending order (``orderby=name desc``, for example). If unspecified, there is no sorting of results.

#### .NET client libraries methods
If there are 175 SdsStreams that match the search criteria "temperature" in a single call for example, the following call will return the first 100 matches:

```csharp
    _metadataService.GetStreamsAsync(query:"temperature", skip:0, count:100)
```

If ``skip`` is set to 100, the following call will return the remaining 75 matches while skipping over the first 100:
```csharp
    _metadataService.GetStreamsAsync(query:"temperature", skip:100, count:100)
```

## Search for streams

SdsStreams search is exposed through the REST API and the client libraries method ``GetStreamsAsync``.

For more information on SdsStream properties, see [Streams](xref:sdsStreams#streampropertiestable).

**Searcheable Properties**
| Property          | Searchable  |
|-------------------|-------------|
| Id                | Yes		  |
| TypeId            | Yes		  |
| Name              | Yes		  |
| Description       | Yes		  |
| Indexes           | No		  |
| InterpolationMode | No		  |
| ExtrapolationMode | No		  |
| PropertyOverrides | No		  |

**Searcheable Child Resources**
| Property          | Searchable  |
|-------------------|-------------|
| [Metadata](xref:sdsStreamExtra)*		| Yes		  |
| [Tags](xref:sdsStreamExtra)*	| Yes		  |
| ACL | No		  |
| Owner | No		  |
**\*Notes on metadata and tags:** You can access SdsStream metadata and tags through Metadata and Tags API respectively. Metadata and tags are associated with SdsStream objects and can be used as search criteria. See [below](#Stream_Metadata_search_topic) for more information.

#### Request
Search for SdsStreams using the REST API and specifying the optional `query` parameter:
 ```text
      GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams?query={query}&skip={skip}&count={count}
 ```
#### Parameters
`string query`  
[Optional] Parameter representing the search criteria. If unspecified, returns all values. Can be used with `skip`, `count` and `orderby`. 

`int skip`  
[Optional] Parameter representing the zero-based offset of the first SdsStream to retrieve. If unspecified, a default value of 0 is used. Use when more items match the search criteria than can be returned in a single call.

`int count`  
[Optional] Parameter representing the maximum number of SdsStreams to retrieve. If unspecified, a default value of 100 is used. The maximum value is 1,000. 

#### .NET client libraries method
``GetStreamsAsync`` is used to search for and return SdsStreams. 
```csharp
      _metadataService.GetStreamsAsync(query:"QueryString", skip:0, count:100);
```

The SdsStream fields valid for search are identified in the fields table located on the [Streams](xref:sdsStreams#streampropertiestable) page.
Note that SdsStream metadata has unique syntax rules.
See [How search works with stream metadata](#Stream_Metadata_search_topic).