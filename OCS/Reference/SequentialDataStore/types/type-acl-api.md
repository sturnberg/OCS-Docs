# Type ACL API

## `Get Types Access Control List`

Get the default ACL for the Types collection. For more information on ACLs, see [Access Control](xref:accessControl).

### Request
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/AccessControl/Types
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  

### Response  
The response includes a status code and a response body.

#### Response body  
The default ACL for Types

### .NET client libraries method
```csharp
   Task<AccessControlList> GetTypesAccessControlListAsync();
```
***********************

## `Update Types Access Control List`

Update the default ACL for the Types collection. For more information on ACLs, see [Access Control](xref:accessControl).

### Request
 ```text
	PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/AccessControl/Types
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
   Task UpdateTypesAccessControlListAsync(AccessControlList typesAcl);
```

***********************

## `Get Type Access Control List`

Get the ACL of the specified type. For more information on ACLs, see [Access Control](xref:accessControl).

### Request
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}/AccessControl
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string typeId`  
The type identifier  

### Response  
The response includes a status code and a response body.

#### Response body  
The ACL for the specified type

### .NET client libraries method
```csharp
   Task<AccessControlList> GetTypeAccessControlListAsync(string typeId);
```
***********************

## `Update Type Access Control List`

Update the ACL of the specified type. For more information on ACLs, see [Access Control](xref:accessControl).

Note that this does not update the ACL for the associated types. For further details about type referencing please see: [Type Reusability](#type-reusability).

### Request
 ```text
	PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}/AccessControl
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string typeId`  
The type identifier  

#### Request body 
Serialized ACL

### Response  
The response includes a status code.

### .NET client libraries method
```csharp
   Task UpdateTypeAccessControlListAsync(string typeId, AccessControlList typeAcl);
```
***

## `Get Type Owner`

Get the Owner of the specified type. For more information on Owners, see [Access Control](xref:accessControl).

### Request
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}/Owner
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string typeId`  
The type identifier  

### Response  
The response includes a status code and a response body.

#### Response body  
The Owner for the specified type 

### .NET client libraries method
```csharp
   Task<Trustee> GetTypeOwnerAsync(string typeId);
```
***********************

## `Update Type Owner`

Update the Owner of the specified type. For more information on Owners, see [Access Control](xref:accessControl).

Note that this does not update the Owner for the associated types. For further details about type referencing please see: [Type Reusability](#type-reusability).

### Request
 ```text
	PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}/Owner
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string typeId`  
The type identifier  

#### Request body 
Serialized Owner

### Response  
The response includes a status code.

#### .NET client libraries methods
```csharp
   Task UpdateTypeOwnerAsync(string typeId, Trustee typeOwner);
```
***

## `Get Type Access Rights`

Gets the Access Rights associated with the specified type for the requesting identity. For 
more information on Access Rights, see [Access Control](xref:accessControl#commonaccessrightsenum).

### Request
 ```text
	GET api/v1//Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}/AccessRights
 ```

### Parameters 

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string typeId`  
The type identifier  

### Response  
The response includes a status code and a response body.

#### Response body  
The Access Rights of the specified type for the requesting identity.

#### Example response body 
```json
HTTP/1.1 200
Content-Type: application/json

["Read", "Write"]
```

#### .NET client libraries methods
```csharp
   Task<string[]> GetTypeAccessRightsAsync(string typeId);
```
***********************