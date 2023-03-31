![[file_management_1.png]]

## Disk Partition
- Boot block - Stores the bootstrap program to load
- Superblock - Keep the metadata of a file system (number of blocks, block size, the location of index nodes)
![[disk_partition_1.png]]
### Directory Tree
In modern OSs, we keep he idea of the tree but are actually stored as graphs
![[directory_tree_1.png]]

## Files
Composed of File Data and Metadata

### File Data
One or more blocks (e.g. sector, page) of data

### Metadata
- Name, size
- Which directory it is located in
- Creation/modified/access time
- Hidden or system file
- Owner and owner's group
- Permissions: read/write/execute
- Unique identifier (file name may not be unique)
- Structure that maps a file to blocks on the secondary storage

### Mapping file to blocks
![[file_to_block_mapping.png]]
One of the key jobs of file system
- Directory is also a file
- Directory is stored a a special type of file
	- Contains a list of entries inside the directory, plus some metadata for each entry
	- ![[directory_1.png]]
	- ![[directory_2.png]]
