# NVIM Lua migration

TODO
- [ ] Figure out sourcing issue
- [X] Find link for properly setting Lua telescope keybindings.
- [ ] Figure out "header" for .lua files for specific plugins.

## How to enable telescope to search specific directories

- Use `:lua require("telescope.builtin").find_files({ search_dirs = { ".", "/data" } })`
- Add the following to the maps.lua:
  - `keymap('n', '<leader>fw', "<cmd>lua require('telescope.builtin').live_grep({search_dirs = {'~/wiki'}})<cr>", opts)`
- Change the values within the `{ }` to define which directories you want in scope.
- 
https://github.com/nvim-telescope/telescope.nvim/issues/1276#issuecomment-924631386

## Download fonts

- Download desired (or all) [patched fonts](https://github.com/ryanoasis/nerd-fonts/releases/tag/v2.3.3) from the `releases` directory.
- Unzip the zipped directory after download and move to `~/.local/share/fonts`

## Lualine

- In addition to installing lualine.vim the normal way, [patched nerd fonts](https://github.com/ryanoasis/nerd-fonts#patched-fonts) also need to be downloaded.
- Either clone the directory or download the specific fonts, then drop them into `~/.local/share/fonts`.

Reference: https://github.com/nvim-lualine/lualine.nvim

## Packer.nvim

- It makes the most sense to bootstrap this so that it auto installs on any new installations.
- Paste the following (or tailored) within `plugin.nvim` file.

```
local ensure_packer = function()
  local fn = vim.fn
  local install_path = fn.stdpath('data')..'/site/pack/packer/start/packer.nvim'
  if fn.empty(fn.glob(install_path)) > 0 then
    fn.system({'git', 'clone', '--depth', '1', 'https://github.com/wbthomason/packer.nvim', install_path})
    vim.cmd [[packadd packer.nvim]]
    return true
  end
  return false
end

local packer_bootstrap = ensure_packer()

return require('packer').startup(function(use)
  use 'wbthomason/packer.nvim'
  -- My plugins here
  -- use 'foo1/bar1.nvim'
  -- use 'foo2/bar2.nvim'

  -- Automatically set up your configuration after cloning packer.nvim
  -- Put this at the end after all plugins
  if packer_bootstrap then
    require('packer').sync()
  end
end)
```

Reference: https://github.com/wbthomason/packer.nvim

