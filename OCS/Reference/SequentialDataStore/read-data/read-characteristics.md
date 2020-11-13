# Read Characteristics

When data is requested at an index for which no stored event exists, the read characteristics determine 
whether the result is an error, no event, interpolated event, or extrapolated event. The combination of 
the type of the index and the interpolation and extrapolation modes of the SdsType and the SdsStream 
determine the read characteristics.

**\*Notes:** Use the ISO 8601 representation of dates and times in SDS, `2020-02-20T08:30:00-08:00` for February 20, 2020 at 8:30 AM PST, for example.
SDS returns timestamps in UTC if the timestamp is of property `DateTime` and in local time if it is of `DateTimeOffset`. 
