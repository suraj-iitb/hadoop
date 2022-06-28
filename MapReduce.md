# MapReduce

**Major Operations**:
1. Map
2. Reduce

## Working of MapReduce
1. Read file (any type) stored on HDFS
  - InputFormat: Type of file to deal with. Eg: `TextInputFormat` (default), `FileInputFormat`, etc.
  - RecordReader: Read records from input splits on HDFS. It has delimiters like \n (default) or \t.
2. Mapper Operation (1 mapper per input split)
  - Process each record in the input split via `map()` method of `Mapper` class
  - Emit output using `Context` object
3. Partition Operation
  - Assign partition number to the record emitted by the mapper (so that record with same keys always go to the same reducer)
  - Partition index/number is calculated during `context.write()`
4. Combiner Operation (1 combiner per mapper)
  - Combines the values based on the key
  - May not be executed if no duplicate keys
6. Shuffling & Sorting
  - Shuffling means transferring data from mapper to reducer (Reducer launches threads to read data from mapper)
  - Sorting sorts the key before reading
7. Reducer Operation (No of reducers can be configured)
  - Process each unique key via `reducer()` method of `Reducer` class
8. Output the file on HDFS
  - OutputFormat: Type of output file to deal with. Eg: `TextOutputFormat` (default), `FileOutputFormat`, etc.
  - RecordWriter: Write records on HDFS. It has delimiters like \n (default for record) or \t (default for key/value pair).
