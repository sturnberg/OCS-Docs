# Types
The Sequential Data Store (SDS) stores streams of events and provides convenient ways to find and associate 
events. Events are stored in Streams (or streams). a type (or type) defines the shape or structure of the 
event and how to associate events within the stream.

Define simple atomic types, such as integers, floats, strings, arrays, and dictionaries, or 
complex or nested types using the [Properties collection of Types](#sdstypeproperty). 

A type used to define a stream must have a key. A key is a [Property, or a combination of Properties](#sdstypeproperty) 
that constitutes an ordered, unique identity. If the key is ordered so it functions as an index, it is 
known as the *primary index*. While a timestamp (``DateTime``) is a very common type of index, any type that 
can be ordered is permitted. Secondary and other indexes are defined in the stream. 
For more information, see [Indexes](xref:sdsIndexes).

When defining a type, consider how the events will be represented in a stream as the type defines 
each event in a stream. An event is a single unit whose properties have values that relate to the 
index; that is, each property of a type event is related to the event's index. Each event is a single unit.

A type is referenced by its identifier or ``Id`` field. Type identifiers must be unique within a namespace.

A type can also refer other types by using their identifiers. This enables type re-usability.
Nested types and base types are automatically created as separate types. For more information, see [Type Reusability](#type-reusability).

Types define how events are read and associated within a collection of streams. The read 
characteristics when attempting to read non-existent indexes, indexes that fall between, before or after 
existing indexes, are determined by the interpolation and extrapolation settings of the Type. For more 
information about read characteristics, see [Interpolation](xref:sdsReadingData#interpolation) and [Extrapolation](xref:sdsReadingData#extrapolation).

Types are immutable. After a type is created, its definition cannot be updated. a type must be deleted and recreated if the definition is incorrect.
In addition, a type may be deleted only if no streams, stream views, or other types reference it.

Only the types that are used to define streams or stream views are required to be added to the SDS. 
Types that define [Properties](#sdstypeproperty) or base types are contained within the parent type so they don't need to be added to the SDS independently.

## Type Reusability
SdsTypes can also refer to other types by using their identifiers. This enables type re-usability.
For example, if there is a common index and value property for a group of types that may have additional properties,
a base type can be created with those properties.

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
                "SdsTypeCode": 16
            }
        },
        {
            "Id": "Measurement",
            "Name": "Measurement",
            "SdsType": {
                "SdsTypeCode": 14
            }
        }
    ]
}
```

If a new type should be created with properties in addition to the ones shown above,
a reference to the base type can be added by simply specifying the base type's ``Id``.

```json
{
    "Id": "Complex",
    "Name": "Complex",
    "SdsTypeCode": 1,
    "BaseType":{
        "Id":"Simple"
    },
    "Properties": [
        {
            "Id": "Depth",
            "Name": "Depth",
            "SdsType": {
                "SdsTypeCode": 14
            }
        }
    ]
}
```

The new type may also include the full type definition of the reference type instead of specifying only the ``Id`` as shown below:

```json
{
    "Id": "Complex",
    "Name": "Complex",
    "SdsTypeCode": 1,
    "BaseType":{
        "Id": "Simple",
        "Name": "Simple",
        "SdsTypeCode": 1,
        "Properties": [
            {
                "Id": "Time",
                "Name": "Time",
                "IsKey": true,
                "SdsType": {
                    "SdsTypeCode": 16
                }
            },
            {
                "Id": "Measurement",
                "Name": "Measurement",
                "SdsType": {
                    "SdsTypeCode": 14
                }
            }
        ]
    },
    "Properties": [
        {
            "Id": "Depth",
            "Name": "Depth",
            "SdsType": {
                "SdsTypeCode": 14
            }
        }
    ]
}
```

If the full definition is sent, the referenced types (base type "Simple" in the above example)
should match the actual type that was initially created. If the full definition is sent and the referenced types do not exist,
they will be created automatically by the SDS. Further type creations can reference them as shown above.
Note that when trying to get types back from the SDS, the results will also include types that were automatically created by the SDS.

Base types and properties of type Object, Enum, or user-defined collections such as Array, List and Dictionary,
will be treated as referenced types. Note that streams cannot be created using these referenced types.
If a stream of particular type is to be created, the type should contain at least one property
with a valid index type as described in the [Indexes](xref:sdsIndexes) section. 
The index property may also be in the base type as shown in the example above.

This works seamlessly when using any programming language, using .NET for example:

```csharp

public class Basic
{
    [SdsMember(IsKey = true, Order = 0)]
    public DateTime Time { get; set; }

    public double Temperature { get; set; }
}

public class EngineMonitor : Basic
{
    public double PistonSpeed { get; set; }
}

public class WindShieldMonitor : Basic
{
    public double Luminance { get; set; }
}

SdsType engineType = SdsTypeBuilder.CreateSdsType<EngineMonitor>();
engineType.Id = "Engine";
engineType.BaseType.Id = "Basic";

SdsType windShieldType = SdsTypeBuilder.CreateSdsType<WindShieldMonitor>();
windShieldType.Id = "WindShield";
windShieldType.BaseType.Id = "Basic";

```

Note that if necessary, the base type's Id can also be changed to be more meaningful.
