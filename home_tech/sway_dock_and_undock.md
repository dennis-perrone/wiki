# Configure Sway for Dock and Undocking

## Within the sway configuration

```bash
# Move focused workspaces between monitors
bindsym $mod+Control+right move workspace to output right
bindsym $mod+Control+left move workspace to output left

gaps inner 10
gaps outer 0

default_border pixel 1

# Trying display stuff
set $laptop eDP-1
bindswitch --reload --locked lid:on output $laptop disable
bindswitch --reload --locked lid:off output $laptop enable
exec_always $HOME/bin/display_toggle.sh
```

## Display Toggle

```bash
#!/usr/bin/bash

if grep -q open /proc/acpi/button/lid/LID/state; then
    swaymsg output eDP-1 enable
else
    swaymsg output eDP-1 disable
```

## References

1. [Reddit: Managing Outputs with a Docked Laptop](https://www.reddit.com/r/swaywm/comments/z4bon6/managing_outputs_with_a_docked_laptop/)
