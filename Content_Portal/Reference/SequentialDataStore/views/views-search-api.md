# Search for stream views
SdsStreamView search is exposed through the REST API and the client libraries method ``GetStreamViewsAsync``. 
For more information on SdsStreamView properties, see [Stream Views](xref:sdsStreamViews#streamviewpropertiestable).

**Searcheable Properties**
| Property     | Searchable |
|--------------|------------|
| Id           | Yes		|
| Name         | Yes		|
| Description  | Yes		|
| SourceTypeId | Yes		|
| TargetTypeId | Yes		|
| Properties   | Yes, with limitations* |
**\*Notes on `Properties` field:** The `Properties` collection contains a list of SdsStreamViewProperty objects. The query will attempt to find a match on the SdsStreamViewProperty's `Id`, `SourceTypeId`, and `TargetTypeId` fields. The `Properties` collection of nested views will also be searched. See example below.  

#### Example
You can search for ``ComplexView`` using the `Id`("NestedView"), `SourceTypeId`, and `TargetTypeId` of ``NestedView`` but not its `Description`("An example of a nested view").  
```json
{ 
   "Id":"ComplexView",
   "Name":"ComplexView",
   "SourceTypeId":"ComplexSourceType",
   "TargetTypeId":"ComplexTargetType",
   "Description":null,
   "Properties":[ 
      { 
         "SourceId":"Value",
         "TargetId":"Value",
         "SdsStreamView":{ 
            "Id":"NestedView",
            "SourceTypeId":"NestedType",
            "TargetTypeId":"NestedType",
            "Description":"An example of a nested view",
            "Properties":[ 
               { 
                  "SourceId":"Value",
                  "TargetId":"Value"
               }
            ]
         }
      }
   ]
}
```
#### Request
Search for stream views using the REST API and specifying the optional `query` parameter:
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews?query={query}&skip={skip}&count={count}
 ```
#### Parameters
`string query`  
[Optional] Parameter representing the search criteria. If unspecified, returns all values. Can be used with `skip`, `count` and `orderby`. 

`int skip`  
[Optional] Parameter representing the zero-based offset of the first SdsStreamView to retrieve.If unspecified, a default value of 0 is used. Use when more items match the search criteria than can be returned in a single call.

`int count`  
[Optional] Parameter representing the maximum number of SdsStreamViews to retrieve. If unspecified, a default value of 100 is used. The maximum value is 1,000. 

#### .NET client libraries method
``GetStreamViewsAsync`` is used to search for and return stream views. 
```csharp
    _metadataService.GetStreamViewsAsync(query:"QueryString", skip:0, count:100);
```
