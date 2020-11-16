# Quantities ACL API

## `Get Quantities Access Control List`

Get the default ACL for the Quantities collection. For more information on ACLs, see [Role-based access control](xref:accessControl).

#### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/AccessControl/Quantities
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  

#### Response
The response includes a status code and a response body.

##### Response body  
The default ACL for Quantities

#### .NET client libraries method
```csharp
   Task<AccessControlList> GetQuantitiesAccessControlListAsync();
```
***

## `Update Quantities Access Control List`

Update the default ACL for the Quantities collection. For more information on ACLs, see [Role-based access control](xref:accessControl).

#### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/AccessControl/Quantities
 ```

##### Parameters
`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  

##### Request body
Serialized ACL

#### Response
The response includes a status code.

#### .NET client libraries method
```csharp
   Task UpdateQuantitiesAccessControlListAsync(AccessControlList quantitiesAcl);
```

***********************

## `Get Quantity Access Control List`

Get the ACL of the specified quantity. For more information on ACLs, see [Role-based access control](xref:accessControl).

#### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/AccessControl
 ```

##### Parameters
`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

#### Response  
The response includes a status code and a response body.

##### Response body
The ACL for the specified quantity

#### .NET client libraries method
```csharp
   Task<AccessControlList> GetQuantityAccessControlListAsync(string quantityId);
```
***********************

## `Update Quantity Access Control List`

Update the ACL of the specified quantity. For more information on ACLs, see [Role-based access control](xref:accessControl).

#### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/AccessControl
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

##### Request body
Serialized ACL

#### Response 
The response includes a status code.

#### .NET client libraries method
```csharp
   Task UpdateQuantityAccessControlListAsync(string quantityId, AccessControlList quantityAcl);
```
***

## `Get Quantity Owner`

Get the Owner of the specified quantity. For more information on Owners, see [Role-based access control](xref:accessControl).

#### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/Owner
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

#### Response 
The response includes a status code and a response body.

##### Response body  
The Owner for the specified quantity

#### .NET client libraries method
```csharp
   Task<Trustee> GetQuantityOwnerAsync(string quantityId);
```
***********************

## `Update Quantity Owner`

Update the Owner of the specified quantity. For more information on Owners, see [Role-based access control](xref:accessControl).

#### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/Owner
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

##### Request body  
Serialized Owner

#### Response  
The response includes a status code.

#### .NET client libraries method
```csharp
   Task UpdateQuantityOwnerAsync(string quantityId, Trustee quantityOwner);
```
***

## `Get Quantity Access Rights`

Gets the Access Rights associated with the specified quantity for the requesting identity.  For 
more information on Access Rights, see [Role-based access control](xref:accessControl#commonaccessrightsenum).

#### Request
 ```text
    GET api/v1//Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/AccessRights
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

#### Response    
The response includes a status code and a response body.

##### Response body 
The Access Rights of the specified quantity for the requesting identity.

##### Example response body
```json
HTTP/1.1 200
Content-Type: application/json

["Read", "Write"]
```

#### .NET client libraries method
```csharp
   Task<string[]> GetQuantityAccessRightsAsync(string quantityId);
```
***********************