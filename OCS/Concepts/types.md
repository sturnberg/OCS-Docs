# Types
The Sequential Data Store (SDS) stores streams of events and provides convenient ways to find and associate 
events. Events are stored in SdsStreams (or streams). An SdsType (or type) defines the shape or structure of the 
event and how to associate events within the stream.

Define simple atomic types, such as integers, floats, strings, arrays, and dictionaries, or 
complex or nested types using the [Properties collection of SdsTypes](#sdstypeproperty). 

An SdsType used to define an SdsStream must have a key. A key is a [Property, or a combination of Properties](#sdstypeproperty) 
that constitutes an ordered, unique identity. If the key is ordered so it functions as an index, it is 
known as the *primary index*. While a timestamp (``DateTime``) is a very common type of index, any type that 
can be ordered is permitted. Secondary and other indexes are defined in the stream. 
For more information, see [Indexes](xref:sdsIndexes).

When defining an SdsType, consider how the events will be represented in an SdsStream as the SdsType defines 
each event in an SdsStream. An event is a single unit whose properties have values that relate to the 
index; that is, each property of a type event is related to the event's index. Each event is a single unit.

An SdsType is referenced by its identifier or ``Id`` field. SdsType identifiers must be unique within a namespace.

An SdsType can also refer other SdsTypes by using their identifiers. This enables type re-usability.
Nested types and base types are automatically created as separate types. For more information, see [Type Reusability](#type-reusability).

SdsTypes define how events are read and associated within a collection of SdsStreams. The read 
characteristics when attempting to read non-existent indexes, indexes that fall between, before or after 
existing indexes, are determined by the interpolation and extrapolation settings of the SdsType. For more 
information about read characteristics, see [Interpolation](xref:sdsReadingData#interpolation) and [Extrapolation](xref:sdsReadingData#extrapolation).

SdsTypes are immutable. After an SdsType is created, its definition cannot be updated. An SdsType must be deleted and recreated if the definition is incorrect.
In addition, an SdsType may be deleted only if no SdsStreams, SdsStreamViews, or other SdsTypes reference it.

Only the SdsTypes that are used to define SdsStreams or SdsStreamViews are required to be added to the SDS. 
SdsTypes that define [Properties](#sdstypeproperty) or base types are contained within the parent type so they don't need to be added to the SDS independently.
