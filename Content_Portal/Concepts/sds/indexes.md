---
uid: sdsIndexes
---

# Indexes
Indexes speed up and order the results of searches. A key uniquely identifies a record within 
a collection of records. Keys are unique within the collection.

In SDS, the key of an SdsType is also an index. The key is often referred to as the *primary index,* 
while all other indexes are referred to as *secondary indexes* or *secondaries*.

An SdsType that is used to define an SdsStream must specify a key. When inserting data into an SdsStream, every 
key value must be unique. SDS will not store more than a single event for a given key; an event with 
a particular key may be deleted or updated, but two events with the same key cannot exist.

In .NET, the SdsType properties that define the primary index are identified using an ``OSIsoft.Sds.SdsMemberAttribute`` 
and setting its ``IsKey`` field to true. If the key consists of only a single property it is permissible to 
use the ``System.ComponentModel.DataAnnotations.KeyAttribute``. In the SdsType, the Property or Properties 
representing the primary index have their ``SdsTypeProperty.IsKey`` field set to true.

Secondary indexes are defined on SdsStreams and are applied to a single property. You can define several 
secondary indexes. Secondary index values need not be unique.

## Compound indexes
A single property (such as a `DateTime`) is adequate for defining an index most of the time. 
But for more complex scenarios, SDS allows you to define multiple properties. 
Indexes defined by multiple properties are known as *compound indexes*.
Only the primary index (or key) supports compound indexes.

When defining a compound index within .NET framework, you should apply the ``OSIsoft.Sds.SdsMemberAttribute`` 
on each property field of the SdsType that is combined to define the index.
Set the Property ``IsKey`` to ``true`` and give the ``Order`` field a zero-based index value.
The ``Order`` field defines the precedence of the Property when sorting.
A Property with an order of 0 has highest precedence.

When defining compound indexes outside of .NET framework, specify the ``IsKey`` and ``Order`` fields
on the ``SdsTypeProperty`` object.

You can specify a maximum of three properties to define a compound index.
In read and write operations, specify compound indexes in the URI by ordering each property that composes the index
 separated by the pipe character, ‘|’. 
To help those using compound indexes, .NET client libraries methods also allow the use of tuples for indexes.

**Notes:** 
- Compound indexing only applies to SdsTypes. In other words, there is no compound indexing for secondary indexes that are on SdsStreams. For more information, see [SdsStreams](xref:sdsStreams#indexes).  
- The examples below are for compound indexes on SdsTypes and not of secondary indexes on SdsStreams.


**REST API**
```text
// Read data located between two compound indexes:
GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data?startIndex={firstIndex|secondIndex|thirdIndex}&endIndex={firstIndex|secondIndex|thirdIndex}
GET api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data?startIndex={firstIndex|secondIndex}&endIndex={firstIndex|secondIndex}

// Delete data with a compound index:
DELETE api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data?index={firstIndex|secondIndex}
DELETE api/v1/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data?startIndex={firstIndex|secondIndex|thirdIndex}&endIndex={firstIndex|secondIndex|thirdIndex}
```
**.NET examples**
```csharp
// Read data located between two compound indexes:
IEnumerable<DerivedCompoundIndex> compoundValues = await client.GetWindowValuesAsync<DerivedCompoundIndex>(compoundStream.Id, 1/20/2017 01:00|1/20/2017 00:00, 1/20/2017 02:00|1/20/2017 14:00);

// Remove data with a compound index:
Task RemoveValueAsync(compoundStream.Id, 1/20/2017 01:00|1/20/2017 00:00);
```

