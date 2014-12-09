Following are notable differences in Neovim compared to Vim.

## Configuration
* Use `.nvimrc` instead of `.vimrc` for storing configuration.
* Use `.nvim` instead of `.vim` to store configuration files.

## Defaults

* `'nocompatible'` is always set (and `set compatible` is ignored)
* `'encoding'` defaults to `utf-8` / [#935](https://github.com/neovim/neovim/pull/935)
* `'ttyfast'` defaults to "on" / [#1045](https://github.com/neovim/neovim/issues/1045)

## Features

* Neovim always ships with all features, in contrast to Vim which may have certain features removed depending on compile-time feature selection. This is like if Vim's "HUGE" build was the only Vim release type (except Neovim is smaller than Vim's "HUGE" build).
* `:python` and `:python3` are always available (if your system has both Python 2 & 3) and may be used side-by-side in plugins. [#718](https://github.com/neovim/neovim/issues/718#issuecomment-47589739)

## Plugins

Neovim has a new [plugin architecture](Plugin-UI-architecture).

## Plugin compatibility layer [#872](https://github.com/neovim/neovim/pull/872), [#895](https://github.com/neovim/neovim/pull/895) [#1130](https://github.com/neovim/neovim/pull/1130)

A compatibility layer is provided to support legacy Vim plugins that depend on
`if_python`, `if_lua`, `if_ruby` (commands `:python`/`:pyfile`/`:pydo`, etc.), but it has some differences:

- Code runs in another process.
- `rpcrequest()` blocks until the client responds.

## Missing legacy features

*These legacy Vim features may be implemented in the future, but they are not planned for the current milestone.*

* `vim.bindeval()` (new feature in Vim 7.4 python interface)
* `if_ruby`
* `if_perl`
* `if_mzscheme`
* `if_tcl`

## Removed legacy features

*These legacy Vim features were intentionally removed in Neovim.*

* Removed support for 8.3 filesystem/shortnames [#635](https://github.com/neovim/neovim/pull/635)
* Encryption/blowfish/`cryptmethod`/`key` [#699](https://github.com/neovim/neovim/pull/699). (May be partially restored by [#701](https://github.com/neovim/neovim/issues/701))
* `:shell` [#450](https://github.com/neovim/neovim/pull/450)
* `'shelltype'` [#1240](https://github.com/neovim/neovim/pull/1240)
* `:mode` does not accept an argument (this was for MS-DOS) [#588](https://github.com/neovim/neovim/pull/588)
* `'bioskey'`
* `'conskey'`
* `'textauto'`
* `'textmode'`
* EBCDIC