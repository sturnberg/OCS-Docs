# SdsTypeProperty
The Properties collection defines the fields in an SdsType. 

The following table shows the required and optional SdsTypeProperty fields. Fields that 
are not included are reserved for internal SDS use.

|          Property         | Type                    | Optionality | Details |
|---------------------------|-------------------------|-------------|---------|
| Id                        | String                  | Required    | Identifier for referencing the type |
| Name                      | String                  | Optional    | Friendly name |
| Description               | String                  | Optional    | Description text |
| SdsType                   | SdsType                 | Required    | Field defining the property's SdsType |
| IsKey                     | Boolean                 | Required    | Identifies the property as the index |
| Value                     | Object                  | Optional    | Value of the property |
| Order                     | Int                     | Optional    | Order of comparison within a compound index |
| InterpolationMode         | SdsInterpolationMode    | Optional    | Interpolation setting of the property. Default is null. |
| Uom                       | String                  | Optional    | Unit of measure of the property |

The SdsTypeProperty's identifier follows the same [rules](#typepropertiestable) as the SdsType's identifier.

Boolean value ``IsKey`` identifies the primary index of an SdsType in a single index. An index that is defined by more than one 
SdsTypeProperty is called a compound index. The maximum number of properties that can define a compound index is three. 
In a compound index, each SdsTypeProperty that is included in the index is specified as ``IsKey``.
The ``Order`` field marks the order of comparison within a compound index.

The ``Value`` field is used for properties that represent a value. An example of a property with a 
value is an enum's named constant. When representing an enum in an SdsType, the SdsType's 
SdsTypeProperty collection defines the enum's constant list. The SdsTypeProperty's ``Id`` represents 
the constant's name and the SdsTypeProperty's ``Value`` represents the constant's value (see the enum ``State`` definitions in the code samples below).

``InterpolationMode`` is assigned when the SdsTypeProperty of the event should be interpolated in a specific way 
that differs from the interpolation mode of the SdsType. ``InterpolationMode`` is only applied to an SdsTypeProperty 
that is not part of the index. If the ``InterpolationMode`` is not set, the SdsTypeProperty is interpolated 
in the manner defined by the SdsType's ``InterpolationMode``.

An SdsType with the ``InterpolationMode`` set to `Discrete` cannot also have the SdsTypeProperty with ``InteroplationMode``. 
For more information on interpolation of events, see [Interpolation](xref:sdsReadingData#interpolation).

``Uom`` is the unit of measure for the SdsTypeProperty. The ``Uom`` of the SdsTypeProperty may be specified by the name or the 
abbreviation. The names and abbreviations of ``Uoms`` are case sensitive. 

The ``InterpolationMode`` and ``Uom`` of the SdsTypeProperty can be overridden on the SdsStream. For more information, see [Streams](xref:sdsStreams#sdsstreampropertyoverride).
