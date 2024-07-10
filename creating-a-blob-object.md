# Creating a Blob Object

Here we would be calculating the SHA hash of the file and writing to to objects after compressing it. In the git `git hash-object` is used to compute the SHA hash of a Git object. When used with the `-w` flag, it also writes the object to the `.git/objects` directory.

Here's an example of using `git hash-object`:

```bash
# Create a file with some content
  $ echo "hello world" > test.txt

  # Compute the SHA hash of the file + write it to .git/objects
  $ git hash-object -w test.txt
  3b18e512dba79e4c8300dd08aeb37f8e728b8dad

  # Verify that the file was written to .git/objects
  $ file .git/objects/3b/18e512dba79e4c8300dd08aeb37f8e728b8dad
  .git/objects/3b/18e512dba79e4c8300dd08aeb37f8e728b8dad: zlib compressed data
```

&#x20;Each Git Blob is stored as a separate file in the `.git/objects` directory. The file contains a header and the contents of the blob object, compressed using Zlib.

The format of a blob object file looks like this (after Zlib decompression):

```
  blob <size>\0<content>
```

* `<size>` is the size of the content (in bytes)
* `\0` is a null byte
*   `<content>` is the actual content of the file

    For example, if the contents of a file are `hello world`, the blob object file would look like this (after Zlib decompression):

```
  blob 11\0hello world
```

* Although the object file is stored with zlib compression, the SHA hash needs to be computed over the "uncompressed" contents of the file, not the compressed version.
* The input for the SHA hash is the header (`blob <size>\0`) + the actual contents of the file, not just the contents of the file.
