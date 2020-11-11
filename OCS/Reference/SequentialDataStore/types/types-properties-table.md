# SdsType fields and properties table
<a name="typepropertiestable"></a>
The table below lists required and optional fields in an SdsType. Fields that are not included are reserved for internal SDS use.
For more information on search including limitations, see [Search in SDS](xref:sdsSearching).
| Property          | Type                   | Optionality | Searchable | Details |
|-------------------|------------------------|-------------|---------|---------|
| Id                | String                 | Required    | Yes | Identifier for referencing the type |
| Name              | String                 | Optional    | Yes | Friendly name |
| Description       | String                 | Optional    | Yes | Description text |
| SdsTypeCode       | SdsTypeCode            | Required    | No | Numeric code identifying the base SdsType |
| InterpolationMode | SdsInterpolationMode   | Optional    | No | Interpolation setting of the type. Default is Continuous. For more information, see [Interpolation](xref:sdsReadingData#interpolation).|
| ExtrapolationMode | SdsExtrapolationMode   | Optional    | No | Extrapolation setting of the type. For more information, see [Extrapolation](xref:sdsReadingData#extrapolation). |
| Properties        | IList\<SdsTypeProperty\> | Required    | Yes, with limitations | List of SdsTypeProperty items. See [SdsTypeProperty](#sdstypeproperty) below.  |

### Rules for the SdsType Identifier (SdsType.Id)
1. Is not case sensitive
2. Cannot just be whitespace
3. Cannot contain leading or trailing whitespace
4. Cannot contain forward slash ("/")
5. Can contain a maximum of 100 characters  

Type management using the .NET SDS client libraries methods is performed through ``ISdsMetadataService``. 
You can create ``ISdsMetadataService`` using one of the ``SdsService.GetMetadataService()`` factory methods.
.NET client libraries provide `SdsTypeBuilder` to help build SdsTypes from .NET types. SdsTypeBuilder is discussed in greater detail below.
