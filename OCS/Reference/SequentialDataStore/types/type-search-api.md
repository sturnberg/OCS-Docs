# Search for types

SdsType search is exposed through the REST API and the client libraries method ``GetTypesAsync``. 
For more information on type properties, see [Types](xref:sdsTypes#typepropertiestable).

**Searcheable Properties**
| Property          | Searchable |
|-------------------|------------|
| Id                | Yes        |
| Name              | Yes        |
| Description       | Yes        |
| SdsTypeCode       | No         |
| InterpolationMode | No         |
| ExtrapolationMode | No         |
| Properties        | Yes, with limitations* |
**\*Notes on `Properties` field:** `Name` and `Id` of an SdsType are included in its `Properties` field. Similarly, `Name` and `Id` of a nested type are included in its `Properties`. If there are two types with the same `Properties`, `Name` or `Id`, the search will return both types in the result.

#### Request
Search for SdsTypes using the REST API and specifying the optional `query` parameter:
 ```text
      GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types?query={query}&skip={skip}&count={count}
 ```
#### Parameters
`string query`  
[Optional] Parameter representing the search criteria. If unspecified, returns all values. Can be used with `skip`, `count` and `orderby`. 

`int skip`  
[Optional] Parameter representing the zero-based offset of the first SdsType to retrieve. If unspecified, a default value of 0 is used. Use when more items match the search criteria than can be returned in a single call.

`int count`  
[Optional] Parameterr representing the maximum number of SdsTypes to retrieve. If unspecified, a default value of 100 is used. The maximum value is 1,000. 

#### .NET client libraries method
``GetTypesAsync`` is used to search for and return types. 
```csharp
      _metadataService.GetTypesAsync(query:"QueryString", skip:0, count:100);
```