# Interpolation

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
