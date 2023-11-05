# Add Last Modified Date to File

- Created:  2023-11-04
- Modified: 2023-11-04

## Notes

- Add the following into the script that creates the note:
  - `sed -i "/- Last Modified: /c\- Last Modified: $(date +%c)" <file_name>`
- My preferred format:
  - `sed -i "/- Last Modified: /c\- Last Modified: $(date +%Y-%m-%d %H:%M:%S %Z)" <file_name>`
