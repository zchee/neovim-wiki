Automated testing is essential for a project that aims to receive contributions from the community, it assists the project in growing faster without worrying about broken features. Pull requests that commit unit tests for existing functions will be given priority.

In Neovim, unit testing is achieved by compiling it as a shared library that can be loaded and called by luajit's [ffi module](http://luajit.org/ext_ffi.html). The ffi module is capable of parsing very basic C headers (no conditional directives or macro expansions), and we'll make use of this to avoid writing any glue C code. 

Each module must have a separate test script (written in lua) in the test/unit directory. It might be possible to get started real fast by looking at existing [examples](https://github.com/neovim/neovim/tree/master/test/unit), but to get a deeper understanding of how this works, the best place is the ffi module [documentation](http://luajit.org/ext_ffi.html).

## Guidelines for writing tests

- Consider [BDD](http://en.wikipedia.org/wiki/Behavior-driven_development) guidelines for organization and readability of tests. Describe what you're testing (and the environment if applicable) and create specs that assert its behavior.
- For testing static functions or functions that have side effects visible only in module-global variables, create accessors for the modified variables. For example, say you are testing a function in misc1.c that modifies a static variable, create a file `test/c-helpers/misc1.c` and add a function that retrieves the value after the function call. Files under `test/c-helpers` will only be compiled when building the test shared library.
- Luajit needs to know about type and constant declarations used in function prototypes. The [helpers.lua](https://github.com/neovim/neovim/blob/master/test/unit/helpers.lua) file automatically parses `types.h`, so types used in the tested functions must be moved to it to avoid having to rewrite the declarations in the test files (even though this is how it's currently done currently in the misc1/fs modules, but contributors are encouraged to refactor the declarations).
    - Macro constants must be rewritten as enums so they can be "visible" to the tests automatically.
- Busted supports various test "output providers". The [utfTerminalDetailed](https://github.com/neovim/neovim/pull/2156) output provider shows [verbose details](https://travis-ci.org/neovim/neovim/jobs/54478323#L1661) that can be useful to diagnose hung tests.

## Checklist for migrating legacy tests:

- remove the test from the Makefile (`src/nvim/testdir/Makefile`)
- remove the associated `test.in`, `test.out`, and `test.ok` files from `src/nvim/testdir/`
- make sure the lua test ends in `_spec.lua`
- make sure the test count increases accordingly in the build log
- make sure the new test contains the same control characters (`^]`...) as the old test