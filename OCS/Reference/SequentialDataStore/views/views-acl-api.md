# Stream view ACL API

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
