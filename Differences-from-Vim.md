[`:help vim_diff`](http://neovim.io/doc/user/vim_diff.html#vim-differences) documents differences between Neovim and Vim, but this wiki page may contain additional notes and links to relevant PRs.

## Defaults

* `'nocompatible'` is always set (`:set nocp` is ignored; `:set cp` is an **error**)
* `'encoding'` defaults to `utf-8` [#935](https://github.com/neovim/neovim/pull/935)

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

*These legacy Vim features were intentionally removed from Neovim.*

* Removed support for 8.3 filesystem/shortnames [#635](https://github.com/neovim/neovim/pull/635)
* [EBCDIC](https://en.wikipedia.org/wiki/EBCDIC) support
* Encryption/blowfish/`cryptmethod`/`key` [#699](https://github.com/neovim/neovim/pull/699). (May be partially restored by [#701](https://github.com/neovim/neovim/issues/701))
* `:shell` [#450](https://github.com/neovim/neovim/pull/450)
* `'shelltype'` [#1240](https://github.com/neovim/neovim/pull/1240)
* `:mode` does not accept an argument (this was for MS-DOS) [#588](https://github.com/neovim/neovim/pull/588)
* `'bioskey'` [#1353](https://github.com/neovim/neovim/pull/1353)
* `'conskey'` [#1353](https://github.com/neovim/neovim/pull/1353)
* `'textauto'` [#559](https://github.com/neovim/neovim/pull/559)
* `'textmode'` [#540](https://github.com/neovim/neovim/pull/540)
* `'ttyfast'` [#1945](https://github.com/neovim/neovim/issues/1945)
* `'edcompatible'` [#1911](https://github.com/neovim/neovim/issues/1911)
* "Easy mode" (`eview`, `evim`, `vim -y`) [#1656](https://github.com/neovim/neovim/pull/1656)
* "Vi mode" (`nvim -v`) [#2008](https://github.com/neovim/neovim/pull/2008)
* `(g)vimdiff` (solely an alias for `(g)vim -d`) 
* The ability to start `nvim` via aliases has been removed in favor
of using the existing command line arguments ([#2008](https://github.com/neovim/neovim/pull/2008) [#1849](https://github.com/neovim/neovim/pull/1849))