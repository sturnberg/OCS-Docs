# Data Characteristics

When data is requested at an index for which no stored event exists, the read characteristics determine 
whether the result is an error, no event, interpolated event, or extrapolated event. The combination of 
the type of the index and the interpolation and extrapolation modes of the SdsType and the SdsStream 
determine the read characteristics.

**\*Notes:** Use the ISO 8601 representation of dates and times in SDS, `2020-02-20T08:30:00-08:00` for February 20, 2020 at 8:30 AM PST, for example.
SDS returns timestamps in UTC if the timestamp is of property `DateTime` and in local time if it is of `DateTimeOffset`. 

## Interpolation

Interpolation determines how a stream behaves when asked to return an event at an index between 
two existing events. InterpolationMode determines how the returned event is constructed. SDS provides 
multiple ways to set the interpolation mode to get the desired behavior. The table 
below lists InterpolationModes:

|Mode                       |Enumeration value |Operation |
|---------------------------|------------------|----------|
|Default                    |0                 |The default InterpolationMode is Continuous |
|Continuous                 |0                 |Returns interpolated data using previous and next index values | 
|StepwiseContinuousLeading  |1                 |Returns the data from the previous index  |
|StepwiseContinuousTrailing |2                 |Returns the data from the next index |
|Discrete                   |3                 |No event is returned |
|ContinuousNullableLeading  |4                 |Returns interpolated data or data from the previous index if either of the surrounding indexes has a null value|
|ContinuousNullableTrailing |5                 |Returns interpolated data or data from the trailing index if either of the surrounding indexes has a null value|

Note that `Continuous` cannot return values for type properties that cannot be interpolated, such as when the type property is not numeric. 

The table below describes how the **Continuous InterpolationMode** affects
properties that occur between data in a stream:
**InterpolationMode = Continuous or Default**

| Property Type             | Result for a property for an index between data in a stream  | Comment |
|---------------------------|--------------------------------------------------------------|---------|
|Numeric Types              |Interpolated*                   |Rounding is done as needed for integer types |
|Time-related Types         |Interpolated                    |DateTime, DateTimeOffset, TimeSpan |
|Nullable Types             |Interpolated**                  |Limited support for nullable numeric types |
|Array and List Types       |Default value                   |         |
|String Type                |Default value                   |         |
|Boolean Type               |Returns value of nearest index  |         |
|Enumeration Types          |Returns Enum value at 0         |This may have a value for the enumeration |
|GUID                       |Default value                   |         |
|Version                    |Default value                   |         |
|IDictionary or IEnumerable |Default value                   |Dictionary, Array, List, and so on. |
|Empty Type		|Not supported                  	 | |
|Object Type 		|Not supported                   	| |


*When extreme values are involved in an interpolation (for example
Decimal.MaxValue) the call might result in a BadRequest exception.

\**For the `Continuous` interpolation mode, Nullable types are interpolated in the same manner as their non-nulllable equivalents as long as the values surrounding the desired interpolation index are non-null. If either of the values are null, the interpolated value will be null.

If the InterpolationMode is not assigned, the events are interpolated in the default manner, unless the interpolation 
mode is overridden in the SdsTypeProperty or the SdsStream. For more information on overriding the interpolation mode 
on a specific type property see [SdsTypeProperty](xref:sdsTypes#sdstypeproperty). For more information on overriding the interpolation mode for a specific stream see [Sds Streams](xref:sdsStreams).


## Extrapolation

Extrapolation defines how a stream responds to requests with indexes that precede or follow all 
data in the steam. ExtrapolationMode acts as a master switch to determine whether extrapolation 
occurs and at which end of the data. 

ExtrapolationMode works with the InterpolationMode to determine how a stream responds. The following tables 
show how ExtrapolationMode affects returned values for each InterpolationMode value:

**ExtrapolationMode with InterpolationMode = Default (or Continuous), StepwiseContinuousLeading, and StepwiseContinuousTrailing**

| ExtrapolationMode   | Enumeration value   | Index before data          | Index after data          |
|---------------------|---------------------|----------------------------|---------------------------|
| All                 | 0                   | Returns first data value   | Returns last data value   |
| None                | 1                   | No event is returned       | No event is returned      |
| Forward             | 2                   | No event is returned       | Returns last data value   |
| Backward            | 3                   | Returns first data value   | No event is returned      |

**ExtrapolationMode with InterpolationMode = Discrete**

| ExtrapolationMode   | Enumeration value   | Index before data   | Index after data    |
|---------------------|---------------------|---------------------|---------------------|
| All                 | 0                   | No event is returned| No event is returned|
| None                | 1                   | No event is returned| No event is returned|
| Forward             | 2                   | No event is returned| No event is returned|
| Backward            | 3                   | No event is returned| No event is returned|

**ExtrapolationMode with InterpolationMode = ContinuousNullableLeading and ContinuousNullableTrailing**

| ExtrapolationMode   | Enumeration value   | Index before data          | Index after data          |
|---------------------|---------------------|----------------------------|---------------------------|
| All                 | 0                   | Returns the default value         | Returns the default value   |
| None                | 1                   | No event is returned       | No event is returned      |
| Forward             | 2                   | No event is returned       | Returns the default value value   |
| Backward            | 3                   | Returns the default value         | No event is returned      |

For additional information about the effect of read characteristics, see the
documentation on the [read method](xref:sdsReadingDataApi)
you are using.

