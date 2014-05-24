## In-Progress

* Replace [`eval.c`](https://github.com/neovim/neovim/blob/57cd2d661454cd6686c7d98cafa783ea94495fd5/src/eval.c) (20k lines) by VimL => Lua translator
* Remove superfluous `#include`s with Google's [include-what-you-use](https://code.google.com/p/include-what-you-use/) [#549](https://github.com/neovim/neovim/issues/549)
* [Use pipes instead of temp files](https://github.com/neovim/neovim/issues/473) for `system()` calls and shell operations to improve performance (and usability: [1](https://groups.google.com/d/msg/vim_use/JSXaM9YjWKo/HtHn36WFb_kJ), [2](https://groups.google.com/d/msg/vim_use/adD_-9yBCEU/Y0ul-OwXGpYJ), [3](https://github.com/mattn/gist-vim/issues/48#issuecomment-12916349), [4](https://groups.google.com/d/msg/vim_use/oU7y-hmQoNc/2qQnkPl6aKkJ))
* Avoid unnecessary `STRLEN`
* Port all IO to libuv
* msg-pack remote API

## Planned (or in discussion)

Items in the [vNext milestone](https://github.com/neovim/neovim/issues?milestone=6&state=open) are being planned or considered; they have **no specific release target** and may be cancelled or deferred indefinitely.

## Completed

- Removed support for legacy systems and moved to C99
    - Removed tons of `FEAT_*` macros with [unifdef]
    - Reduced C code from 300k lines to 170k
- Enabled modern compiler features and [optimizations](https://github.com/neovim/neovim/pull/426)
- Formatted entire source with [uncrustify]
- Replaced autotools build system with [CMake]
- Implemented [continuous integration] and [test coverage]
- Wrote 100+ new unit tests
- Split large, monolithic files (`misc1.c`) into logical units
  (`path.c`, `indent.c`, `garray.c`, `keymap.c`, ...)
- [Implemented](https://github.com/neovim/neovim/pull/475) job control ("async")
- Reworked out-of-memory handling resulting in greatly simplified control flow
- Merged 50+ upstream patches (nearly caught up with upstream)
- [Removed](https://github.com/neovim/neovim/pull/635) 8.3 filename support
- [Changed](https://github.com/neovim/neovim/pull/574) to portable format 
  specifiers (first step towards building on Windows)
- [Reduce indiscriminate redraws](https://github.com/neovim/neovim/pull/485#issuecomment-39924973) to improve performance
