# Read a Tree Object

Trees are used to store directory structures. It solves the problem of storing the filename and also allows you to store a group of files together.

A tree object has multiple "entries". Each entry includes:

* A SHA hash that points to a blob or tree object
  * If the entry is a file, this points to a blob object
  * If the entry is a directory, this points to a tree object
* The name of the file/directory
*   The mode of the file/directory

    * This is a simplified version of the permissions you'd see in a Unix file system.
    * For files, the valid values are:
      * `100644` (regular file)
      * `100755` (executable file)
      * `120000` (symbolic link)
    * For directories, the value is `040000`



For example, if you had a directory structure like this:

```
  your_repo/
    - file1
    - dir1/
      - file_in_dir_1
      - file_in_dir_2
    - dir2/
      - file_in_dir_3
```

The entries in the tree object would look like this:

```
  040000 dir1 <tree_sha_1>
  040000 dir2 <tree_sha_2>
  100644 file1 <blob_sha_1>
```

The `git ls-tree` command is used to inspect a tree object.

For a directory structure like this:

```
  your_repo/
    - file1
    - dir1/
      - file_in_dir_1
      - file_in_dir_2
    - dir2/
      - file_in_dir_3
```

The output of `git ls-tree` would look like this:

```bash
  $ git ls-tree <tree_sha>
  040000 tree <tree_sha_1>    dir1
  040000 tree <tree_sha_2>    dir2
  100644 blob <blob_sha_1>    file1
```

Note that the output is alphabetically sorted, this is how Git stores entries in the tree object internally.

```bash
 $ git ls-tree --name-only <tree_sha>
  dir1
  dir2
  file1
```
