# Differences from vim

This page outlines in what ways Neovim currently differs from Vim.

## Config files
Neovim will try to read `.neovimrc` instead of `.vimrc`. If it doesn't exist, it will fall back to reading `.vimrc`.

## Plugins
The plugin architecture is going to be replaced. This means there are no support for python plugins for instance.