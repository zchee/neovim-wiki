This page outlines in what ways Neovim currently differs from Vim.

## Config files
Neovim uses `.nvimrc` instead of `.vimrc` for storing configuration.

## Plugins
The plugin architecture is going to be replaced. This means there is no support for Python plugins, for instance. However, a compatibility layer could eventually be written that allows existing plugins to still work, by acting as an adapter for the API.