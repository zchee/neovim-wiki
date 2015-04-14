## In-Progress

* Enable `-Wconversion` on all source files [#567](https://github.com/neovim/neovim/issues/567)
* Replace [`eval.c`](https://github.com/neovim/neovim/blob/57cd2d661454cd6686c7d98cafa783ea94495fd5/src/eval.c) (20k lines) by Vimscript => Lua translator
* Remove superfluous `#include`s with [include-what-you-use](https://code.google.com/p/include-what-you-use/) [#549](https://github.com/neovim/neovim/issues/549) ([why?](http://zeuxcg.org/2010/11/15/include-rules/))
* Avoid unnecessary `STRLEN`
* Port all IO to libuv
* Migrate legacy integration tests to lua + msgpack API [#1286](https://github.com/neovim/neovim/issues/1286)
* Lua plugin host (and `if_lua` compatibility layer)

## Planned

Items in the [first release milestone](https://github.com/neovim/neovim/milestones/first%20release) provide a rough estimate of progress towards a production-quality, cross-platform, packaged product.

Items in the [vNext milestone](https://github.com/neovim/neovim/milestones/vNext) are being planned or considered; they have **no release target** and may be cancelled or deferred indefinitely.

## Completed

- Python plugin host
    - Includes compatibility layer for legacy Vim python interface `if_pyth` (`:python`, `:pydo`, `:pyfile`)
- End-to-end [automation](https://github.com/neovim/bot-ci) of [documentation](http://neovim.org/doc), [analysis](http://neovim.org/doc/reports/clang), [nightly builds](https://github.com/neovim/neovim/releases/tag/nightly), etc.
- Enhance build system with lua-based C preprocessor
- Implement `system()` with pipes ([#978](https://github.com/neovim/neovim/pull/978)) instead of temp files to improve [performance](https://github.com/neovim/neovim/pull/978#issuecomment-50092527) and reliability ([1](https://groups.google.com/d/msg/vim_use/JSXaM9YjWKo/HtHn36WFb_kJ), [2](https://groups.google.com/d/msg/vim_use/adD_-9yBCEU/Y0ul-OwXGpYJ), [3](https://github.com/mattn/gist-vim/issues/48#issuecomment-12916349), [4](https://groups.google.com/d/msg/vim_use/oU7y-hmQoNc/2qQnkPl6aKkJ))
- Use `hrtime()` (more precise and monotonic) for profiling instead of `gettimeofday()` [#831](https://github.com/neovim/neovim/issues/831)
- Update translations (runtime messages--not user manual):
    - `pt_BR`
    - `de`
    - `sv`
- Implement msgpack remote API [#509](https://github.com/neovim/neovim/pull/509) [#779](https://github.com/neovim/neovim/pull/779)
- Remove support for legacy systems and move to C99
    - Remove tons of `FEAT_*` macros with [unifdef](http://dotat.at/prog/unifdef/)
    - Reduce C code from 300k lines to 170k
- Enable modern compiler features
    - Use [function attributes](https://github.com/neovim/neovim/pull/426) to aid performance, static analysis [#1113](https://github.com/neovim/neovim/issues/1113#issuecomment-53512526) [#1867](https://github.com/neovim/neovim/pull/1867)
- Format entire source with [uncrustify](http://uncrustify.sourceforge.net/)
- Replace autotools build system with [CMake](http://cmake.org/)
- Implement [continuous integration](https://travis-ci.org/neovim/neovim) and [test coverage](https://coveralls.io/r/neovim/neovim)
- 200+ new unit tests
- Split large, monolithic files (`misc1.c`) into logical units
  (`path.c`, `indent.c`, `keymap.c`, ...)
- Implement [job control](https://github.com/neovim/neovim/pull/475) ("async")
- Rework OOM handling to simplify control flow
- Remove 8.3 filename support [#635](https://github.com/neovim/neovim/pull/635)
- Use portable string format tokens [#574](https://github.com/neovim/neovim/pull/574) (improves cross-platform viability)
- [Reduce indiscriminate redraws](https://github.com/neovim/neovim/pull/485#issuecomment-39924973) to improve performance
- Remove 'proto' directory [#155](https://github.com/neovim/neovim/issues/155)
    - Vim uses a single global header `vim.h` that is included in every module and includes all other headers. This is bad for documentation (module dependencies are obscured) and incremental building (changing any header file will cause every module to be rebuilt)