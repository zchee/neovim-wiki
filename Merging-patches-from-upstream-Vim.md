Neovim was forked from Vim 7.4.160; it is kept up-to-date with relevant Vim patches in order to avoid duplicate work. For details, see [#438](https://github.com/neovim/neovim/issues/438).

Visit the [**vim patch report**](http://neovim.io/doc/reports/vimpatch/) to see which patches are needed, or use the [`vim-patch.sh`](https://github.com/neovim/neovim/blob/master/scripts/vim-patch.sh) script: 

    ./scripts/vim-patch.sh -l

Everyone is welcome to send pull requests for relevant Vim patches (see [below](#pull-requests)), but some types of patches are **not relevant to Neovim:**

- **Compiler warning fixes**: Neovim strives to have no warnings at all, and has a very different build system from Vim.
    - **Note:** Coverity fixes in Vim *are* relevant to Neovim.
- **#ifdef tweaking**: For example, Vim decided to enable `FEAT_VISUAL` for all platforms — but Neovim already does that. Adding new `FEAT_` guards also isn't relevant to Neovim.
- **Legacy system support**: Fixes for legacy systems such as Solaris, Amiga, OS/2 Xenix, Mac OS 9, Windows older than XP SP2, are not needed because they are not supported by Neovim.
- **`if_*.c`** changes: `if_python.c` et. al. were removed.
- **term.c** changes: the Neovim TUI uses libtermkey to read terminal sequences; Vim's `term.c` was removed.
- Most **GUI-related** changes: Neovim GUIs are implemented external to the core C codebase.

Anything else might be relevant; err on the side of caution, and post an issue if you aren't sure. 

To mark a patch as "Not Applicable", append `NA` next to the commented-out patch number in `version.c`.

Quick start
-----------

Say you've pulled down the Neovim source, and you want to merge Vim patch 7.4.123. Now just run [**vim-patch.sh**](https://github.com/neovim/neovim/blob/master/scripts/vim-patch.sh):

    ./scripts/vim-patch.sh -p 7.4.123

The script guides you with further instructions. It's easy and painless, just try it!

If you're unsure with which patch to start or just don't care, pick one from the bottom of the queue. Merging the patches in roughly chronological order works best as some patches might depend on others. You're most likely going to encounter merge conflicts regardless, but this way such conflicts are kept to a minimum.

If you're intending to port an old patch (prior to 7.4.1000), you might want to check [relevant old patches from vim](https://github.com/neovim/neovim/wiki/Relevant-old-patches-from-vim)
Pull requests
-------------

- The pull request *title* should include `vim-patch:7.4.xxx`. 
- The [*commit message*](https://github.com/neovim/neovim/commit/4ccf1125ff569eccfc34abc4ad794044c5ab7455) should include:
    - A token indicating the Vim patch number, formatted as follows (no space!): <br/>
     `vim-patch:7.4.123`
    - A URL pointing to the Vim commit: <br/>
      https://github.com/vim/vim/commit/v7-4-123
    - The original Vim commit message, including the author
    - **The [vim-patch.sh](https://github.com/neovim/neovim/blob/master/scripts/vim-patch.sh) script automates most of this for you.**

**Reviewers:** [hint for reviewing `runtime/` patches](https://github.com/neovim/neovim/pull/1744#issuecomment-68202876)


Code differences
----------------

The following functions have been removed or deprecated in favor of newer alternatives.
See the [`memory.c` Doxygen page](http://neovim.io/doc/dev/memory_8c.html) for more information.

| Deprecated or removed                   | Replacement        |
|:----------------------------------------|:------------------:|
| `vim_free`                              | `xfree`             |
| `malloc` `alloc` `lalloc`               | `xmalloc`          |
| `calloc`                                | `xcalloc`          |
| `realloc` `vim_realloc`                 | `xrealloc`         |
| `mch_memmove`                           | `memmove`          |
| `vim_memset` `copy_chars` `copy_spaces` | [`memset`][memset] |
| `vim_strncpy` `strncpy` `strcpy`        | `xstrlcpy`         |

| Data type | Format (Vim source) | Portable format (Nvim source) |
|:----------|:--------------------|:------------------------------|
| `long`    | `"%ld"`             | `"%" PRId64`                  |
| `size_t`  | `"%ld"`             | `"%zu"`                       |

- See also: https://github.com/neovim/neovim/pull/1729#discussion_r22423779

"Old style" Vim tests (`src/testdir/*.in`) should be converted to Lua tests (see [#1286](https://github.com/neovim/neovim/issues/1286) and [#1328](https://github.com/neovim/neovim/pull/1328)). See [Checklist for migrating legacy tests][checklist]. However, please _do not_ convert "new style" Vim tests (`src/testdir/*.vim`). The "new style" Vim tests are faster than the old ones, and converting them takes time and effort better spent elsewhere.

Documentation differences
-------------------------

The following should be removed from all imported documentation, and not be used in new documentation:

- `{not in Vi}` : we don't care about compatibility with Vi (see [`818f7ae`][vi-annotations]).
- `{Only when compiled with ...}` - the vast majority of features have been made non-optional (see [Introduction](Introduction#legacy-support-and-compile-time-features))

[vi-annotations]: https://github.com/neovim/neovim/commit/818f7aefd2fe7eacd7135c5e3154934f24c85ca7

[memset]: https://github.com/neovim/neovim/pull/1635
[checklist]: Unit-tests#checklist-for-migrating-legacy-tests