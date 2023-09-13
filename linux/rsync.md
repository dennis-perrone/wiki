# Rsync

## Definition  
- The `rsync` command is a way to copy files from one system to another system securely. The tool uses an algorithm that minimizes the amount of copied data by synchronizing only the changed portions of files. If two files or directories are similar between two servers, then the `rsync` command copies only the differences between the file systems.  

## Command Options

- **`-r`** or **`--recursive`**: Synchronize the whole directory tree recursively.  
- **`-l`** or **`--links`**: Synchronize symbolic links  
- **`-p`** or **`--perms`**: Permissive permissions  
- **`-t`** or **`--times`**: Preserve time stamps  
- **`-g`** or **`--group`**: Preserve group ownership  
- **`-o`** or **`--owner`**: Preserve the owner of the files  
- **`-D`** or **`--devices`**: Preserve device files  
- **`-n`**: Dry run. Simulates actual actions  
- **`-a`**: Enables archive mode.  
  
**NOTE**: A trailing `/` will copy the contents of a directory, no `/` will copy the entire root directory.  
	- `rsync -av /home /backup` will result in the `home` in the `/backup` directory.  
	- `rsync -av /home/ /backup` will result in the folders and subdirectories within `/home` to be copied to `/backup`  

## Usage
- To move `/var/log` to `/tmp` on local box:  
	- `rsync -av /var/log /tmp`  
- To move `/var/log` to `/tmp` on remote box:  
	- `rsync -av /var/log hostname:/tmp`  
- To retrieve `/var/log` from remote box and place in `/tmp`:  
	- `rsync -av hostname:/var/log /tmp`  
