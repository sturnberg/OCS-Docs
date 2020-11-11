# Stream Views
SdsStreamViews (or stream views) provide flexibility in the use of SdsTypes.
While you cannot actually change the properties of SdsTypes themselves,
the stream views feature enables you to create a view of a selected SdsStream that appears as if you had changed the SdsType on which it is based.
You create a stream view by choosing a source and target type then a set of mappings between properties of those two types. 
Using a stream view to leverage existing SdsType properties is preferable to creating a new SdsType, because the SdsStream that is based on the SdsType continues to function with its previously archived stream data intact.

SdsStreamView is used to specify the mapping between the source and target types.
Use a PUT method to assign a stream view to a stream, and display the stream data specified for the selected stream view with a GET method. For more information, see [Reading with SdsStreamViews](xref:sdsReadingData#reading-with-sdsstreamviews).

To assign an SdsStreamView to an SdsStream, execute an [Update Stream Type](xref:sdsStreams#update-stream-type) call.  By specifying the stream view ID, you can effectively assign the target type of the stream view to a specified stream. 

SDS attempts to determine how to map properties from the source to the target. When the mapping 
is straightforward, such as when the properties are in the same position and of the same data type, 
or when the properties have the same name, SDS will map the properties automatically. When SDS is unable to determine how to map a source property, the property is removed. If SDS encounters 
a target property that it cannot map to, the property is added and configured with a default value.
For more information, see [Stream views mapping](#stream-views-mapping) below.

## "Changing" the stream type

You use SdsStreamViews to change the SdsType that defines an SdsStream. You cannot modify the SdsType itself as types are immutable. 
But you can map an SdsStream from its current SdsType to a different SdsType by way of stream view.

To update an SdsType of an SdsStream, define an SdsStreamView and do the following:
```text
   PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Type?streamViewId={streamViewId}
```

For more information, see [Update Stream Type](xref:sdsStreams#update-stream-type).

### Stream views mapping

SDS automatically maps properties from the source to the target type when it is straightforward:
 - The properties are in the same position
 - The properties are of the same data type
 - The properties are of the same name

See [Work with SdsStreamViews in .NET framework](#work-with-sdsstreamviews-in-net-framework) below for how automatic mapping works.  

If needed, you can specify mapping. SDS largely supports mapping within the same data type. 

**Mapping compatibility chart**
 
| Source type\ Target type    | Numeric types 	| Nullable numeric types 	| Enumeration types 	| Nullable enumeration types 	| Object types    	| 
|----------------------------	|---------------	|------------------------	|-------------------	|----------------------------	|--------------------|
| Numeric types              	| Yes           	| Yes                    	| No                	| No                         	| No                 |
| Nullable numeric types     	| Yes           	| Yes                    	| No                	| No                         	| No                 |
| Enumeration types          	| No            	| No                     	| Yes               	| Yes                        	| No                 |
| Nullable enumeration types 	| No            	| No                     	| Yes               	| Yes                        	| No                 | 
| Object types               	| No            	| No                     	| No                	| No                         	| Yes*               |

\*: Mappable if `typeId` matches between the source and the target type 