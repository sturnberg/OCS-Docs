# Create stream views

To work with stream views, you first need to have types, streams and streams data defined. 
Here's a simplified procedure for working with the stream view. 
For code examples, see [Work with SdsStreamViews in .NET framework](#work-with-sdsstreamviews-in-net-framework)
 and [Work with SdsStreamViews outside of .NET framework](#work-with-sdsstreamviews-outside-of-net-framework) below. 

1. Create a type that will be the source type. 
2. Create a stream that is of the type defined in step 1.
3. Write data into the stream that was created in step 2.
4. Read data from the stream to verify.
5. Create another type that will be the target type.
6. Create a stream view using the source type (step 1) and the target type (step 5).  
    - The mapping between the source and the target type happens automatically if you do not specify it in [SdsStreamViewProperty](#sdsstreamviewproperty).
7. Get [SdsStreamViewMap](#get-stream-view-map) to see how properties are mapped.
8. Read data from the stream with the stream view to verify. For more information, see [Reading with SdsStreamViews](xref:sdsReadingData#reading-with-sdsstreamviews).