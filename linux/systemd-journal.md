# Systemd Journal

- To search by PID/UID:
  - PID: `journalctl _PID=1`
  - UID: `journalctl _UID=1`
- To search logs with `warning` or a higher priority:
  - `journalctl -p warning`
- To search logs in the last `10 minutes`:
  - `journalctl --since "--10min"`  
- To search logs since `x` time from `y` service:
  - `journalctl --since 9:00:00 _SYSTEMD_UNIT="sshd.service"`  
