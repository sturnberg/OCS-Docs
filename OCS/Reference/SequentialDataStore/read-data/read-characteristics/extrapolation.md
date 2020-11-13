
# Extrapolation

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

