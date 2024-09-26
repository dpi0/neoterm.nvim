# Neoterm

**WARNING: This is the old default branch and no longer receives updates. Please use the default `main` branch instead.**

Simple neovim terminal plugin written in lua. Terminal runs in a floating window in a configurable position.

Requires `neovim` 0.7+ for access to the lua autocmd API.

# Usage

Neoterm provides both vim commands as well as a lua API

## Commands

Neoterm provides the following commands

| Command              | Description                                                                            |
| -------------------- | -------------------------------------------------------------------------------------- |
| `NeotermOpen`      | Open the neoterm window                                                              |
| `NeotermClose`      | Close the neoterm window                                                              |
| `NeotermToggle`      | Toggle the neoterm window                                                              |
| `NeotermRun <args>`  | Run the given command in the neoterm window                                            |
| `NeotermRerun`       | Run the previous command again                                                         |
| `NeotermExit`        | Close the neoterm window and delete the terminal buffer                                |

## Lua API

The following functions are available on the neoterm module. They map directly to the commands above

```lua
-- Setup global config
require('neoterm').setup({
  clear_on_run = true, -- Run clear command before user specified commands
  position = 'right',  -- Position of the terminal window: fullscreen (0), top (1), right (2), bottom (3), left (4), center (5) (string or integer value)
  noinsert = false,    -- Disable entering insert mode when opening the neoterm window
  width = 0.5,         -- Width of the terminal window (percentage, ratio, or range between 0-1)
  height = 1,          -- Height of the terminal window (percentage, ratio, or range between 0-1)
})

local neoterm = require('neoterm')

neoterm.open()
-- Override global config on a specific open call
neoterm.open({ position = 'bottom', noinsert = true, width = 0.7, height = 0.3 })
neoterm.close()
neoterm.toggle()
neoterm.run('ls')
-- Control whether or not the screen is cleared before running the command
neoterm.run('ls', {clear = false})
neoterm.rerun()
neoterm.exit()
```

# Example Keybindings

```vim
nnoremap <leader>tt <cmd>NeotermToggle<CR>
nnoremap <leader>tr :NeotermRun<space>
nnoremap <leader>tR <cmd>NeotermRerun<CR>
nnoremap <leader>tx <cmd>NeotermExit<CR>
tnoremap <leader>tn <C-\\><C-n>
tnoremap <leader>tt <cmd>NeotermToggle<CR>
tnoremap <leader>tx <cmd>NeotermExit<CR>
```

# Screenshots

## Right (default)
```lua
require('neoterm').open()
-- or
require('neoterm').open({ position = 'right' })
-- or
require('neoterm').open({ position = 2 })
```
![position-right](https://github.com/user-attachments/assets/f60ded98-8be4-4dd6-a77b-757ece4f5d84)

## Top
```lua
require('neoterm').open({ position = 'top', height = 0.6 })
```
![position-top](https://github.com/user-attachments/assets/3aba21d5-b0b2-4250-a415-cc478916c90a)

## Bottom
```lua
require('neoterm').open({ position = 'bottom' })
--or
require('neoterm').open({ position = 3 })
```
![position-bottom](https://github.com/user-attachments/assets/4c3f557c-44ca-4894-a75d-ef45a3943942)

## Left
```lua
require('neoterm').open({ position = 'left', width = 0.7 })
```
![position-left](https://github.com/user-attachments/assets/812a7d5b-31ed-4061-9bc8-93236b0763f4)

## Center
```lua
require('neoterm').open({ position = 'left', width = 0.6, height = 0.6 })
```
![position-center](https://github.com/user-attachments/assets/4cbbf668-c7d4-43ee-a9a6-2e5a6ba3b9fb)

## Fullscreen
```lua
require('neoterm').open({ position = 'fullscreen' })
-- or
require('neoterm').open({ position = 0 })
```
![position-fullscreen](https://github.com/user-attachments/assets/9423e593-2c86-48aa-8cba-49024c38e3be)


## Deprecation Notice

> [!WARNING]
> The `mode` option is deprecated. Please use the new `position` option instead.

#### Migration Guide

- `mode = vertical` → `position = right`

- `mode = horizontal` → `position = bottom`

- `mode = fullscreen` → `position = fullscreen`
