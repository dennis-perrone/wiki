# Add Container Name to Shell Prompt

```bash
function show_container() {
if [[ -f "/run/.containerenv" ]]; then
  TOOLBOX_NAME=[$(cat /run/.containerenv | grep 'name=' | sed -e 's/^name="\(.*\)"$/\1/')]
  echo $TOOLBOX_NAME
else
  TOOLBOX_NAME=""
fi
}
```

- Within the prompt, add `$(show_container)` to where ever it should be displayed.
