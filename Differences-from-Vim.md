[`:help vim_diff`](http://neovim.io/doc/user/vim_diff.html#vim-differences) documents differences between Neovim and Vim, but this wiki page may contain additional notes and links to relevant PRs.

## Defaults

See [`:help nvim-option-defaults`](http://neovim.io/doc/user/vim_diff.html#nvim-option-defaults) for a list of the new defaults.
See [#2676](https://github.com/neovim/neovim/issues/2676) for discussion regarding the new defaults, as well as links to the various changes.

## Features

* Neovim has a built-in terminal emulator, which can be accessed using `:term[inal]`. To exit terminal mode, press `<C-\><C-n>`. `:tmap` and `:tnoremap` can be used to create terminal mode mappings.
* Neovim always ships with all features, in contrast to Vim which may have certain features removed/added at compile-time. This is like if Vim's "HUGE" build was the only Vim release type (except Neovim is smaller than Vim's "HUGE" build).
* `:python` and `:python3` are always available (if your system has both Python 2 & 3) and may be used side-by-side in plugins. [#718](https://github.com/neovim/neovim/issues/718#issuecomment-47589739)
    * If `python` is available on your `$PATH`, and the [`neovim` python package](https://pypi.python.org/pypi/neovim/) is installed, Python plugins will work. You don't need to worry about [link-time details](https://github.com/Valloric/YouCompleteMe/issues/8#issuecomment-34374807) or [ABI incompatibilities](https://groups.google.com/d/msg/vim_use/l8TY2EiXNwk/A9Ef-ozbjKoJ).

## Plugins

Neovim has a new [plugin architecture](Plugin-UI-architecture).


A compatibility layer is provided ([#872](https://github.com/neovim/neovim/pull/872) [#895](https://github.com/neovim/neovim/pull/895) [#1130](https://github.com/neovim/neovim/pull/1130)) to support legacy Vim plugins that depend on
`if_python` (commands `:python`/`:pyfile`/`:pydo`, etc.), but there are some differences:

- Plugins runs in another process.
- `rpcrequest()` blocks until the client responds.

## Missing legacy features
 
*These legacy Vim features may be implemented in the future, but they are not planned for the current milestone.*

* `vim.bindeval()` (new feature in the Vim 7.4 Python interface)
* `if_ruby`
* `if_lua`
* `if_perl`
* `if_mzscheme`
* `if_tcl`

## Removed legacy features

See [`:help nvim-features-removed`](http://neovim.io/doc/user/vim_diff.html#nvim-features-removed) for a list of the features intentionally removed from Neovim.