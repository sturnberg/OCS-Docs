# Units definition

A SdsUom represents a single unit of measure, such as 'meter'.

The following table shows the required and optional SdsUom fields.

| Property         | Type   | Optionality | Details | Example  |
| ---------------- | ------ | ----------- | ------- | -------- |
| Id               | String | Required    | Unique identifier for the unit of measure | meters per second |
| Abbreviation     | String | Optional    | Abbreviation for the unit of measure  | m/s |
| Name             | String | Optional    | Full name for the unit of measure | Meters per second |
| DisplayName      | String | Optional    | Friendly display name for the unit of measure | meters per second |
| QuantityId       | String | Required    | The identifier associated with the quantity that this unit is a measure of | Velocity|
| ConversionFactor | Double | Required    | Used for unit conversions.  When a value of this unit is multiplied by the ConversionFactor and then incremented by the ConversionOffset, the value in terms of the base unit of the corresponding quantity is returned. | 1.0 |
| ConversionOffset | Double | Required    | Used for unit conversions. See details for ConversionFactor | 0.0  |