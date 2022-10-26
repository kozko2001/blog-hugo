
---
title: NeoVim
date: 2022-04-14 00:00:00
---
---

# neovim-config

Followed the Youtube series of [neovim from scratch](https://www.youtube.com/playlist?list=PLhoH5vyxr6Qq41NFL4GvhFp-WLd5xzIz). Here are some notes I took :)

To install just clone the repository into `~/.config/nvim/`

During first execution, is normal that something is missing... 

Just execute `:PackerInstall`
Execute `:LSPInstall` to install LspClients

### notes

We are using lua, that means we have the configuration spread around the files, and importing them
in the init.lua


#### What are AutoCmd

Are scripts that can be executed when specific events happens, for example we could 
set to reload the plugins, each time the plugins.lua is saved.

checkout `:help autcmd` for more info and events to subscribe.

#### What is packer

Packer is a plugin to manager plugins, it enable you to download plugins for vim from other github repositories

#### What is a NerdFont

NerdFont are patched programming fonts like `CodeFira` etc... where they add all the icons from a lot of "icon" fonts out there

Take a look to https://www.nerdfonts.com/

#### What is cmp

Is a plugin for having autocompletion from a lot of different sources like
- path: files in the filesystem
- buffer: occurrences from the current buffer
- snippets
- LSP 

#### LSP more info

`:LSPInstall` => To install new LSP clients and servers
`:LspInfo` => Show wich LSP client is working

Keybindings
===========

- `gl` -> show error in current cursor
- `gd` -> go to definition
- `gi` -> go to implementation
- `C-k` -> Show documentation
- `gr` -> go to references
- `[d` -> go to prev diagnostic
- `]d` -> go to next diagnostic

#### Telescope

Telescope is a plugin that permits you to fuzzy search like...

- `Space-f` -> Find files
- `Space-t` Search in files
- Search branches etc....


#### TreeSitter

TreeSitter allow you to load better syntax parsers for files. For example vim doesn't parse correctly JSX etc...


#### Comments

- `M+/` => Comment lines in normal mode and in visual mode

#### Tree

- `Space-e` -> Shows the tree on the side

With the focus of the tree...

- `d` -> delete file
- `r` -> rename file
- `a` -> create file

#### Magit

- `Space-g` -> Magit


#### Toggle term

Terminal that you can use inside vim

- `C-\` - Open / close
- `jk` - Inside the terminal to go to normal mode

#### Markdown preview

you need to install glow from https://github.com/charmbracelet/glow

- `Space-Space-p` -> Preview markdown


#### Debugging

For debugging we use the DAP protocol?, which allow us to debug almost anything that vscode can use...

It's a bit cucumbersome to setup... let's see if we are up for the challenge...

You need to configure each launch of the debugger as you would do in the vscode, see the dap.lua file for an example

Keymaps:
- `SPACE d c` -> Launch debugger (or if you are already debugging... continue
- `SPACE d b` -> add breakpoint
- `SPACE d i/o/p` -> step into/over/out (parent)
- `SPACE d t` -> terminate debugging session
- `SPACE d r` -> Open repl => You can change the value of variables, evaluate etc..
- `SPACE d s` -> show breakpoints => breakpoints are not saved between sessions :(

#### Test

- `SPACE t t` -> executes nearest test
- `SPACE t f` => Test file 
- `SPACE t s` => show summary of tests