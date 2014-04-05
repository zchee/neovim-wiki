## In Progress

* Replace [`eval.c`](https://github.com/neovim/neovim/blob/57cd2d661454cd6686c7d98cafa783ea94495fd5/src/eval.c) (20k lines) by VimL => Lua translator
* [Use pipes instead of temp files](https://github.com/neovim/neovim/issues/473) for `system()` calls and shell operations to improve performance and reliability (references: [1](https://groups.google.com/d/msg/vim_use/JSXaM9YjWKo/HtHn36WFb_kJ), [2](https://groups.google.com/d/msg/vim_use/adD_-9yBCEU/Y0ul-OwXGpYJ), [3](https://github.com/mattn/gist-vim/issues/48#issuecomment-12916349), [4](https://groups.google.com/d/msg/vim_use/oU7y-hmQoNc/2qQnkPl6aKkJ))
* Port all IO to libuv

## Planned

## Completed