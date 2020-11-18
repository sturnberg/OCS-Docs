# Read data

The .NET and REST APIs provide programmatic access to read and write data. This section identifies and describes 
the APIs used to read [SdsStreams](xref:sdsStreams) data. Results are influenced by [SdsTypes](xref:sdsTypes), [SdsStreamViews](xref:sdsStreamViews), [filter expressions](xref:sdsFilterExpressions), and [table format](xref:sdsTableFormat).

If you are working in a .NET environment, convenient SDS Client Libraries are available. 
The `ISdsDataService` interface, which is accessed using the ``SdsService.GetDataService()`` helper, 
defines the functions that are available.

### Response Format

Supported response formats include JSON, verbose JSON, and SDS. 

The default response format for SDS is JSON, which is used in all examples in this document. Default JSON responses do not include any values that are equal to the default value for their type.

Verbose JSON responses include all values, including defaults, in the returned JSON payload. To specify verbose JSON return, add the header ``Accept-Verbosity`` with a value of ``verbose`` to the request.  

To specify SDS format, set the ``Accept`` header in the request to ``application/sds``.

### Indexes and reading data

Most read operations take at least one index as a parameter. Indexes may be specified as strings, or 
using the SDS Client libraries, the index may be passed as-is to read methods that take the index 
type as a generic argument. For more information, see [Indexes](xref:sdsIndexes). For information on compound indexes, see [Compound indexes](xref:sdsIndexes#compound-indexes).

### Filter Expressions

Filter expressions can be applied to any read that returns multiple values, including Get Values, Get Range Values, 
Get Window Values, and Get Intervals. The filter expression is applied to the collection events conditionally 
filtering events that do not meet the filter conditions.

Filter expressions are covered in detail in the [Filter expressions](xref:sdsFilterExpressions) section.

### Table Format

Results of a query can be organized into tables by directing the form parameter to return a table. 
Two forms of table are available: table and header table.

When the form parameter is specified as table, ``?form=table``, events are returned in row column form. 
Results include a collection named ``Columns`` that lists column name and type and a collection named 
``Rows`` containing a collection of rows matching the order of the columns.

Specifying a form of type ``table-headers``, ``?form=tableh``, results in a collection where the Rows collection 
contains a column header list.

Table formats are covered in detail in the [Table format](xref:sdsTableFormat) section.