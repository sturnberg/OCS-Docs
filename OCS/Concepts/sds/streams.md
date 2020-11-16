# Streams

Streams are collections of sequentially occurring values indexed by a single property, typically time series data.
You define Streams to organize incoming data from another system into the OCS.
To define a stream, you must first define a type, which defines the structure of the data you want to stream into a selected namespace.

SDS stores collections of events and provides convenient ways to find and associate events.
Events of consistent structure are stored in Streams. Streams are referenced by their identifier or `Id` field.
Stream identifiers must be unique within a namespace.

A stream must include a `TypeId` that references the identifier of an existing type.
Stream management using the .NET SDS client libraries is performed through `ISdsMetadataService`.
Create the `ISdsMetadataService`, using one of the ``Service.GetMetadataService()`` factory methods.

## Streams Metadata and Tags
Stream metadata is represented as a dictionary of string keys and associated string values. 
It can be used to associate additional information with a stream. Stream tags are represented 
as a list of strings. Tags can be used to categorize or denote special attributes of streams. 
The Stream Metadata API And Stream Tags API do not accept the search query parameter in their respective
Get calls. However, stream tags and metadata can be used as criteria in search query strings to return 
Stream results with the [Stream](xref:sdsStreams) API.
