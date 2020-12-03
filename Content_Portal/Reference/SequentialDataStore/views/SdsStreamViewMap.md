## SdsStreamViewMap
When an SdsStreamView is added, SDS defines a plan mapping. Plan details are retrieved as an SdsStreamViewMap. 
The SdsStreamViewMap provides a detailed property-by-property definition of the mapping. 

The table below shows the SdsStreamViewMap fields. The SdsStreamViewMap cannot be written to SDS, 
so required and optional have no meaning.

| Property     | Type                     | Optionality  | Details |
|--------------|--------------------------|--------------|---------|
| SourceTypeId | String                   | Required     | Identifier of the SdsType of the SdsStream |
| TargetTypeId | String                   | Required     | Identifier of the SdsType to convert events to |
| Properties   | IList\<SdsStreamViewMapProperty\>| Optional     | Property-level mapping |

### SdsStreamViewMapProperty
The SdsStreamViewMapProperty is similar to SdsStreamViewProperty but adds a `mode` detailing one or more actions taken on 
the property.

The table below shows the SdsStreamViewMapProperty fields. The SdsStreamViewMap cannot be written; it can only be 
retrieved from SDS, so required and optional have no meaning.

| Property     | Type        | Details |
|--------------|-------------|---------|
| SourceTypeId | String      | Identifier of the SdsType of the SdsStream |
| TargetTypeId | String      | Identifier of the SdsType to convert events to |
| Mode         | SdsStreamViewMode | Aggregate of actions applied to the properties. SdsStreamViewModes are combined via binary arithmetic |
| SdsStreamViewMap   | SdsStreamViewMap  | Mapping for derived types |

**SdsStreamViewModes**
| Name                   | Value  | Description |
|------------------------|--------|-------------|
| None                   | 0x0000 | No action   |
| FieldAdd               | 0x0001 | Add a property matching the specified SdsTypeProperty |
| FieldRemove            | 0x0002 | Remove the property matching the specified SdsTypeProperty |
| FieldRename            | 0x0004 | Rename the property matching the source SdsTypeProperty to the target SdsTypeProperty |
| FieldMove              | 0x0008 | Move the property from the location in the source to the location in the target|
| FieldConversion        | 0x0016 | Convert the source property to the target type |
| InvalidFieldConversion | 0x0032 | Cannot perform the specified mapping |
