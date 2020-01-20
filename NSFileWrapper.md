# NSFileWrapper

## Discussion

The NSFileWrapper class provides access to the attributes and contents of file system nodes. A file system node is a file, directory, or symbolic link. Instances of this class are known as file wrappers.



## Note

Starting in macOS **10.7**, NSFileWrapper moved from Application Kit to Foundation. As a result of this the `icon`, and `setIcon:` methods have moved to a new category of NSFileWrapper that remains in Application Kit.
File wrappers represent a file system node as an object that can be displayed as an image (and possibly edited in place), saved to the file system, or transmitted to another application.
There are three types of file wrappers:

- **Regular-file** file wrapper: Represents a regular file.
- **Directory** file wrapper: Represents a directory.
- **Symbolic-link** file wrapper: Represents a symbolic link.


A file wrapper has these attributes:

- **Filename**. Name of the file system node the file wrapper represents.
- **file-system attributes**. See NSFileManager for information on the contents of the attributes dictionary.
- **Regular-file contents**. Applicable only to regular-file file wrappers.
- **File wrappers**. Applicable only to directory file wrappers.
- **Destination node**. Applicable only to symbolic-link file wrappers.