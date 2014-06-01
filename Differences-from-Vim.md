This page outlines in what ways Neovim currently differs from Vim.

## Config files
* Use `.nvimrc` instead of `.vimrc` for storing configuration.
* Use `.nvim` instead of `.vim` to store configuration files.

## Plugins
Neovim has a new [plugin architecture](Plugin-UI-architecture). A compatibility layer is being developed to support legacy Vim plugins.

## Removed legacy features

* Removed support for 8.3 filesystem/shortnames [#635](https://github.com/neovim/neovim/pull/635)
* Encryption/blowfish/`cryptmethod` [#699](https://github.com/neovim/neovim/pull/699). (May be partially restored by [#701](https://github.com/neovim/neovim/issues/701))