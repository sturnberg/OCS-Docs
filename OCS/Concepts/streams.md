# Streams

SdsStreams are collections of sequentially occurring values indexed by a single property, typically time series data.
You define SdsStreams to organize incoming data from another system into the OCS.
To define an SdsStream, you must first define an SdsType, which defines the structure of the data you want to stream into a selected namespace.

SDS stores collections of events and provides convenient ways to find and associate events.
Events of consistent structure are stored in SdsStreams. SdsStreams are referenced by their identifier or `Id` field.
SdsStream identifiers must be unique within a namespace.

An SdsStream must include a `TypeId` that references the identifier of an existing SdsType.
SdsStream management using the .NET SDS client libraries is performed through `ISdsMetadataService`.
Create the `ISdsMetadataService`, using one of the ``SdsService.GetMetadataService()`` factory methods.