Neovim was forked from Vim 7.4.160; it is kept up-to-date with relevant Vim patches in order to avoid duplicate work. For details, see [issue #438](https://github.com/neovim/neovim/issues/438).

Visit the [**vim patch report**](http://neovim.org/doc/reports/vimpatch/) to see which patches are needed, or use the [**vim-patch.sh**](https://github.com/neovim/neovim/blob/master/scripts/vim-patch.sh) script: 

    ./scripts/vim-patch.sh --list

Everyone is welcome to send pull requests for relevant Vim patches (see [below](#pull-requests)). But some types of patches are **not relevant to Neovim:**

- **Compiler warning fixes**: Neovim strives to have no warnings at all, and has a very different build system from Vim.
- **#ifdef tweaking**: For example, Vim decided to enable `FEAT_VISUAL` for all platforms—but Neovim already does that. Adding new `FEAT_` guards also isn't relevant to Neovim.
- **Legacy system support**: Fixes for legacy systems such as Solaris, Amiga, Xenix, Mac OS 9, Windows 95, MS-DOS, are not needed because they are not supported by Neovim.
- Most **GUI-related** changes: Neovim GUIs are implemented external to the core C codebase.

Anything else might be relevant; err on the side of caution, and post an issue if you aren't sure. 

To mark a patch as "Not Applicable", append `NA` next to the commented-out patch number in `version.c`.

Quick start
-----------

Say you've pulled down the Neovim source, and you want to merge Vim patch 7.4.123. Now just run [**vim-patch.sh**](https://github.com/neovim/neovim/blob/master/scripts/vim-patch.sh):

    ./scripts/vim-patch.sh 7.4.123

The script guides you with further instructions. It's easy and painless, just try it!

Pull requests
-------------

- The pull request *title* should include `vim-patch:7.4.xxx`. 
- If the patch includes a new test (`src/testdir/test*.in`), please convert it to lua tests (see [#1286](https://github.com/neovim/neovim/issues/1286) and [#1328](https://github.com/neovim/neovim/pull/1328)). This usually just means [running a script](https://github.com/neovim/neovim/pull/2178#issuecomment-83230194) and tweaking the result.
- The [*commit message*](https://github.com/neovim/neovim/commit/4ccf1125ff569eccfc34abc4ad794044c5ab7455) should include:
    - A token indicating the Vim patch number, formatted as follows (no space!): <br/>
     `vim-patch:7.4.123`
    - A URL pointing to the Vim commit: <br/>
      https://code.google.com/p/vim/source/detail?r=5d03c374712128077ac4c342aad02120ed98df70
    - The original Vim commit message, including the author
    - **The [vim-patch.sh](https://github.com/neovim/neovim/blob/master/scripts/vim-patch.sh) script automates most of this for you.**

**Reviewers:** [hint for reviewing `runtime/` patches](https://github.com/neovim/neovim/pull/1744#issuecomment-68202876)


Code differences
----------------

- Where Vim code uses `malloc()` and friends, merges to Neovim [should use `xmalloc` and related `memory.c` "x-functions"](https://github.com/neovim/neovim/pull/691#issuecomment-52400360).
- Where Vim code uses `vim_free()`, Neovim uses `free()`.
- Vim tests (in `src/testdir/`) should be converted to lua tests (see [#1286](https://github.com/neovim/neovim/issues/1286) and [#1328](https://github.com/neovim/neovim/pull/1328))
    - [Checklist for migrating legacy tests](https://github.com/neovim/neovim/wiki/Unit-tests#checklist-for-migrating-legacy-tests)
- `copy_chars()` and `copy_spaces()` were removed; use `memset()` instead [#1635](https://github.com/neovim/neovim/pull/1635)
