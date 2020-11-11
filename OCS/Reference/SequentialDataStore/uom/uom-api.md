# SdsUom API
The REST APIs provide programmatic access to read and write SDS data. The APIs in this section interact with SdsUoms. When working in .NET, convenient SDS Client Libraries are available. The ``ISdsMetadataService`` interface, accessed using the ``SdsService.GetMetadataService( )`` helper, defines the available functions. See [Units of Measure](#units-of-measure) for general [SdsUom](#sdsuom) information.

***

## ``Get Uom``

Returns the unit of measure corresponding to the specified uomId within a given namespace.

#### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Units/{uomId}
 ```
##### Parameters
`string tenantId`  
The tenant identifier  

`string namespaceId`  
The namespace identifier  

`string uomId`  
The unit of measure identifier

#### Response   
The response includes a status code and a response body.

##### Response body   
The requested SdsUom

##### Example response body when `uomId = "ounce"` is passed
```json
HTTP/1.1 200
Content-Type: application/json

{
    "Id": "ounce",
    "Abbreviation": "oz",
    "Name": "ounce",
    "DisplayName": "ounce",
    "QuantityId": "Mass",
    "ConversionFactor": 0.028349523
}
```
#### .NET client libraries method
```csharp
   Task<SdsUom> GetUomAsync(string uomId);
```
***

## ``Get Uoms``

Returns a list of all available units of measure in the system.

#### Request
 ```text
    GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Units?skip={skip}&count={count}
 ```
##### Parameters
``string tenantId``  
The tenant identifier  

``string namespaceId``  
The namespace identifier  

``int skip``  
An optional parameter representing the zero-based offset of the first SdsUomQuantity to retrieve. If not specified, a default value of 0 is used.

``int count``  
An optional parameter representing the maximum number of SdsUomQuantity to retrieve. If not specified, a default value of 100 is used.

#### Response  
The response includes a status code and a response body.

##### Response body    
A list of SdsUom objects

##### Example response body
```json
HTTP/1.1 200
Content-Type: application/json
[
    {
        "Id": "count",
        "Abbreviation": "count",
        "Name": "count",
        "DisplayName": "count",
        "QuantityId": "Quantity",
        "ConversionFactor": 1
    },
    {
        "Id": "Ampere hour",
        "Abbreviation": "Ah",
        "Name": "Ampere hour",
        "DisplayName": "Ampere hour",
        "QuantityId": "Electric Charge",
        "ConversionFactor": 3600
    },
    {
        "Id": "coulomb",
        "Abbreviation": "C",
        "Name": "coulomb",
        "DisplayName": "coulomb",
        "QuantityId": "Electric Charge",
        "ConversionFactor": 1
    }
    ...
]
```
#### .NET client libraries method
```csharp
   Task<IEnumerable<SdsUom>> GetUomsAsync(int skip = 0, int count = 100);
```
***


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