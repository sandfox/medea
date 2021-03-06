# medea

A lightweight key-value storage library.

* Can be embedded in Node.js applications.
* Support for basic get, put, and remove operations.
* Heavily inspired by Basho's [Bitcask](https://github.com/basho/bitcask) key-value database.
* Values can be any string or `Buffer`.

## Example

```javascript
var Medea = require('medea');

var medea = new Medea();

medea.open(function(err) {
  medea.put('hello', 'world!', function(err) {
    medea.get('hello', function(err, val) {
      console.log(val.toString());
      medea.close();
    });
  });
});
```

## Install

```bash
$ npm install medea
```

## Usage

### medea.open([directory], callback)

Opens a Medea database.

`directory`: Optional. Defaults to `medea` in the current directory.

`callback`: Takes one error parameter.

### medea.get(key, callback)

Returns the value associated with the given key.

`key`: identifier to retrieve the value

`callback`: has the signature `function (err, value)` where `value` is the returned value.

### medea.put(key, value, callback) 

Stores a value in the database.

`key`: identifier

`value`: value associated with the key

`callback`: function that takes an error parameter

### medea.remove(key, callback)

Removes an entry from the database.

`key`: identifier for the item to remove

`callback`: Takes one error parameter.

### medea.sync(callback)

Performs an fsync operation on the data file.

### medea.close(callback)

Closes the database.

### medea.listKeys()

Returns an array of all the keys in the database.

### medea.mapReduce(options, callback)

Experimental.

Ad-hoc map-reduce queries over the database.  The query results are not indexed.  A more robust map-reduce implementation will be provided in the near future.

See `examples/map_reduce.js` for an example.

## Limitations

Currently, multiple processes cannot access the same data directory.  Run one process per directory.

Repeated use leads to fragmentation and empty files. A merge process needs to be run for cleanup, but that piece has yet to be developed.

This software is still in an early, experimental phase.  Feedback, issues, and pull requests are welcome. :)

## License

MIT

Copyright 2013 Apigee Corporation and Contributors
