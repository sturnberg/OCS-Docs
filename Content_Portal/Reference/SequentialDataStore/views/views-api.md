# SdsStreamView API
The REST APIs provide programmatic access to read and write SDS data. The APIs in this section interact 
with SdsStreamViews. When working in .NET, convenient SDS .NET client libraries methods are available. The `ISdsMetadataService` 
interface, accessed using the ``SdsService.GetMetadataService()`` helper, defines the available functions. 
See [Stream Views](#stream-views) for general SdsStreamView information.

***********************

## `Get Stream View`
Returns the stream view corresponding to the specified streamViewId within a given namespace.

### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier  

### Response
The response includes a status code and a response body.


### Response body  
The requested SdsStreamView.

#### Example response body
```json
HTTP/1.1 200
Content-Type: application/json
{  
   "Id":"StreamView",
   "Name":"StreamView",
   "SourceTypeId":"Simple",
   "TargetTypeId":"Simple3",
   "Properties":[  
      {  
         "SourceId":"Time",
         "TargetId":"Time"
      },
      {  
         "SourceId":"State",
         "TargetId":"State"
      },
      {  
         "SourceId":"Measurement",
         "TargetId":"Value"
      }
   ]
}
```

### .NET client libraries method
```csharp
   Task<SdsStreamView> GetStreamViewAsync(string streamViewId);
```

***********************

## `Get Stream View Map`

Returns the stream view map corresponding to the specified streamViewId within a given namespace.

### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}/Map
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier  

### Response
 The response includes a status code and a response body.


### Response body  
The requested SdsStreamView.

#### Example response body
```json
HTTP/1.1 200
Content-Type: application/json

{  
   "SourceTypeId":"Simple",
   "TargetTypeId":"Simple3",
   "Properties":[  
      {  
         "SourceId":"Time",
         "TargetId":"Time"
      },
      {  
         "SourceId":"Measurement",
         "TargetId":"Value",
         "Mode":20
      },
      {  
         "SourceId":"State",
         "Mode":2
      },
      {  
         "TargetId":"State",
         "Mode":1 
      }
   ]
}
```


### .NET client libraries method
```csharp
   Task<SdsStreamViewMap> GetStreamViewMapAsync(string streamViewId);
```

***********************

## `Get Stream Views`

Returns a list of stream views within a given namespace.

If specifying the optional search query parameter, the list of stream views returned will match 
the search criteria. If the search query parameter is not specified, the list will include 
all stream views in the namespace. See [Search in SDS](xref:sdsSearching) for information about specifying those respective parameters.


### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews?query={query}&skip={skip}&count={count}&orderby={orderby}
 ```

### Parameters 

`string tenantId`  
The tenant identifier

`string namespaceId`  
The namespace identifier

`string query`  
An optional parameter representing a string search. 
See [Search in SDS](xref:sdsSearching)
for information about specifying the search parameter.

`int skip`  
An optional parameter representing the zero-based offset of the first SdsStreamView to retrieve. 
If not specified, a default value of 0 is used.

`int count`  
An optional parameter representing the maximum number of SdsStreamViews to retrieve. 
If not specified, a default value of 100 is used.

`string orderby`  
An optional parameter representing sorted order which SdsStreamViews will be returned. A field name is required. The sorting is based   on the stored values for the given field (of type string). For example, ``orderby=name`` would sort the returned results by the      ``name`` values (ascending by default). Additionally, a value can be provided along with the field name to identify whether to sort       ascending or descending, by using values ``asc`` or ``desc``, respectively. For example, ``orderby=name desc`` would sort the returned   results by the ``name`` values, descending. If no value is specified, there is no sorting of results.


### Response
The response includes a status code and a response body.


### Response body  
A collection of zero or more SdsStreamViews.

#### Example response body
```json
HTTP/1.1 200
Content-Type: application/json
[  
  {  
     "Id":"StreamView",
     "Name":"StreamView",
     "SourceTypeId":"Simple",
     "TargetTypeId":"Simple3"
  },
  {  
     "Id":"StreamViewWithProperties",
     "Name":"StreamViewWithProperties",
     "SourceTypeId":"Simple",
     "TargetTypeId":"Simple3",
     "Properties":[  
        {  
           "SourceId":"Time",
           "TargetId":"Time"
        },
        {
           "SourceId":"State",
           "TargetId":"State"
        },
        {
           "SourceId":"Measurement",
           "TargetId":"Value"
        }				 
     ]
  }
]
```
                
### .NET client libraries method
```csharp
   Task<IEnumerable<SdsStreamView>> GetStreamViewsAsync(int skip = 0, int count = 100);
```

***********************

## `Get or Create Stream View`

If a stream view with a matching identifier already exists, the stream view passed in is compared with the existing stream view.
If the stream views are identical, a Found (302) status is returned and the stream view. If the stream views are different, the Conflict (409) error is returned.

If no matching identifier is found, the specified stream view is created.  

### Request
 ```text
    POST api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier. The identifier must match the ``SdsStreamView.Id`` field.   

#### Request body  
The request content is the serialized SdsStreamView. If you are not using the SDS client libraries, using JSON is recommended.

### Response
The response includes a status code and a response body.

### Response body  
The newly created or matching SdsStreamView.

### .NET client libraries method
```csharp
   Task<SdsStreamView> GetOrCreateStreamViewAsync(SdsStreamView sdsStreamView);
```

***********************

## `Create or Update Stream View` 

Creates or updates the definition of a stream view. 

### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}
 ```

### Parameters 

`string tenantId`
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier  

#### Request body  
The request content is the serialized SdsStreamView.

### Response
The response includes a status code and a response body.

### Response body  
The newly created or updated SdsStreamView.

### .NET client libraries method
```csharp
   Task CreateOrUpdateStreamViewAsync(SdsStreamView SdsStreamView);
```

***********************

## `Delete Stream View`

Deletes a stream view from the specified tenant and namespace.

### Request
 ```text
    DELETE api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier  

### Response
The response includes a status code.

### .NET client libraries method
```csharp
   Task DeleteStreamViewAsync(string streamViewId);
```

***********************
## `Get Stream Views Access Control List`

Get the default ACL for the Stream Views collection. For more information on ACLs, see [Access Control](xref:accessControl).

### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/AccessControl/StreamViews
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  

### Response
The response includes a status code and a response body.

### Response body  
The default ACL for Stream Views

### .NET client libraries method
```csharp
   Task<AccessControlList> GetStreamViewsAccessControlListAsync();
```
***********************

## `Update Stream Views Access Control List`

Update the default ACL for the Stream Views collection. For more information on ACLs, see [Access Control](xref:accessControl).

### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/AccessControl/StreamViews
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  

#### Request body  
Serialized ACL

### Response
The response includes a status code.

### .NET client libraries method
```csharp
   Task UpdateStreamViewsAccessControlListAsync(AccessControlList viewsAcl);
```

***********************

## `Get Stream View Access Control List`

Get the ACL of the specified stream view. For more information on ACLs, see [Access Control](xref:accessControl).

### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}/AccessControl
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier  

### Response
The response includes a status code and a response body.

#### Response body  
The ACL for the specified stream view

### .NET client libraries method
```csharp
   Task<AccessControlList> GetStreamViewAccessControlListAsync(string streamViewId);
```
***********************

## `Update Stream View Access Control List`

Update the ACL of the specified stream view. For more information on ACLs, see [Access Control](xref:accessControl).

### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}/AccessControl
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier  

#### Request body  
Serialized ACL

### Response
The response includes a status code.

### .NET client libraries method
```csharp
   Task UpdateStreamViewAccessControlListAsync(string streamViewId, AccessControlList viewAcl);
```
***

## `Get Stream View Owner`

Get the Owner of the specified stream view. For more information on Owners, see [Access Control](xref:accessControl).

### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}/Owner
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier  

### Response
The response includes a status code and a response body.

#### Response body  
The Owner for the specified stream view

### .NET client libraries method
```csharp
   Task<Trustee> GetStreamViewOwnerAsync(string streamViewId);
```
***********************

## `Update Stream View Owner`

Update the Owner of the specified stream view. For more information on Owners, see [Access Control](xref:accessControl).

### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}/Owner
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier  

#### Request body  
Serialized Owner

### Response
The response includes a status code.

### .NET client libraries method
```csharp
   Task UpdateStreamViewOwnerAsync(string streamViewId, Trustee viewOwner);
```
***

## `Get Stream View Access Rights`

Gets the Access Rights associated with the specified stream view for the requesting identity. For 
more information on Access Rights, see [Access Control](xref:accessControl#commonaccessrightsenum).

### Request
 ```text
    GET api/v1//Tenants/{tenantId}/Namespaces/{namespaceId}/StreamViews/{streamViewId}/AccessRights
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamViewId`  
The stream view identifier  

### Response
The response includes a status code and a response body.

#### Response body  
The Access Rights of the specified stream view for the requesting identity.

#### Example response body
```json
HTTP/1.1 200
Content-Type: application/json

["Read", "Write"]
```

### .NET client libraries method
```csharp
   Task<string[]> GetStreamViewAccessRightsAsync(string streamViewId);
```
***********************
