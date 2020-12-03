# Stream Views
StreamViews (or stream views) provide flexibility in the use of types.
While you cannot actually change the properties of types themselves,
the stream views feature enables you to create a view of a selected Stream that appears as if you had changed the type on which it is based.
You create a stream view by choosing a source and target type then a set of mappings between properties of those two types. Using a stream view to leverage existing type properties is preferable to creating a new type, because the stream that is based on the type continues to function with its previously archived stream data intact.

StreamView is used to specify the mapping between the source and target types.
Use a PUT method to assign a stream view to a stream, and display the stream data specified for the selected stream view with a GET method. For more information, see [Reading with StreamViews](xref:sdsReadingData#reading-with-sdsstreamviews).

To assign a stream view to a stream, execute an [Update Stream Type](xref:sdsStreams#update-stream-type) call. By specifying the stream view ID, you can effectively assign the target type of the stream view to a specified stream. 

SDS attempts to determine how to map properties from the source to the target. When the mapping 
is straightforward, such as when the properties are in the same position and of the same data type, 
or when the properties have the same name, SDS will map the properties automatically. When SDS is unable to determine how to map a source property, the property is removed. If SDS encounters 
a target property that it cannot map to, the property is added and configured with a default value.
For more information, see [Stream views mapping](#stream-views-mapping) below.

## "Changing" the stream type

You use stream views to change the type that defines a stream. You cannot modify the type itself as types are immutable. 
But you can map a stream from its current type to a different type by way of stream view.

To update a type of a stream, define a stream view and do the following:
```text
   PUT api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Type?streamViewId={streamViewId}
```

For more information, see [Update Stream Type](xref:sdsStreams#update-stream-type).

