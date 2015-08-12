Automated testing is essential for a project that aims to receive contributions from the community, it assists the project in growing faster without worrying about broken features. Pull requests that commit unit tests for existing functions will be given priority.

In Neovim, unit testing is achieved by compiling it as a shared library that can be loaded and called by luajit's [FFI module](http://luajit.org/ext_ffi.html).

Tests are broadly divided into *unit tests* ([test/unit](https://github.com/neovim/neovim/tree/master/test/unit) directory) and *functional tests* ([test/functional](https://github.com/neovim/neovim/tree/master/test/functional) directory). To get started quickly, look at existing [examples](https://github.com/neovim/neovim/tree/master/test/unit).

## Guidelines for writing tests

- Consider [BDD](http://en.wikipedia.org/wiki/Behavior-driven_development) guidelines for organization and readability of tests. Describe what you're testing (and the environment if applicable) and create specs that assert its behavior.
- For testing static functions or functions that have side effects visible only in module-global variables, create accessors for the modified variables. For example, say you are testing a function in misc1.c that modifies a static variable, create a file `test/c-helpers/misc1.c` and add a function that retrieves the value after the function call. Files under `test/c-helpers` will only be compiled when building the test shared library.
- Luajit needs to know about type and constant declarations used in function prototypes. The [helpers.lua](https://github.com/neovim/neovim/blob/master/test/unit/helpers.lua) file automatically parses `types.h`, so types used in the tested functions must be moved to it to avoid having to rewrite the declarations in the test files (even though this is how it's currently done currently in the misc1/fs modules, but contributors are encouraged to refactor the declarations).
    - Macro constants must be rewritten as enums so they can be "visible" to the tests automatically.
- Busted supports various "output providers". The **[gtest](https://github.com/Olivine-Labs/busted/pull/394) output provider** shows verbose details that can be useful to diagnose hung tests.
- **Use busted's `pending()` feature** to skip tests ([example](https://github.com/neovim/neovim/commit/5c1dc0fbe7388528875aff9d7b5055ad718014de#diff-bf80b24c724b0004e8418102f68b0679R18)). Do not silently skip the test with `if-else`. If a functional test depends on some external factor (e.g. the existence of `md5sum` on `$PATH`), *and* you can't mock or fake the dependency, then skip the test via `pending()` if the external factor is missing. This ensures that the *total* test-count (success + fail + error + pending) is the same in all environments.
    - *Note:* `pending()` is ignored if it is missing an argument _unless_ it is [contained in an `it()` block](https://github.com/neovim/neovim/blob/d21690a66e7eb5ebef18046c7a79ef898966d786/test/functional/ex_cmds/grep_spec.lua#L11). Provide empty function argument if if the `pending()` call is outside of `it()` ([example](https://github.com/neovim/neovim/commit/5c1dc0fbe7388528875aff9d7b5055ad718014de#diff-bf80b24c724b0004e8418102f68b0679R18)).
- Consider using [luacheck](https://github.com/mpeterv/luacheck) to lint your lua code. It is [supported by syntastic](https://github.com/scrooloose/syntastic/wiki/Lua:---luacheck).

## Legacy tests

To run a single legacy test, set `TESTNUM` to the name of the test (excluding the "test" prefix) and run `make`.

```sh
cd src/nvim/testdir

# run `test_command_count.in`
make clean && TESTNUM=_command_count make

# run `test53.in`
make clean && TESTNUM=53 make
```

## Checklist for migrating legacy tests

- Remove the test from the Makefile (`src/nvim/testdir/Makefile`).
- Remove the associated `test.in`, `test.out`, and `test.ok` files from `src/nvim/testdir/`.
- Make sure the lua test ends in `_spec.lua`.
- Make sure the test count increases accordingly in the build log.
- Make sure the new test contains the same control characters (`^]`, ...) as the old test.
  - Instead of the actual control characters, use an equivalent textual representation (e.g. `<esc>` instead of `^]`). The `legacy2luatest` script does some of these conversions automatically; you are encouraged to extend the script to support more control characters.

## Tips

- Really long `source([=[...]=])` blocks may break syntax highlighting. You can fix this by calling `:syntax sync fromstart`.