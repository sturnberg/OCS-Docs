# Stream ACL API

## `Get Streams Access Control List`

Get the default ACL for the Streams collection. For more information on ACL, see [Access Control](xref:accessControl).

### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/AccessControl/Streams
 ```

### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  

### Response
The response includes a status code and a response body.

#### Response body 
The default ACL for Streams

### .NET client libraries method
```csharp
   Task<AccessControlList> GetStreamsAccessControlListAsync();
```
***********************

## `Update Streams Access Control List`

Update the default ACL for the Streams collection. For more information on ACL, see [Access Control](xref:accessControl).

### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/AccessControl/Streams
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
   Task UpdateStreamsAccessControlListAsync(AccessControlList streamsAcl);
```

***********************

## `Get Stream Access Control List`

Get the ACL of the specified stream. For more information on ACL, see [Access Control](xref:accessControl).

### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/AccessControl
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
The ACL for the specified stream 

### .NET client libraries method
```csharp
   Task<AccessControlList> GetStreamAccessControlListAsync(string streamId);
```
***********************

## `Update Stream Access Control List`

Update the ACL of the specified stream. For more information on ACL, see [Access Control](xref:accessControl).

### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/AccessControl
 ```

### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

#### Request body  
Serialized ACL

### Response
The response includes a status code.

### .NET client libraries method
```csharp
   Task UpdateStreamAccessControlListAsync(string streamId, AccessControlList streamAcl);
```
*** 

## `Get Stream Owner`

Get the `Owner` of the specified stream. For more information, see [Access Control](xref:accessControl).

### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Owner
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
The `Owner` for the specified stream 

### .NET client libraries method
```csharp
   Task<Trustee> GetStreamOwnerAsync(string streamId);
```
***********************

## `Update Stream Owner`

Update the `Owner` of the specified stream. For more information, see [Access Control](xref:accessControl).

### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Owner
 ```

### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

#### Request body  
Serialized Owner

### Response
The response includes a status code

### .NET client libraries method
```csharp
   Task UpdateStreamOwnerAsync(string streamId, Trustee streamOwner);
```
*** 

## `Get Stream Access Rights`

Gets the access rights associated with the specified stream for the requesting identity. For 
more information on access rights, see [Access Control](xref:accessControl#commonaccessrightsenum).

### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/AccessRights
 ```

### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

### Response
The response includes a status code and a response body

#### Response body 
The Access Rights associated with specified stream for the requesting identity.

#### Example response body
```json
HTTP/1.1 200
Content-Type: application/json

["Read", "Write"]
```

### .NET client libraries method
```csharp
   Task<string[]> GetStreamAccessRightsAsync(string streamId);
```
***********************