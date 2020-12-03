# Units ACL API

## `Get Uom Access Control List`

Get the ACL of the specified unit of measure. For more information on ACLs, see [Access Control](xref:accessControl).

#### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/Units/{uomId}/AccessControl
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

`string uomId`  
The unit of measure identifier

#### Response   
The response includes a status code and a response body.

##### Response body  
The ACL for the specified Uom

#### .NET client libraries method
```csharp
   Task<AccessControlList> GetQuantityUomAccessControlListAsync(string quantityId, string uomId);
```
***********************

## `Update Uom Access Control List`

Update the ACL of the specified unit of measure. For more information on ACLs, see [Access Control](xref:accessControl).

#### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/Units/{uomId}/AccessControl
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

`string uomId`  
The unit of measure identifier

##### Request body  
Serialized ACL

#### Response   
The response includes a status code.

#### .NET client libraries method
```csharp
   Task UpdateQuantityUomAccessControlListAsync(string quantityId, string uomId, AccessControlList uomAcl);
```
***

## `Get Uom Owner`

Get the Owner of the specified unit of measure. For more information on Owners, see [Access Control](xref:accessControl).

#### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/Units/{uomId}/Owner
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

`string uomId`  
The unit of measure identifier

#### Response   
The response includes a status code and a response body.

##### Response Body  
The Owner for the specified Uom 

#### .NET client libraries method
```csharp
   Task<Trustee> GetQuantityUomOwnerAsync(string quantityId, string uomId);
```
***********************

## `Update Uom Owner`

Update the Owner of the specified unit of measure. For more information on Owners, see [Access Control](xref:accessControl).

#### Request
 ```text
    PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/Units/{uomId}/Owner
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

`string uomId`  
The unit of measure identifier

##### Request body 
Serialized Owner

#### Response    
The response includes a status code.

#### .NET client libraries method
```csharp
   Task UpdateQuantityUomOwnerAsync(string quantityId, string uomId, Trustee uomOwner);
```
***

## `Get Uom Access Rights`

Gets the Access Rights associated with the specified unit of measure for the requesting identity. For 
more information on Access Rights, see [Access Control](xref:accessControl#commonaccessrightsenum).

#### Request
 ```text
    GET api/v1//Tenants/{tenantId}/Namespaces/{namespaceId}/Quantities/{quantityId}/Units/{uomId}/AccessRights
 ```

##### Parameters

`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string quantityId`  
The quantity identifier  

`string uomId`  
The unit of measure identifier

#### Response  
The response includes a status code and a response body.

##### Response Body  
The Access Rights of the specified unit of measure for the requesting identity.

##### Example response body
```json
HTTP/1.1 200
Content-Type: application/json

["Read", "Write"]
```

#### .NET client libraries method
```csharp
   Task<string[]> GetQuantityUomAccessRightsAsync(string quantityId, string uomId);
```
***********************