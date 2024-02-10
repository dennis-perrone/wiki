# Current tmux configuration

- Created:  2024-02-09 16:05:49 EST
- Modified: 2024-02-09 16:05:49 EST

## Notes

```
# Download manager from git clone https://github.com/tmux-plugins/
tpm ~/.tmux/plugins/tpm.
# Run <prefix> + I (capital I) to install plugins.
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-yank'

#bind | split-window -h
#bind - split-window -v
bind | split-window -h -c "#{pane_current_path}"
bind - split-window -v -c "#{pane_current_path}"
unbind '"'
unbind %

bind r source-file ~/.config/tmux/tmux.conf \; display "Reloaded c
onfiguration"

bind -n M-S-Right previous-window
bind -n M-S-Left next-window

bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

unbind C-b
set -g prefix C-a
bind C-a send-prefix

set-option -sa terminal-overrides ",xterm*:Tc"
set -g mouse on

set -g base-index 1
set -g pane-base-index 1
set-window-option -g pane-base-index 1
set-option -g renumber-windows on

run '~/.tmux/plugins/tpm/tpm'
```

## References

1. [YouTube: Tmux tutorial](https://www.youtube.com/watch?v=DzNmUNvnB04&ab_channel=DreamsofCode)
