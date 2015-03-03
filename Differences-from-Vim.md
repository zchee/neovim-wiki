Following are notable differences in Neovim compared to Vim.

## Configuration
* Use `.nvimrc` instead of `.vimrc` for storing configuration.
* Use `.nvim` instead of `.vim` for storing configuration files.
* Use `.nviminfo` instead of `.viminfo` for persistent session information.

## Defaults

* `'nocompatible'` is always set (`set nocp` is ignored; `set cp` is an **error**)
* `'encoding'` defaults to `utf-8` [#935](https://github.com/neovim/neovim/pull/935)

## Features

* Neovim always ships with all features, in contrast to Vim which may have certain features removed depending on compile-time feature selection. This is like if Vim's "HUGE" build was the only Vim release type (except Neovim is smaller than Vim's "HUGE" build).
* `:python` and `:python3` are always available (if your system has both Python 2 & 3) and may be used side-by-side in plugins. [#718](https://github.com/neovim/neovim/issues/718#issuecomment-47589739)
    * If `python` is available on your `$PATH`, and the [`neovim` python package](https://pypi.python.org/pypi/neovim/) is installed, Neovim python plugins will "just work". You don't need to worry about [link-time details](https://github.com/Valloric/YouCompleteMe/issues/8#issuecomment-34374807) or [ABI incompatibilities](https://groups.google.com/d/msg/vim_use/l8TY2EiXNwk/A9Ef-ozbjKoJ).
* You can map meta (alt) key chords in the terminal. Examples:
    * numbers: `<m-1>`, `<m-2>`, ...
    * enter: `<m-enter>`
    * non-printable: `<m-bs>`, `<m-del>`, `<m-ins>`
    * space: `<m-space>`
    * slashes `<m-/>`, `<m-\>`
    * equals, minus: `<m-=>`, `<m-->`
    * question, dollar: `<m-?>`, `<m-$>`
    * Actually, if you find one that isn't mappable, please note it here.
* You can map `CTRL-SHIFT-...` key chords and they are distinguished from `CTRL-...` variants. Examples:
    * `<c-tab>`, `<c-s-tab>`
    * `<c-bs>`, `<c-s-bs>`
    * `<c-enter>`, `<c-s-enter>`
* Events:
    * `TabNew`
    * `TabNewEntered`
    * `TabClosed`
* Highlight groups:
    * `EndOfBuffer`

## Plugins

Neovim has a new [plugin architecture](Plugin-UI-architecture).

## Plugin compatibility layer [#872](https://github.com/neovim/neovim/pull/872) [#895](https://github.com/neovim/neovim/pull/895) [#1130](https://github.com/neovim/neovim/pull/1130)

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
* `(g)vimdiff` (solely an alias for `vim -d`) [#1849](https://github.com/neovim/neovim/pull/1849)