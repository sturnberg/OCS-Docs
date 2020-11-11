
# SdsType API

The REST APIs provide programmatic access to read and write SDS data. The APIs in this section 
interact with SdsTypes. When working in .NET, convenient SDS Client Libraries are available. 
The ISdsMetadataService interface, accessed using the `SdsService.GetMetadataService()` helper, 
defines the available functions. See [Types](#types) for general type-related information.

***********************

## `Get Type`
Returns the type corresponding to the specified typeId within a given namespace.

### Request
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}
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
The requested SdsType

#### Example response body 
```json
HTTP/1.1 200
Content-Type: application/json

{
    "Id": "Simple",
    "Name": "Simple",
    "SdsTypeCode": 1,
    "Properties": [
        {
            "Id": "Time",
            "Name": "Time",
            "IsKey": true,
            "SdsType": {
                "Id": "19a87a76-614a-385b-ba48-6f8b30ff6ab2",
                "Name": "DateTime",
                "SdsTypeCode": 16
            }
        },
        {
            "Id": "State",
            "Name": "State",
            "SdsType": {
                "Id": "e20bdd7e-590b-3372-ab39-ff61950fb4f3",
                "Name": "State",
                "SdsTypeCode": 609,
                "Properties": [
                    {
                        "Id": "Ok",
                        "Value": 0
                    },
                    {
                        "Id": "Warning",
                        "Value": 1
                    },
                    {
                        "Id": "Alarm",
                        "Value": 2
                    }
                ]
            }
        },
        {
            "Id": "Measurement",
            "Name": "Measurement",
            "SdsType": {
                "Id": "6fecef77-20b1-37ae-aa3b-e6bb838d5a86",
                "Name": "Double",
                "SdsTypeCode": 14
            }
        }
    ]
}
```

### .NET client libraries method
```csharp
    Task<SdsType> GetTypeAsync(string typeId);
```

***********************

## `Get Type Reference Count`

Returns a dictionary mapping the object name to the number of references held by streams, stream views and parent types for the specified type. See [Streams](xref:sdsStreams) and [Steam Views](xref:sdsStreamViews) for more information on the use of types to define streams and stream views. For further details about type referencing please see: [Type Reusability](#type-reusability).

### Request
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}/ReferenceCount
 ```

### Parameters   

`string tenantId`  
The tenant identifier

`string namespaceId`  
The namespace identifier

`string typeId`  
The type identifier

#### Response  
The response includes a status code and a response body.

#### Response body  
A dictionary mapping object name to number of references.

#### Example response body 
```json
    {
        "SdsStream": 3,
        "SdsStreamView": 2,
        "SdsType": 1
    }
```

### .NET client libraries method
```csharp
    Task<IDictionary<string, int>> GetTypeReferenceCountAsync(string typeId);
```

***********************

## `Get Types`
Returns a list of types within a given namespace.

If specifying the optional search query parameter, the list of types returned will match 
the search criteria. If the search query parameter is not specified, the list will include 
all types in the Namespace. See [Search in SDS](xref:sdsSearching) 
for information about specifying those respective parameters.

Note that the results will also include types that were automatically created by SDS as a result of type referencing. For further details about type referencing please see: [Type Reusability](#type-reusability)

### Request
 ```text
	GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types?query={query}&skip={skip}&count={count}&orderby={orderby}
 ```

### Parameters   

`string tenantId`  
The tenant identifier

`string namespaceId`  
The namespace identifier

`string query`  
[Optional] Parameter representing a string search. See the [Search in SDS](xref:sdsSearching) topic for information about specifying the query parameter.

`int skip`  
[Optional] Parameter representing the zero-based offset of the first SdsType to retrieve.  If not specified, 
a default value of 0 is used.

`int count`  
[Optional] Parameter representing the maximum number of SdsTypes to retrieve. If not specified, a default value of 100 is used.

`string orderby`  
[Optional] Parameter representing sorted order which SdsTypes will be returned. A field name is required. The sorting is based on the stored values for the given field (of type string). For example, ``orderby=name`` would sort the returned results by the ``name`` values (ascending by default). 
Additionally, a value can be provided along with the field name to identify whether to sort ascending or descending, by using values ``asc`` or ``desc``, respectively. For example, ``orderby=name desc`` would sort the returned results by the ``name`` values, descending.
If no value is specified, there is no sorting of results.

#### Response  
The response includes a status code and a response body.

#### Response body  
A collection of zero or more SdsTypes

#### Example response body 
```json
HTTP/1.1 200
Content-Type: application/json

