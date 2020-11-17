# SdsBoundaryType

The `SdsBoundaryType` enum defines how data on the boundary of queries is handled: around the start index for range value queries, 
and around the start and end index for window values. The following are valid values for `SdsBoundaryType`:

| Boundary | Enumeration value | Operation |
| -------  | ----------------- | --------- |
| Exact    | 0                 | Results include the event at the specified index boundary if a stored event exists at that index. |
| Inside   | 1                 | Results include only events within the index boundaries |
| Outside  | 2                 | Results include up to one event that falls immediately outside of the specified index boundary. |
| ExactOrCalculated | 3        | Results include the event at the specified index boundary. If no stored event exists at that index, one is calculated based on the index type and interpolation and extrapolation settings. |
