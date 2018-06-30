# unixfs-v2 DRAFT implementation

Usage:

```javascript
const unixfs = require('unixfsv2')
const blockstore = require('some-block-store')

const getDirectory = async path => {
  let last
  for await (let block of unixfs(__dirname)) {
    await blockstore.put(block)
  }
  return last.cid.toBaseEncodedString()
}
```

## API

### unixfs.dir(path[, recursive=true][, chunkSize=1meg])

Returns an async generator that yields `Block` instances.

The last block instance returned is the `dag-cbor` block for
the root node.

### unixfs.dir(path[, chunkSize=1meg])

Returns an async generator that yields `Block` instances.

The last block instance returned is the `dag-cbor` block for
the root node.