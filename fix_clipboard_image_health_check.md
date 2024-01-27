# Fix clipboard image health check

- Created:  2024-01-26 17:02:30 EST
- Modified: 2024-01-26 17:02:30 EST

## Notes

- When updating NVIM's plugins, clipboard-image.nvim will error out for health check.
- Navigate to `$HOME/.local/share/nvim/site/pack/packer/start/clipboard-image.nvim/lua/clipboard-image`.
- Edit `health.lua`
- Remove line 3 `local health = require "health"`
- Replace lines 51-57 from this:

```bash
 health.report_start "Checking dependencies"
  if is_dep_exist then
    health.report_ok(report_msg)
  else
    health.report_error(report_msg)
  end
end
```

- To this:

```bash
  vim.health.start("Checking dependencies")
  if is_dep_exist then
    vim.health.ok(report_msg)
  else
    vim.health.error(report_msg)
  end
end
```

## References

1. [Clipboard Image Pull Request](https://github.com/ekickx/clipboard-image.nvim/pull/48)
