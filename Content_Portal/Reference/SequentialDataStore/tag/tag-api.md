# Streams Tags API 

## `Get stream tags`  
Returns the tag list for the specified stream. 

### Request
 ```text
      GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Tags 
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
The tags for the specified SdsStream   

#### Example response body
```json
HTTP/1.1 200 
Content-Type: application/json

[ 
    "a tag", 
    "another tag" 
] 
```  

### .NET client libraries method
```csharp
      Task<IList<string>> GetStreamTagsAsync(string streamId); 
```

***********************
## `Update stream tags`
Replaces the tag list for the specified stream with the tags listed in the request body.
Overwrites any existing tags; does not merge. 

### Request
 ```text
      PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Tags 
 ```

### Parameters  
`string tenantId`  
The tenant identifier    
  
`string namespaceId`  
The namespace identifier  
  
`string streamId`  
The stream identifier  

#### Request body  
The request content is the serialized list of tags 

### Authorization  
Allowed by administrator accounts  

### Response  
The response includes a status code  

### .NET client libraries method
```csharp
      Task UpdateStreamTagsAsync(string streamId, IList<string> tags); 
```

***********************
## `Delete stream tags`
Deletes the tag list for the specified stream. 

### Request
 ```text
      DELETE api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Tags 
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
      Task DeleteStreamTagsAsync(string streamId); 
```

***********************