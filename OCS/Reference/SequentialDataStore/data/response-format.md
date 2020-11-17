### Response Format

Supported response formats include JSON, verbose JSON, and SDS. 

The default response format for SDS is JSON, which is used in all examples in this document. Default JSON responses do not include any values that are equal to the default value for their type.

Verbose JSON responses include all values, including defaults, in the returned JSON payload. To specify verbose JSON return, add the header ``Accept-Verbosity`` with a value of ``verbose`` to the request.  

To specify SDS format, set the ``Accept`` header in the request to ``application/sds``.
