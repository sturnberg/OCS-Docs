# Units API
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


