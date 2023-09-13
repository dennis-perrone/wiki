# Reset root password on RHEL 9

1. Press `e` on the GRUB boot.
2. Move the cursor to the rescue kernel entry to boot (the one with the word rescue in its name).
3. Press `e` to edit the selected entry.
4. Move the cursor to the kernel command line (the line that starts with linux).
5. Append rd.break. With that option, the system breaks just before the system hands control from the initramfs to the actual system.
6. Press `Ctrl+x` to boot with the changes.
7. Press Enter to perform maintenance when prompted.
