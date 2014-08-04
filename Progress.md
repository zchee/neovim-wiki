## In-Progress

* Replace [`eval.c`](https://github.com/neovim/neovim/blob/57cd2d661454cd6686c7d98cafa783ea94495fd5/src/eval.c) (20k lines) by VimL => Lua translator
* Remove superfluous `#include`s with Google's [include-what-you-use](https://code.google.com/p/include-what-you-use/) [#549](https://github.com/neovim/neovim/issues/549)
* Avoid unnecessary `STRLEN`
* Port all IO to libuv

## Planned

Items in the [first release milestone](https://github.com/neovim/neovim/milestones/first%20release) provide a rough estimate of progress towards a production-quality, cross-platform packaged product.

Items in the [vNext milestone](https://github.com/neovim/neovim/milestones/vNext) are being planned or considered; they have **no release target** and may be cancelled or deferred indefinitely.

## Completed

- Implement `system()` with pipes ([#978](https://github.com/neovim/neovim/pull/978)) instead of temp files to improve [performance](https://github.com/neovim/neovim/pull/978#issuecomment-50092527) and reliability ([1](https://groups.google.com/d/msg/vim_use/JSXaM9YjWKo/HtHn36WFb_kJ), [2](https://groups.google.com/d/msg/vim_use/adD_-9yBCEU/Y0ul-OwXGpYJ), [3](https://github.com/mattn/gist-vim/issues/48#issuecomment-12916349), [4](https://groups.google.com/d/msg/vim_use/oU7y-hmQoNc/2qQnkPl6aKkJ))
- Use `hrtime()` (more precise and monotonic) for profiling instead of `gettimeofday()` [#831](https://github.com/neovim/neovim/issues/831)
- Update translations (runtime messages--not user manual):
    - `pt_BR`
    - `de`
    - `sv`
- Implement msgpack remote API [#509](https://github.com/neovim/neovim/pull/509) [#779](https://github.com/neovim/neovim/pull/779)
- Remove support for legacy systems and move to C99
    - Removed tons of `FEAT_*` macros with [unifdef]
    - Reduce C code from 300k lines to 170k
- Enable modern compiler features and [optimizations](https://github.com/neovim/neovim/pull/426)
- Formatt entire source with [uncrustify]
- Replace autotools build system with [CMake]
- Implement [continuous integration] and [test coverage]
- 120+ new unit tests
- Split large, monolithic files (`misc1.c`) into logical units
  (`path.c`, `indent.c`, `keymap.c`, ...)
- [Implemented](https://github.com/neovim/neovim/pull/475) job control ("async")
- Rework out-of-memory handling resulting in greatly simplified control flow
- Merge 50+ upstream patches
- Remove 8.3 filename support [#635](https://github.com/neovim/neovim/pull/635)
- Use portable string format tokens [#574](https://github.com/neovim/neovim/pull/574)
    - First step towards building on Windows
- [Reduce indiscriminate redraws](https://github.com/neovim/neovim/pull/485#issuecomment-39924973) to improve performance
