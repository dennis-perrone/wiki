# Special Permissions for Files and Directories

## u + s (suid)

	- **Effects on Files:** File executes as the user that owns the file, not as the user that ran the file.  
	- **Effects on Directories:** No effect.  
	- The user sticky bit shows it's self as a letter in the permissions path of `ls`:  
		- To assign sticky but to a directory, use `chmod 4770 dir_name` or `chmod u+s file_name`  
		- This can be validated by a "t" following the permissions `rwsr-wr-w`.
		- Lower case "t" indicates that the set uid bit has been set along with the execute permission for the "other" group.  
		- Upper case "t" indicates that the set uid bit has been set but not the execute permission for "other".  
		- Means that only the person who created the file can delete it.  

## g + s (sgid)

	- **Effects on Files:** File executes as the group that owns the file.  
	- **Effects on Directories:** Files that are created in the directory have a group owner to match the group owner of the directory.  
	- The group sticky but shows itself as a letter in the permissions path of `ls`:  
		- To assign sticky but to a directory, use `chmod 2770 dir_name` or `chmod g+s dir_name`  
		- This can be validated by "s" replacing the "x" in the group permissions. `rwxrws---.`  
		- Lower case "s" indicates that the set guid bit has been set along with the execute permission "other.  
		- Upper case "s" indicates that the set guid bit has been set but not the execute permission for "other".  

## o + t (sticky)

	- **Effects on Files:** No effect.  
	- **Effects on Directories:** Users with write access to the directory can remove only files that they own; they cannot remove or force saves to files that other users own.  
		- To assign sticky but to a directory, use `chmod 1770 dir_name` or `chmod o+t dir_name`  
		- This can be validated by a "t" following the permissions `rwxr-wr-wT`  
		- Lower case "t" indicates that the set uid bit has been set along with the execute permission for the "other" group.  
		- Upper case "t" indicates that the set uid bit has been set but not the execute permission for "other".  
		- Means that only the person who created the file can delete it.  
