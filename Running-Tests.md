Neovim uses third-party tooling to execute tests. So be sure, from the repository directory, to build the tools before testing:

    make cmake

## Running tests

To run all _non-legacy_ (unit + functional) tests:

    make test

To run only _unit_ tests:

    make unittest

To run only _functional_ tests:

    make functionaltest

---

Tests can be "tagged" by adding `#` before a token in the test description.

``` lua
it('#foo bar baz', function()
  ...
end)
it('#foo another test', function()
  ...
end)
```

To run only the tagged tests:

    TEST_TAG=foo make functionaltest

---

To run a *specific* unit test:

    TEST_FILE=test/unit/foo.lua make unittest

To run a *specific* functional test:

    TEST_FILE=test/functional/foo.lua make functionaltest

To *repeat* a test many times:

    .deps/usr/bin/busted --filter 'foo' --repeat 1000 test/functional/ui/foo_spec.lua

---

To run all legacy (Vim) integration tests:

    make oldtest

To run a *single* legacy test,  run `make` with `TEST_FILE=test_name.res`. E.g. to run `test_syntax.vim`:

    TEST_FILE=test_syntax.res make oldtest

-  The `.res` extension (instead of `.vim`) is required.
- Specify only the test file name, not the full path.

### Functional tests

`$GDB` can be set to [run tests under gdbserver](https://github.com/neovim/neovim/pull/1527). If `$VALGRIND` is also set, it will add the `--vgdb=yes` option to valgrind instead of
starting gdbserver directly.
