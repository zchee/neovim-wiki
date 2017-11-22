## Pull requests

"Cleanup" PRs should include some unit tests that cover the function being changed, so that we can feel more confident about regressions, future changes, and Vim-patch merges.

For example if [coveralls](https://coveralls.io/builds/3555525/source?filename=src%2Fnvim%2Fbuffer.c) shows that `build_stl_str_hl` is not covered by our tests, any "cleanup" PR for `build_stl_str_hl` should include unit-test coverage.

## Frozen legacy modules

Refactoring Vim structurally and aesthetically is an important goal of Neovim. But there are some modules that should not be changed significantly, because they are maintained only by Bram, at present. Until someone takes "ownership" of these modules, the cost of any significant changes (including style or structural changes that re-arrange the code) to these modules outweighs the benefit. The modules are:

- `regexp.c`
- `regexp_nfa.c`
- `syntax.c`

## Style-only changes

While there is a [code style guide](http://neovim.io/develop/style-guide.xml), you should not put work into PR's that only change "trivial" code style (e.g. comment style). They would put additional burden on people [porting vim patches](https://github.com/neovim/neovim/wiki/Merging-patches-from-upstream-Vim) for not a lot of gain.

If, however, you find a portion of code that you think could be clearer by following the style guide, it would certainly be worth looking at a PR and decide on a case-by-case basis.