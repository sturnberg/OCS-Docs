# SdsSearchMode

The `SdsSearchMode` enum defines search behavior when seeking a stored event near a specified index. The following are valid values for `SdsSearchMode`:

| Mode  | Enumeration value | Operation |
| ----- | ----------------- | --------- |
| Exact | 0                 | If a stored event exists at the specified index, that event is returned. Otherwise no event is returned. |
| ExactOrNext | 1           | If a stored event exists at the specified index, that event is returned. Otherwise the next event in the stream is returned. |
| Next | 2                  | Returns the stored event after the specified index. |
| ExactOrPrevious | 3       | If a stored event exists at the specified index, that event is returned. Otherwise the previous event in the stream is returned. |
| Previous | 4              | Returns the stored event before the specified index. |
