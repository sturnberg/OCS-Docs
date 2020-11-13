# Types
The Sequential Data Store (SDS) stores streams of events and provides convenient ways to find and associate 
events. Events are stored in Streams (or streams). An Type (or type) defines the shape or structure of the 
event and how to associate events within the stream.

Define simple atomic types, such as integers, floats, strings, arrays, and dictionaries, or 
complex or nested types using the [Properties collection of Types](#sdstypeproperty). 

An Type used to define an Stream must have a key. A key is a [Property, or a combination of Properties](#sdstypeproperty) 
that constitutes an ordered, unique identity. If the key is ordered so it functions as an index, it is 
known as the *primary index*. While a timestamp (``DateTime``) is a very common type of index, any type that 
can be ordered is permitted. Secondary and other indexes are defined in the stream. 
For more information, see [Indexes](xref:sdsIndexes).

When defining an Type, consider how the events will be represented in an Stream as the Type defines 
each event in an Stream. An event is a single unit whose properties have values that relate to the 
index; that is, each property of a type event is related to the event's index. Each event is a single unit.

An Type is referenced by its identifier or ``Id`` field. Type identifiers must be unique within a namespace.

An Type can also refer other Types by using their identifiers. This enables type re-usability.
Nested types and base types are automatically created as separate types. For more information, see [Type Reusability](#type-reusability).

Types define how events are read and associated within a collection of Streams. The read 
characteristics when attempting to read non-existent indexes, indexes that fall between, before or after 
existing indexes, are determined by the interpolation and extrapolation settings of the Type. For more 
information about read characteristics, see [Interpolation](xref:sdsReadingData#interpolation) and [Extrapolation](xref:sdsReadingData#extrapolation).

Types are immutable. After an Type is created, its definition cannot be updated. An Type must be deleted and recreated if the definition is incorrect.
In addition, an Type may be deleted only if no Streams, StreamViews, or other Types reference it.

Only the Types that are used to define Streams or StreamViews are required to be added to the SDS. 
Types that define [Properties](#sdstypeproperty) or base types are contained within the parent type so they don't need to be added to the SDS independently.
