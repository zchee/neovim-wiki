This page outlines in what ways Neovim currently differs from Vim.

## Config files
* Use `.nvimrc` instead of `.vimrc` for storing configuration.
* Use `.nvim` instead of `.vim` to store configuration files.

## Plugins
The plugin architecture is going to be replaced. This means there is no support for Python plugins, for instance. However, a compatibility layer could eventually be written that allows existing plugins to still work, by acting as an adapter for the API.

## Removed legacy features

* Removed support for 8.3 filesystem/shortnames [#635](https://github.com/neovim/neovim/pull/635)
* Encryption/blowfish/`cryptmethod` [#699](https://github.com/neovim/neovim/pull/699). (May be partially restored by [#701](https://github.com/neovim/neovim/issues/701))