[    
    {
        "Id": "Simple",
        "Name": "Simple",
        "SdsTypeCode": 1,
        "Properties": [
            {
                "Id": "Time",
                "Name": "Time",
                "IsKey": true,
                "SdsType": {
                    "Id": "19a87a76-614a-385b-ba48-6f8b30ff6ab2",
                    "Name": "DateTime",
                    "SdsTypeCode": 16
                }
            },
            {
                "Id": "State",
                "Name": "State",
                "SdsType": {
                    "Id": "e20bdd7e-590b-3372-ab39-ff61950fb4f3",
                    "Name": "State",
                    "SdsTypeCode": 609,
                    "Properties": [
                        {
                            "Id": "Ok",
                            "Value": 0
                        },
                        {
                            "Id": "Warning",
                            "Value": 1
                        },
                        {
                            "Id": "Alarm",
                            "Value": 2
                        }
                    ]
                }
            },
            {
                "Id": "Measurement",
                "Name": "Measurement",
                "SdsType": {
                    "Id": "6fecef77-20b1-37ae-aa3b-e6bb838d5a86",
                    "Name": "Double",
                    "SdsTypeCode": 14
                }
            }
        ]
    },
    …
]
```


### .NET client libraries method
```csharp
    Task<IEnumerable<SdsType>> GetTypesAsync(string query = "", int skip = 0, int count = 100);
```

***********************

## `Get or Create Type`

Creates the specified type. If a type with a matching identifier already exists, SDS compares the 
existing type with the type that was sent.

If the types are identical, a ``Found`` (302) error 
is returned with the Location header set to the URI where the type may be retrieved using a Get function. 

If the types do not match, a ``Conflict`` (409) error is returned.
Note that a ``Conflict`` (409) error will also be returned if the type contains reference to any existing type, but the referenced type definition in the body does not match the existing type. You may reference an existing type without including the reference type definition in the body by using only the Ids. For further details about type referencing please see: [Type Reusability](#type-reusability).

For a matching type (``Found``), clients that are capable of performing a redirect that includes the 
authorization header can automatically redirect to retrieve the type. However, most clients, 
including the .NET HttpClient, consider redirecting with the authorization token to be a security vulnerability.

When a client performs a redirect and strips the authorization header, SDS cannot authorize the request and 
returns ``Unauthorized`` (401). For this reason, it is recommended that when using clients that do not 
redirect with the authorization header, you should disable automatic redirect and perform the redirect manually.

### Request
 ```text
	POST api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}
 ```

### Parameters 

`string tenantId`  
The tenant identifier

`string namespaceId`  
The namespace identifier

`string typeId`  
The type identifier. The identifier must match the `SdsType.Id` field in the request body. 

#### Request body 
The request content is the serialized SdsType.

#### Example request body
```json
{
    "Id": "Simple",
    "Name": "Simple",
    "SdsTypeCode": 1,
    "Properties": [
        {
            "Id": "Time",
            "Name": "Time",
            "IsKey": true,
            "SdsType": {
                "Id": "19a87a76-614a-385b-ba48-6f8b30ff6ab2",
                "Name": "DateTime",
                "SdsTypeCode": 16
            }
        },
        {
            "Id": "State",
            "Name": "State",
            "SdsType": {
                "Id": "e20bdd7e-590b-3372-ab39-ff61950fb4f3",
                "Name": "State",
                "SdsTypeCode": 609,
                "Properties": [
                    {
                        "Id": "Ok",
                        "Value": 0
                    },
                    {
                        "Id": "Warning",
                        "Value": 1
                    },
                    {
                        "Id": "Alarm",
                        "Value": 2
                    }
                ]
            }
        },
        {
            "Id": "Measurement",
            "Name": "Measurement",
            "SdsType": {
                "Id": "6fecef77-20b1-37ae-aa3b-e6bb838d5a86",
                "Name": "Double",
                "SdsTypeCode": 14
            }
        }
    ]
}
```

### Response  
The response includes a status code and a response body.

#### Response body  
The request content is the serialized SdsType. If you are not using the SDS Client Libraries, it is recommended that you use JSON.

#### Example response body 
```json
HTTP/1.1 201
Content-Type: application/json

