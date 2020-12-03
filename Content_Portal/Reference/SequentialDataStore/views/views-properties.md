# SdsStreamView fields and properties table
<a name="streamviewpropertiestable"></a>
The following table shows the required and optional SdsStreamView fields. Fields that are not included are reserved for internal SDS use. 
See [Search in SDS](xref:sdsSearching#search-for-stream-views) for limitations on search.
| Property     | Type                   | Optionality | Searchable | Details |
|--------------|------------------------|-------------|------------|---------|
| Id           | String                 | Required    | Yes		   |Identifier for referencing the stream view |
| Name         | String                 | Optional    | Yes		   |Friendly name |
| Description  | String                 | Optional    | Yes		   |Description text |
| SourceTypeId | String                 | Required    | Yes		   |Identifier of the SdsType of the SdsStream |
| TargetTypeId | String                 | Required    | Yes		   |Identifier of the SdsType to convert events to |
| Properties   | IList\<SdsStreamViewProperty\> | Optional    | Yes, with limitations*	  |Property level mapping |
**\*Notes on `Properties` field**: SdsStreamViewProperty objects are not searchable.
Only the SdsStreamViewProperty's SdsStreamView is searchable by its `Id`, `SourceTypeId`, and `TargetTypeId`, which are used to return the top level SdsStreamView object when searching.
The same is true for nested SdsStreamViewProperties. For more information, see [search for stream views](xref:sdsSearching#search-for-stream-views).

**Rules for the Stream View Identifier (SdsStreamView.Id)**

1. Is not case sensitive
2. Cannot just be whitespace
3. Cannot contain leading or trailing whitespace
4. Cannot contain forward slash ("/")
5. Can contain a maximum of 100 characters


### Stream views mapping

SDS automatically maps properties from the source to the target type when it is straightforward:
 - The properties are in the same position
 - The properties are of the same data type
 - The properties are of the same name

See [Work with StreamViews in .NET framework](#work-with-sdsstreamviews-in-net-framework) below for how automatic mapping works.  

If needed, you can specify mapping. SDS largely supports mapping within the same data type. 

**Mapping compatibility chart**
 
| Source type\ Target type    | Numeric types 	| Nullable numeric types 	| Enumeration types 	| Nullable enumeration types 	| Object types    	| 
|----------------------------	|---------------	|------------------------	|-------------------	|----------------------------	|--------------------|
| Numeric types              	| Yes           	| Yes                    	| No                	| No                         	| No                 |
| Nullable numeric types     	| Yes           	| Yes                    	| No                	| No                         	| No                 |
| Enumeration types          	| No            	| No                     	| Yes               	| Yes                        	| No                 |
| Nullable enumeration types 	| No            	| No                     	| Yes               	| Yes                        	| No                 | 
| Object types               	| No            	| No                     	| No                	| No                         	| Yes*               |

\*: Mappable if `typeId` matches between the source and the target type 

## SdsStreamViewProperty
The SdsStreamView Properties collection provides detailed instructions for specifying the mapping of 
event properties. Each SdsStreamViewProperty in the Properties collection defines the mapping of an 
event�s `property`. SdsStreamView Properties are required only when property mapping is not straightforward. 
Additionally, if you do not want a SdsType property mapped, it is not necessary to create an SdsStreamView 
property for it.

The following table shows the required and optional SdsStreamViewProperty fields.

| Property | Type    | Optionality | Details |
|----------|---------|-------------|---------|
| SourceId | String  | Required    | Identifier of the SdsTypeProperty from the source SdsType Properties list |
| TargetId | String  | Required    | Identifier of the SdsTypeProperty from the target SdsType Properties list |
| SdsStreamView  | SdsStreamView | Optional    | Additional mapping instructions for derived types |

The SdsStreamView field supports nested properties.

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
