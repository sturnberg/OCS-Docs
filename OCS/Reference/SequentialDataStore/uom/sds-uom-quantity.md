## SdsUomQuantity

A SdsUomQuantity represents a single measurable quantity (for example, length).

The following table shows the required and optional SdsUomQuantity fields.

| Property   | Type    | Optionality | Details | Example  |
| ---------- | ------- | ----------- | ------- | ---------|
| Id         | String  | Required    | Unique identifier for the quantity | Velocity |
| Name       | String  | Optional    | Full name for the quantity | Velocity |
| BaseUom    | SdsUom  | Required    | The base unit of measure for this quantity. All other Uom's measuring this quantity will have ConversionFactor's and ConversionOffsets relative to the BaseUom  | SdsUom representing "meters per second" |
| Dimensions | short[] | Optional    | Reserved for internal use. Represents the seven base SI dimensions: Length, Mass, Time, Electric Current, Thermodynamic Temperature, Amount of Substance, and Luminous Density. | [1,0,-1,0,0,0,0] |