{
    "Id": "Simple",
    "Name": "Simple",
    "Description": null,
    "SdsTypeCode": 1,
    "IsGenericType": false,
    "IsReferenceType": false,
    "GenericArguments": null,
    "Properties": [
        {
            "Id": "Time",
            "Name": "Time",
            "Description": null,
            "Order": 0,
            "IsKey": true,
            "FixedSize": 0,
            "SdsType": {
                "Id": "19a87a76-614a-385b-ba48-6f8b30ff6ab2",
                "Name": "DateTime",
                "Description": null,
                "SdsTypeCode": 16,
                "IsGenericType": false,
                "IsReferenceType": false,
                "GenericArguments": null,
                "Properties": null,
                "BaseType": null,
                "DerivedTypes": null,
                "InterpolationMode": 0,
                "ExtrapolationMode": 0
            },
            "Value": null,
            "Uom": null,
            "InterpolationMode": null
        },
        {
            "Id": "State",
            "Name": "State",
            "Description": null,
            "Order": 0,
            "IsKey": false,
            "FixedSize": 0,
            "SdsType": {
                "Id": "e20bdd7e-590b-3372-ab39-ff61950fb4f3",
                "Name": "State",
                "Description": null,
                "SdsTypeCode": 609,
                "IsGenericType": false,
                "IsReferenceType": false,
                "GenericArguments": null,
                "Properties": [
                    {
                        "Id": "Ok",
                        "Name": null,
                        "Description": null,
                        "Order": 0,
                        "IsKey": false,
                        "FixedSize": 0,
                        "SdsType": null,
                        "Value": 0,
                        "Uom": null,
                        "InterpolationMode": null
                    },
                    {
                        "Id": "Warning",
                        "Name": null,
                        "Description": null,
                        "Order": 0,
                        "IsKey": false,
                        "FixedSize": 0,
                        "SdsType": null,
                        "Value": 1,
                        "Uom": null,
                        "InterpolationMode": null
                    },
                    {
                        "Id": "Alarm",
                        "Name": null,
                        "Description": null,
                        "Order": 0,
                        "IsKey": false,
                        "FixedSize": 0,
                        "SdsType": null,
                        "Value": 2,
                        "Uom": null,
                        "InterpolationMode": null
                    }
                ],
                "BaseType": null,
                "DerivedTypes": null,
                "InterpolationMode": 0,
                "ExtrapolationMode": 0
            },
            "Value": null,
            "Uom": null,
            "InterpolationMode": null
        },
        {
            "Id": "Measurement",
            "Name": "Measurement",
            "Description": null,
            "Order": 0,
            "IsKey": false,
            "FixedSize": 0,
            "SdsType": {
                "Id": "6fecef77-20b1-37ae-aa3b-e6bb838d5a86",
                "Name": "Double",
                "Description": null,
                "SdsTypeCode": 14,
                "IsGenericType": false,
                "IsReferenceType": false,
                "GenericArguments": null,
                "Properties": null,
                "BaseType": null,
                "DerivedTypes": null,
                "InterpolationMode": 0,
                "ExtrapolationMode": 0
            },
            "Value": null,
            "Uom": null,
            "InterpolationMode": null
        }
    ],
    "BaseType": null,
    "DerivedTypes": null,
    "InterpolationMode": 0,
    "ExtrapolationMode": 0
}
```

### .NET client libraries method
```csharp
    Task<SdsType> GetOrCreateTypeAsync(SdsType sdsType)
```

If a type with a matching identifier already exists and it matches the type in the request body, 
the client redirects a GET to the Location header. If the existing type does not match the type
in the request body, a Conflict error response is returned and the client library method throws an exception. 

The .NET SDS Client Libraries manage redirects.

***********************

## `Delete Type`

Deletes a type from the specified tenant and namespace. Note that a type cannot be deleted if any streams, stream views, or other types reference it.

### Request
 ```text
	DELETE api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}
 ```

### Parameters 

`string tenantId`  
The tenant identifier

`string namespaceId`  
The namespace identifier

`string typeId`  
The type identifier

### Response  
The response includes a status code.

### .NET client libraries method
```csharp
    Task DeleteTypeAsync(string typeId);
```

***********************

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