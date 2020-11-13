
# Work with SdsTypes outside of .NET framework
SdsTypes must be built manually when .NET `SdsTypeBuilder` is unavailable. Below, you'll see how types are built and defined in
[Python](https://github.com/osisoft/OSI-Samples-OCS/tree/master/basic_samples/SDS/Python) and 
[JavaScript](https://github.com/osisoft/OSI-Samples-OCS/tree/master/basic_samples/SDS/JavaScript) samples. 
For samples in other languages, go to [OCS code samples in GitHub](https://github.com/osisoft/OSI-Samples-OCS/tree/master/basic_samples/SDS).

SdsType, SdsTypeProperty, and SdsTypeCode are defined below:

**Python**
```python
class SdsTypeCode(Enum):
    Empty = 0
    Object = 1
    DBNull = 2
    Boolean = 3
    Char = 4
      ...
class SdsTypeProperty(object):
    """SDS type property definition"""

    def __init__(self):
            self.__isKey = False

    @property
    def Id(self):
        return self.__id
    @Id.setter
    def Id(self, id):
        self.__id = id

      ...

    @property
    def IsKey(self):
        return self.__isKey
    @IsKey.setter
    def IsKey(self, iskey):
        self.__isKey = iskey

    @property
    def SdsType(self):
        return self.__SdsType
    @SdsType.setter
    def SdsType(self, SdsType):
        self.__SdsType=SdsType
      ...

class SdsType(object):
    """SDS type definitions"""
    def __init__(self):
        self.SdsTypeCode = SdsTypeCode.Object

    @property
    def Id(self):
        return self.__id
    @Id.setter
    def Id(self, id):
        self.__id = id

      ...

    @property
    def BaseType(self):
        return self.__baseType
    @BaseType.setter
    def BaseType(self, baseType):
        self.__baseType = baseType

    @property
    def SdsTypeCode(self):
        return self.__typeCode
    @SdsTypeCode.setter
    def SdsTypeCode(self, typeCode):
        self.__typeCode = typeCode

    @property
    def Properties(self):
        return self.__properties
    @Properties.setter
    def Properties(self, properties):
        self.__properties = properties
```


**JavaScript**
```javascript
SdsTypeCodeMap: {
    Empty: 0,
    "Object": 1,
    DBNull: 2,
    "Boolean": 3,
    Char: 4,
    ...
SdsTypeProperty: function (SdsTypeProperty) {
    if (SdsTypeProperty.Id) {
        this.Id = SdsTypeProperty.Id;
    }
    if (SdsTypeProperty.Name) {
        this.Name = SdsTypeProperty.Name;
    }
    if (SdsTypeProperty.Description) {
        this.Description = SdsTypeProperty.Description;
    }
    if (SdsTypeProperty.SdsType) {
        this.SdsType = SdsTypeProperty.SdsType;
    }
    if (SdsTypeProperty.IsKey) {
        this.IsKey = SdsTypeProperty.IsKey;
    }
},
SdsType: function (SdsType) {
    if (SdsType.Id) {
        this.Id = SdsType.Id
    }
    if (SdsType.Name) {
        this.Name = SdsType.Name;
    }
    if (SdsType.Description) {
        this.Description = SdsType.Description;
    }
    if (SdsType.SdsTypeCode) {
        this.SdsTypeCode = SdsType.SdsTypeCode;
    }
    if (SdsType.Properties) {
        this.Properties = SdsType.Properties;
    }
},
```

These are the SdsTypes we are working with in Python and JavaScript classes:

**Python**
```python
class State(Enum):
    Ok = 0
    Warning = 1
    Alarm = 2

class Simple(object):
    Time = property(getTime, setTime)
    def getTime(self):
        return self.__time
    def setTime(self, time):
        self.__time = time

    State = property(getState, setState)
    def getState(self):
        return self.__state
    def setState(self, state):
        self.__state = state

    Measurement = property(getMeasurement, setMeasurement)
    def getMeasurement(self):
        return self.__measurement
    def setMeasurement(self, measurement):
        self.__measurement = measurement
```

**JavaScript**
```javascript
var State =
{
    Ok: 0,
    Warning: 1,
    Alarm: 2,
}

var Simple = function () {
    this.Time = null;
    this.State = null;
    this.Measurement = null;
}
```

These are the SdsTypes defined in Python and JavaScript:

**Python**
```python
# Create the properties

# Time is the primary index
time = SdsTypeProperty()
time.Id = "Time"
time.Name = "Time"
time.IsKey = True
time.SdsType = SdsType()
time.SdsType.Id = "DateTime"
time.SdsType.Name = "DateTime"
time.SdsType.SdsTypeCode = SdsTypeCode.DateTime

# State is not a pre-defined type. A SdsType must be defined to represent the enum
stateTypePropertyOk = SdsTypeProperty()
stateTypePropertyOk.Id = "Ok"
stateTypePropertyOk.Value = State.Ok
stateTypePropertyWarning = SdsTypeProperty()
stateTypePropertyWarning.Id = "Warning"
stateTypePropertyWarning.Value = State.Warning
stateTypePropertyAlarm = SdsTypeProperty()
stateTypePropertyAlarm.Id = "Alarm"
stateTypePropertyAlarm.Value = State.Alarm

stateType = SdsType()
stateType.Id = "State"
stateType.Name = "State"
stateType.Properties = [ stateTypePropertyOk, stateTypePropertyWarning, \
                        stateTypePropertyAlarm ]

state = SdsTypeProperty()
state.Id = "State"
state.Name = "State"
state.SdsType = stateType

# Value property is a simple non-indexed, pre-defined type
value = SdsTypeProperty()
value.Id = "Measurement"
value.Name = "Measurement"
value.SdsType = SdsType()
value.SdsType.Id = "Double"
value.SdsType.Name = "Double"

# Create the Simple SdsType
simpleType = SdsType()
simpleType.Id = "Simple"
simpleType.Name = "Simple"
simpleType.Description = "Basic sample type"
simpleType.SdsTypeCode = SdsTypeCode.Object
simpleType.Properties = [ time ]
```

**JavaScript**
```javascript
// Time is the primary index
var timeProperty = new SdsObjects.SdsTypeProperty({
    "Id": "Time",
    "IsKey": true,
    "SdsType": new SdsObjects.SdsType({
        "Id": "dateType",
        "SdsTypeCode": SdsObjects.SdsTypeCodeMap.DateTime
    })
});

// State is not a pre-defined type. An SdsType must be defined to represent the enum
var stateTypePropertyOk = new SdsObjects.SdsTypeProperty({
    "Id": "Ok",
    "Value": State.Ok
});
var stateTypePropertyWarning = new SdsObjects.SdsTypeProperty({
    "Id": "Warning",
    "Value": State.Warning
});
var stateTypePropertyAlarm = new SdsObjects.SdsTypeProperty({
    "Id": "Alarm",
    "Value": State.Alarm
});

var stateType = new SdsObjects.SdsType({
    "Id": "State",
    "Name": "State",
    "SdsTypeCode": SdsObjects.SdsTypeCodeMap.Int32Enum,
    "Properties": [stateTypePropertyOk, stateTypePropertyWarning,
        stateTypePropertyAlarm, stateTypePropertyRed]
});

// Measurement property is a simple non-indexed, pre-defined type
var measurementProperty = new SdsObjects.SdsTypeProperty({
    "Id": "Measurement",
    "Name": "Measurement",
    "SdsType": new SdsObjects.SdsType({
        "Id": "doubleType",
        "SdsTypeCode": SdsObjects.SdsTypeCodeMap.Double
    })
});

// Create the Simple SdsType
var simpleType = new SdsObjects.SdsType({
    "Id": "Simple",
    "Name": "Simple", 
    "Description": "This is a simple SDS type ",
    "SdsTypeCode": SdsObjects.SdsTypeCodeMap.Object,
    "Properties": [timeProperty, stateProperty, measurementProperty]
});
```

Working with a derived class is easy. For example, this is a derived class:

```javascript
class Derived(Simple):
    @property
    def Observation(self):
        return self.__observation
    @Observation.setter
    def Observation(self, observation):
        self.__observation = observation
```

Extend the above SdsType as follows:

**Python**
```python
# Observation property is a simple non-indexed, standard data type
observation = SdsTypeProperty()
observation.Id = "Observation"
observation.Name = "Observation"
observation.SdsType = SdsType()
observation.SdsType.Id = "String"
observation.SdsType.Name = "String"
observation.SdsType.SdsTypeCode = SdsTypeCode.String

# Create the derived SdsType
derived = SdsType()
derived.Id = "Derived"
derived.Name = "Derived"
derived.Description = "Derived sample type"
derived.BaseType = simpleType # Set the base type to the derived type
derived.SdsTypeCode = SdsTypeCode.Object
derived.Properties = [ observation ]
```

**JavaScript**
```javascript
var observationProprety = new SdsObjects.SdsTypeProperty({
    "Id": "Observation",
    "SdsType": new SdsObjects.SdsType({
        "Id": "strType",
        "SdsTypeCode": SdsObjects.SdsTypeCodeMap.String
    })
});

var derivedType = new SdsObjects.SdsType({
    "Id": "Derived",
    "Name": "Derived",
    "Description": " Derived sample type",
    "BaseType": simpleType,
    "SdsTypeCode": SdsObjects.SdsTypeCodeMap.Object,
    "Properties": [ observationProprety ]
});
```

## Work with SdsTypes in .NET framework

When working in .NET, use the `SdsTypeBuilder` to create SdsTypes. The `SdsTypeBuilder` eliminates 
potential errors that can occur when working with SdsTypes manually.

There are several ways to work with the `SdsTypeBuilder`. One is to use the static methods for convenience:
```csharp
public enum State
{
    Ok,
    Warning,
    Alarm
}

public class Simple
{
    [SdsMember(IsKey = true, Order = 0)]
    public DateTime Time { get; set; }
    public State State { get; set; }
    public Double Measurement { get; set; }
}

SdsType simpleType = SdsTypeBuilder.CreateSdsType<Simple>();
simpleType.Id = "Simple";
simpleType.Name = "Simple";
simpleType.Description = "Basic sample type";
```

`SdsTypeBuilder` recognizes the ``System.ComponentModel.DataAnnotations.KeyAttribute`` and 
its own ``OSIsoft.Sds.SdsMemberAttribute``. When using the ``SdsMemberAttribute`` to specify 
the primary index, set the ``IsKey`` to true.

The SdsType is created with the following parameters. `SdsTypeBuilder` automatically generates 
unique identifiers. Note that the following table contains only a partial list of fields.

| Field            | Values                  |             |                                      |
|------------------|-------------------------|-------------|--------------------------------------|
| Id               | Simple                                                                       |
| Name             | Simple                                                                       |
| Description      | Basic sample type                                                            |
| Properties       | Count = 3                                                                    |
|   [0]            | Id                      | Time                                               |
|                  | Name                    | Time                                               |
|                  | Description             | null                                               |
|                  | Order                   | 0                                                  |
|                  | IsKey                   | true                                               |
|                  | SdsType                 | Id          | c48bfdf5-a271-384b-bf13-bd21d931c1bf |
|                  |                         | Name        | DateTime                             |
|                  |                         | Description | null                                 |
|                  |                         | Properties  | null                                 |
|                  | Value                   | null                                               |
|   [1]            | Id                      | State                                              |
|                  | Name                    | State                                              |
|                  | Description             | null                                               |
|                  | Order                   | 0                                                  |
|                  | IsKey                   | false                                              |
|                  | SdsType                 | Id          | 02728a4f-4a2d-3588-b669-e08f19c35fe5 |
|                  |                         | Name        | State                                |
|                  |                         | Description | null                                 |
|                  |                         | Properties  | Count = 3                            |
|                  |                         | [0]         | Id                | "Ok"             |
|                  |                         |             | Name              | null             |
|                  |                         |             | Description       | null             |
|                  |                         |             | Order             | 0                |
|                  |                         |             | SdsType           | null             |
|                  |                         |             | Value             | 0                |
|                  |                         | [1]         | Id                | "Warning"        |
|                  |                         |             | Name              | null             |
|                  |                         |             | Description       | null             |
|                  |                         |             | Order             | 0                |
|                  |                         |             | SdsType           | null             |
|                  |                         |             | Value             | 1                |
|                  |                         | [2]         | Id                | "Alarm"          |
|                  |                         |             | Name              | null             |
|                  |                         |             | Description       | null             |
|                  |                         |             | Order             | 0                |
|                  |                         |             | SdsType           | null             |
|                  |                         |             | Value             | 2                |
|                  | Value                   | null                                               |
|   [2]            | Id                      | Measurement                                        |
|                  | Name                    | Measurement                                        |
|                  | Description             | null                                               |
|                  | Order                   | 0                                                  |
|                  | IsKey                   | false                                              |
|                  | SdsType                 | Id          | 0f4f147f-4369-3388-8e4b-71e20c96f9ad |
|                  |                         | Name        | Double                               |
|                  |                         | Description | null                                 |
|                  |                         | Properties  | null                                 |
|                  | Value                   | null                                               |


The `SdsTypeBuilder` also supports derived types. Note that you need not add the base types to 
the SDS before using `SdsTypeBuilder`. Base types are maintained within the SdsType.
