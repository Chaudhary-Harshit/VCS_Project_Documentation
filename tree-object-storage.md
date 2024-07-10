# Tree Object Storage

Just like blobs, tree objects are stored in the `.git/objects` directory. If the hash of a tree object is `e88f7a929cd70b0274c4ea33b209c97fa845fdbc`, the path to the object would be `./git/objects/e8/8f7a929cd70b0274c4ea33b209c97fa845fdbc`.



The format of a tree object file looks like this (after Zlib decompression):

```
  tree <size>\0
  <mode> <name>\0<20_byte_sha>
  <mode> <name>\0<20_byte_sha>
```

* The file starts with `tree <size>\0`. This is the "object header", similar to what we saw with blob objects.
* After the header, there are multiple entries. Each entry is of the form `<mode> <name>\0<sha>`.
  * `<mode>` is the mode of the file/directory (check the previous section for valid values)
  * `<name>` is the name of the file/directory
  * `\0` is a null byte
  * `<20_byte_sha>` is the 20-byte SHA-1 hash of the blob/tree (this is **not** in hexadecimal format)

In a tree object file, the SHA hashes are not in hexadecimal format. They're just raw bytes (20 bytes long).
