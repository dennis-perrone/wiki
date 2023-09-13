# Linux Archive Management (tar)

## Definition

- Archive files are used to create manageable personal backups, or to simplify the task of transferring a set of files across a network when other methods, such as `rsync`, are unavailable or might be more complex. Archive files can be created with or without using compression to make the archive file smaller.  

## Command Options  
- One of the following `tar` command actions is required to perform a `tar` operation:  
	- `-c` **or** `--create`: Create an archive file.  
	- `-t` **or** `--list`: List the contents of an archive.  
	- `-x` **or** `--extract`: Extract an archive.  
-  
- The following `tar` command general options are commonly included:  
	- `-v` **or**` --verbose`: Show the files being archived or extracted during the `tar` operation.  
	- `-f` **or** `--file`: Follow this option with the archive file name to create or open.  
	- `-p`** or** `--preserve-permissions`: Preserve the original file permissions when extracting.  
	- `--xattrs`: Enable extended attribute support, and store extended file attributes.  
	- `--selinux`: Enable SELinux context support, and store SELinux file contexts.

- The following `tar` command compression options are used to select an algorithm:  
	- `-a` **or **`--auto-compress`: Use the archive's suffix to determine the algorithm to use.  
	- `-z` **or**`--gzip`: Use the `gzip` compression algorithm, resulting in a `.tar.gz` suffix.  
	- `-j` **or** `--bzip2`: Use the `bzip2` compression algorithm, resulting in a `.tar.bz2` suffix.  
	- `-J` **or** `--xz`: Use the `xz` compression algorithm, resulting in a `.tar.xz` suffix.  
	- `-Z` **or** `--compress`: Uses an `LZ`-variant algorithm, resulting in a `.tar.Z` suffix.  

## Usage

- To create an archive:  
	- `tar -czf backup_name.tar.gz file01.txt file02.txt file03.txt`  
- To list the contents of an archive:  
	- `tar -tf /path/to/backup.tar.gz`  
