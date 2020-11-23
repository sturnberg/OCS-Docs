# Transforming Data

SDS provides the ability to transform data upon reads. 
The supported data transformations are:
* [Reading with SdsStreamViews](#reading-with-sdsstreamviews): changing the shape of the returned data
* [Unit of Measure Conversions](#unit-conversion-of-data): converting the unit of measure of the data  
Data transformations are supported for all single stream reads,
but transformations have specific endpoints. 

### Reading with SdsStreamViews
When transforming data with an SdsStreamView,
the data read is converted to the *target type*
 specified in the SdsStreamView. 
Working with stream views is covered in detail in the [Stream Views](xref:sdsStreamViews) section.

When data is requested with an SdsStreamView, 
the read characteristics defined by the *target type* 
of the SdsStreamView determine what is returned. 
The read characteristics are discussed in the code samples.

### Unit conversion of data
SDS supports assigning [Units of Measure](xref:unitsOfMeasure) (UOM) to stream data. 
If stream data has UOM information associated, SDS supports reading data with unit conversions applied.
On each read data request, unit conversions are specified by a user defined collection of 
`SdsStreamPropertyOverride` objects in read requests.
The `SdsStreamPropertyOverride` object has the following structure:

| Property          | Type                 | Optionality | Details                                               |
| ----------------- | -------------------- | ----------- | ----------------------------------------------------  |
| SdsTypePropertyId | String               | Required    | Identifier for an SdsTypeProperty with a UOM assigned |
| Uom               | String               | Required    | Target unit of measure                                |
| InterpolationMode | SdsInterpolationMode | N/A         | Currently not supported in context of data reads      |

This is supported in the .NET client libraries methods via overloads that accept a collection of `SdsStreamPropertyOverride` objects, and in the REST API via HTTP POST calls with a request body containing a collection of `SdsStreamPropertyOverride` objects.  
All unit conversions are HTTP POST requests.
All single stream data reads with streams that have
specified UOMs support UOM conversions.

***********************
