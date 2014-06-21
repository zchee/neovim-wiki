This page describes notable differences in Neovim, compared to Vim.

## Configuration
* Use `.nvimrc` instead of `.vimrc` for storing configuration.
* Use `.nvim` instead of `.vim` to store configuration files.

## Plugins

Neovim has a new [plugin architecture](Plugin-UI-architecture).

## Plugin compatibility layer [#872](https://github.com/neovim/neovim/pull/872)

A compatibility layer is provided to support legacy Vim plugins that depend on
`if_python`, `if_lua`, `if_ruby` (commands `:python`/`:pyfile`/`:pydo`, `:lua`/`:luafile`/`:luado`, `:ruby`/`:rubyfile`/`:rbydo`, ...), but it has some differences:

- Code runs in another process.
- `channel_send_call()` blocks until the client responds.
- There's a hardcoded 3 second timeout before `nvim` assumes the client is stuck (for example, `python << EOF while True: pass EOF` would only block for 3 seconds).
- The call stack depth is limited to 20 (this should be more than enough for any use case).

## Removed legacy features

* Removed support for 8.3 filesystem/shortnames [#635](https://github.com/neovim/neovim/pull/635)
* Encryption/blowfish/`cryptmethod` [#699](https://github.com/neovim/neovim/pull/699). (May be partially restored by [#701](https://github.com/neovim/neovim/issues/701))