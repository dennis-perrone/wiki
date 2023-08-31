# How to set up WeeChat

## References

1. [WeeChat Setup](https://gist.github.com/pascalpoitras/8406501)
2. [Search Channels](https://superuser.com/questions/619771/how-do-i-search-for-channel-names-in-weechat)

## Configure Client

```code

/mouse enable

```

This enables mouse clicking

```code
/secure passphrase <pass>
/secure set liberachatpass <pass>
/secure set defaultnicks <nicks-csv>
/secure set defaultsasluser <username>
```

Set passphrase and enables encrypted passwords/usernames. This is stored in ```~/.config/weechat/sec.conf```

```code
/set irc.server_default.sasl_mechanism PLAIN
/set irc.server_default.sasl_username ${sec.data.defaultsasluser}
/set irc.server_default.nicks ${sec.data.defaultnicks}
/set irc.server_default.capabilities "*"

/server add libera irc.libera.chat/6697 -ssl -autoconnect
/set irc.server.libera.sasl_password ${sec.data.liberachatpass}

/connect -auto

/set weechat.plugin.autoload "*,!guile,!javascript,!lua,!php,!tcl,!perl,!ruby,!fifo,!xfer"

/set spell.check.default_dict en
/set spell.check.suggestions 3
/set spell.color.suggestion *green
/spell enable

/set logger.level.irc 4
/set logger.mask.irc %Y/$server/$channel.%m-%d.log

/set fset.color.line_selected_bg1 default
/set fset.color.name_changed 229
/set fset.color.name_changed_selected *229
/set fset.color.type 121
/set fset.color.type_selected *121
/set fset.color.value 31
/set fset.color.value_changed 229
/set fset.color.value_changed_selected *229
/set fset.color.value_selected *31
/set fset.look.auto_refresh "*,!weechat.bar.buflist.size,!plugins.var.buflist.section.*,!plugins.var.python.text_item.conky_*"
/set fset.format.option1 "${if:${selected_line}?${color:*white}>>:  } ${marked} ${name}  ${type}  ${value2}"
/set weechat.bar.fset.conditions "${buffer.full_name} == fset.fset && ${window.win_height} > 7"  

/set script.scripts.download_enabled on
/script install autosort.py buffer_autoset.py cmd_help.py

/buffer_autoset add core.weechat notify 3
/buffer_autoset add irc.server.* notify 3
/buffer_autoset add relay.relay.list short_name relay

/set plugins.var.python.cmd_help.color_delimiters "*white"
/set plugins.var.python.cmd_help.color_arguments "121"
/set plugins.var.python.cmd_help.color_list "121"
/set plugins.var.python.cmd_help.start_on_load "on"
/set plugins.var.python.cmd_help.stop_on_enter "off"

/bar set buflist priority 2000
```

Cloak IP address

[Reference](https://libera.chat/guides/cloaks#requesting-a-self-service-user-cloak)

```code

/join #libera-cloak
Say !cloakme

```

To hide real name and the local user name

[Reddit Reference](https://www.reddit.com/r/linuxquestions/comments/m303nm/comment/gqmex9x/?utm_source=share&utm_medium=web2x&context=3)

```code

/set irc.server.libera.username "My user name"
/set irc.server.libera.realname "My real name"

```

## Useful Commands

To search for channels containing ```python``` in their name

```code

/msg alis list *python*

```

To search for a channel who's topic contains the word ```python```

```code
/msg alis list * -topic *python*

```
