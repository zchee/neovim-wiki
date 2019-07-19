## Navigating the code

- Browse **[Neovim on SourceGraph](https://sourcegraph.com/github.com/neovim/neovim)**
- Install **[universal-ctags](https://github.com/universal-ctags/ctags).** "Exuberant ctags" (the typical `ctags` binary provided by your distro) is unmaintained and won't recognize many function signatures in Neovim source.
- The `contrib` folder contains a [YouCompleteMe configuration](https://github.com/neovim/neovim/tree/master/contrib/YouCompleteMe) for Neovim.

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

