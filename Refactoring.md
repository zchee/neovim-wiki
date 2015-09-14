## Pull requests

"Cleanup" PRs should include some unit tests that cover the function being changed, so that we can feel more confident about regressions, future changes, and Vim-patch merges.

For example, [coveralls](https://coveralls.io/builds/3555525/source?filename=src%2Fnvim%2Fbuffer.c) shows that `build_stl_str_hl` is not covered by our tests yet, so any "cleanup" PR should include unit-test coverage for `build_stl_str_hl`.

## Frozen legacy modules

Refactoring Vim structurally and aesthetically is an important goal of Neovim. But there are some modules that should not be changed significantly, because they are maintained only by Bram, at present. Until someone takes "ownership" of these modules, the cost of any significant changes (including style or structural changes that re-arrange the code) to these modules outweighs the benefit. The modules are:

- `regexp.c`
- `regexp_nfa.c`
- `syntax.c`