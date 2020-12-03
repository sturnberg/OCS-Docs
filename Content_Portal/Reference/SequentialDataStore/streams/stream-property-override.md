# SdsStreamPropertyOverride
``SdsStreamPropertyOverride`` object provides a way to override interpolation behavior and unit of measure for individual 
SdsType Properties for a specific SdsStream.

The ``SdsStreamPropertyOverride`` object has the following structure:

| Property          | Type                 | Optionality | Details |
|-------------------|----------------------|-------------|---------|
| SdsTypePropertyId | String               | Required    | SdsTypeProperty identifier |
| InterpolationMode | SdsInterpolationMode | Optional    | Interpolation setting. Default is null |
| Uom               | String               | Optional    | Unit of measure |


The unit of measure can be overridden for any SdsTypeProperty defined by the stream type, including primary 
and secondary indexes. For more information on SdsTypeProperty `Uom`, see [Types](xref:sdsTypes#sdstypeproperty). 

Read characteristics of the SdsStream are determined by the SdsType and the `PropertyOverride` of the SdsStream. The 
interpolation mode for non-index properties can be defined and overridden at the SdsStream level. For more 
information about type read characteristics see [Types](xref:sdsTypes#sdstypeproperty).

If `InterpolationMode` of the SdsType is set to ``Discrete``, it cannot be overridden 
at any level. When `InterpolationMode` is set to ``Discrete`` and an event is not defined for the index,
a null value is returned for the entire event.