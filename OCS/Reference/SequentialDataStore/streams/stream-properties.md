# Streams fields and properties table 
The following table shows the required and optional SdsStream fields. Fields not listed are reserved
for internal SDS use.

<a name="streampropertiestable"></a>
| Property          | Type                             | Optionality | Searchable | Details |
|-------------------|----------------------------------|-------------|------------|---------|
| Id                | String                           | Required    | Yes		  | An identifier for referencing the stream |
| TypeId            | String                           | Required    | Yes		  | The SdsType identifier of the type to be used for this stream |
| Name              | String                           | Optional    | Yes		  | Friendly name |
| Description       | String                           | Optional    | Yes		  | Description text |
| Indexes           | IList\<SdsStreamIndex\>            | Optional    | No		  | Used to define secondary indexes for stream |
| InterpolationMode | SdsInterpolationMode             | Optional    | No		  | Interpolation setting of the stream. Default is null. |
| ExtrapolationMode | SdsExtrapolationMode             | Optional    | No		  | Extrapolation setting of the stream. Default is null. |
| PropertyOverrides | IList\<SdsStreamPropertyOverride\> | Optional    | No		  | Used to define unit of measure and interpolation mode overrides for a stream. |
| [Tags](xref:sdsStreamExtra)*		| IList\<String\>					| Optional    | Yes		  | A list of tags denoting special attributes or categories.|
| [Metadata](xref:sdsStreamExtra)*	| IDictionary\<String, String\>	| Optional    | Yes		  | A dictionary of string keys and associated string values.  |

**\* Notes on SdsStream metadata and tags:** Stream metadata and tags are accessed via the Metadata and Tags API respectively.
However, they are associated with SdsStream objects and can be used as search criteria.

**Rules for the Stream Identifier (SdsStream.Id)**
1. Is not case sensitive
2. Cannot just be whitespace
3. Cannot contain leading or trailing whitespace
4. Cannot contain forward slash ("/")
5. Can contain a maximum of 100 characters