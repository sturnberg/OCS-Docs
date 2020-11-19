# Stream metadata API 

## `Get stream metadata`
Returns the metadata dictionary for the specified stream.   

### Request  
 ```text
      GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Metadata 
 ```

### Parameters  
`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

### Authorization
Allowed for administrator and user accounts
  
### Response  
The response includes a status code and a response body  

#### Response body  
The metadata for the specified SdsStream

#### Example response body
```json
HTTP/1.1 200 
Content-Type: application/json 

{ 
   "a metadata key":"a metadata value", 
   "another key":"another value" 
} 
```

#### .NET client libraries method
```csharp
      Task<IDictionary<string, string>> GetStreamMetadataAsync(string streamId); 
```
  
***********************

## `Get stream metadata value`
Returns the value for the specified key in the metadata dictionary of the specified stream.  

### Request
 ```text
      GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Metadata/{key} 
 ```

### Parameters
`string tenantId`  
The tenant identifier  
  
`string namespaceId`   
The namespace identifier   
  
`string streamId`  
The stream identifier   
  
`string key`  
The key specifying the metadata value of interest  

### Authorization  
Allowed for administrator and user accounts  

### Response  
The response includes a status code and a response body  

#### Response body  
The metadata for the specified SdsStream 

#### Example response body
```json
HTTP/1.1 200 
Content-Type: application/json 

{ 
   "a metadata value"
} 
```

### .NET client libraries method  
```csharp
      Task<string> GetStreamMetadataValueAsync(string streamId, string key); 
```

***********************

## `Update stream metadata`
Replaces the metadata for the specified stream with the metadata in the request body. 
Overwrites any existing metadata; does not merge.  

### Request
 ```text
      PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Metadata 
 ```

### Parameters  
`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

### Authorization  
Allowed for administrator accounts  

### Response  
The response includes a status code  

### .NET client libraries method  
```csharp
      Task UpdateStreamMetadataAsync(string streamId, IDictionary<string, string> metadata); 
```

***********************

## `Patch stream metadata`
Modifies the metadata based on operations specified in the request body. The request body follows
[JSON Patch format](http://jsonpatch.com/).

### Request  
 ```text
      PATCH api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Metadata 
 ```

### Parameters  
`string tenantId`  
The tenant identifier    
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

### Authorization  
Allowed for administrator accounts

### Response
The response includes a status code and a response body  

#### Response body  
A collection of operations to be applied to the metadata collection as specified by the [JSON Patch format](http://jsonpatch.com/)  

### .NET client libraries method
```csharp
      Task<IDictionary<string, string>> PatchStreamMetadataAsync(string streamId, MetadataPatchDocument patchDoc);
```

***********************

## `Delete stream metadata`
Deletes the metadata for the specified stream.  

### Request
 ```text
      DELETE api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Metadata 
 ```

### Parameters  
`string tenantId`  
The tenant identifier  
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  
  
### Authorization  
Allowed for administrator accounts  

### Response  
The response includes a status code  


### .NET client libraries method
```csharp
      Task DeleteStreamMetadataAsync(string streamId); 
```

***********************

