This page was migrated to the FAQ and CONTRIBUTING.md documents. Please update (or report) the link that took you here!

Developer info lives in one of three places:

- `:help dev` (long-lived, highly relevant info)
- [CONTRIBUTING.md](https://github.com/neovim/neovim/blob/master/CONTRIBUTING.md) (highly relevant to new contributors)
- [FAQ](https://github.com/neovim/neovim/wiki/FAQ) (transient/highly-specific info) 

## Other tools

- [hererocks](https://github.com/mpeterv/hererocks) (very similar to Python's `virtualenv`) is useful for installing Luarocks, LuaJIT, and Lua:
  ```
  curl -LO https://raw.githubusercontent.com/mpeterv/hererocks/latest/hererocks.py
  chmod u+x hererocks.py
  # Install LuaJit and LuaRocks 3.0 to the "myenv" directory.
  ./hererocks.py myenv --luajit latest -r3.0
  ```
- [croissant](https://github.com/giann/croissant) is a Lua REPL

## Experimenting with the API

You can write a simple shell that grabs the API metadata and allows you to send commands to Neovim:

https://github.com/splinterofchaos/neovim-cpp-client-experiment/blob/master/src/vim-shell.cpp

