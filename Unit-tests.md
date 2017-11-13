Tests are broadly divided into *unit tests* ([test/unit](https://github.com/neovim/neovim/tree/master/test/unit) directory) and *functional tests* ([test/functional](https://github.com/neovim/neovim/tree/master/test/functional) directory). Use any of the existing tests as a template to start writing new tests.

- _Unit_ testing is achieved by compiling the tests as a shared library which is loaded and called by LuaJit [FFI](http://luajit.org/ext_ffi.html).
- _Functional_ tests are driven by RPC, so they do not require LuaJit (as opposed to Lua).

You can learn the [key concepts of Lua in 15 minutes](http://learnxinyminutes.com/docs/lua/).

## Running Tests

See [Running tests](https://github.com/neovim/neovim/wiki/Running-tests)

## Guidelines for writing tests

- Consider [BDD](http://en.wikipedia.org/wiki/Behavior-driven_development) guidelines for organization and readability of tests. Describe what you're testing (and the environment if applicable) and create specs that assert its behavior.
- For testing static functions or functions that have side effects visible only in module-global variables, create accessors for the modified variables. For example, say you are testing a function in misc1.c that modifies a static variable, create a file `test/c-helpers/misc1.c` and add a function that retrieves the value after the function call. Files under `test/c-helpers` will only be compiled when building the test shared library.
- Luajit needs to know about type and constant declarations used in function prototypes. The [helpers.lua](https://github.com/neovim/neovim/blob/master/test/unit/helpers.lua) file automatically parses `types.h`, so types used in the tested functions must be moved to it to avoid having to rewrite the declarations in the test files (even though this is how it's currently done currently in the misc1/fs modules, but contributors are encouraged to refactor the declarations).
    - Macro constants must be rewritten as enums so they can be "visible" to the tests automatically.
- Busted supports various "output providers". The **[gtest](https://github.com/Olivine-Labs/busted/pull/394) output provider** shows verbose details that can be useful to diagnose hung tests. Either modify the Makefile or compile with `make CMAKE_EXTRA_FLAGS=-DBUSTED_OUTPUT_TYPE=gtest` to enable it.
- **Use busted's `pending()` feature** to skip tests ([example](https://github.com/neovim/neovim/commit/5c1dc0fbe7388528875aff9d7b5055ad718014de#diff-bf80b24c724b0004e8418102f68b0679R18)). Do not silently skip the test with `if-else`. If a functional test depends on some external factor (e.g. the existence of `md5sum` on `$PATH`), *and* you can't mock or fake the dependency, then skip the test via `pending()` if the external factor is missing. This ensures that the *total* test-count (success + fail + error + pending) is the same in all environments.
    - *Note:* `pending()` is ignored if it is missing an argument _unless_ it is [contained in an `it()` block](https://github.com/neovim/neovim/blob/d21690a66e7eb5ebef18046c7a79ef898966d786/test/functional/ex_cmds/grep_spec.lua#L11). Provide empty function argument if the `pending()` call is outside of `it()` ([example](https://github.com/neovim/neovim/commit/5c1dc0fbe7388528875aff9d7b5055ad718014de#diff-bf80b24c724b0004e8418102f68b0679R18)).
- Use `make testlint` for using the shipped luacheck program ([supported by syntastic](https://github.com/scrooloose/syntastic/blob/d6b96c079be137c83009827b543a83aa113cc011/doc/syntastic-checkers.txt#L3546)) to lint all tests.

### Where tests go

- _Unit tests_ ([test/unit](https://github.com/neovim/neovim/tree/master/test/unit))  should match 1-to-1 with the structure of `src/nvim/`, because they are testing functions directly. E.g. unit-tests for `src/nvim/undo.c` should live in `test/unit/undo_spec.lua`.
- _Functional tests_ ([test/functional](https://github.com/neovim/neovim/tree/master/test/functional)) are higher-level (plugins and user input) than unit tests; they are organized by concept. 
    - Try to find an existing `test/functional/*/*_spec.lua` group that makes sense, before creating a new one.

## Checklist for migrating legacy tests

**Note:** Only "old style" (`src/testdir/*.in`) legacy tests should be converted. Please _do not_ convert "new style" Vim tests (`src/testdir/*.vim`). The "new style" Vim tests are faster than the old ones, and converting them takes time and effort better spent elsewhere.

- Remove the test from the Makefile (`src/nvim/testdir/Makefile`).
- Remove the associated `test.in`, `test.out`, and `test.ok` files from `src/nvim/testdir/`.
- Make sure the lua test ends in `_spec.lua`.
- Make sure the test count increases accordingly in the build log.
- Make sure the new test contains the same control characters (`^]`, ...) as the old test.
  - Instead of the actual control characters, use an equivalent textual representation (e.g. `<esc>` instead of `^]`). The `scripts/legacy2luatest.pl` script does some of these conversions automatically.

## Tips

- Really long `source([=[...]=])` blocks may break syntax highlighting. Try `:syntax sync fromstart` to fix it.