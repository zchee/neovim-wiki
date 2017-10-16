_See **[Quickstart](#quickstart)** to get started immediately. Also note the section on [**Not Applicable** patches](#na-not-applicable-patches)._

Neovim was forked from Vim 7.4.160; it is kept up-to-date with relevant Vim patches in order to avoid duplicate work. To see the status of Vim patches, go to the  [**vim patch report**](http://neovim.io/doc/reports/vimpatch/) or run [`vim-patch.sh`](https://github.com/neovim/neovim/blob/master/scripts/vim-patch.sh): 

    ./scripts/vim-patch.sh -l

Everyone is welcome to [send pull requests](#pull-requests) for relevant Vim patches, but some types of patches are **not applicable:**

- **Compiler warning fixes**: Neovim strives to have no warnings at all, and has a very different build system from Vim.
    - **Note:** Coverity fixes in Vim *are* relevant to Neovim.
- **#ifdef tweaking**: For example, Vim decided to enable `FEAT_VISUAL` for all platforms — but Neovim already does that. Adding new `FEAT_` guards also isn't relevant to Neovim.
- **Legacy system support**: Fixes for legacy systems such as Amiga, OS/2 Xenix, Mac OS 9, Windows older than XP SP2, are not needed because they are not supported by Neovim.
- **`if_*.c`** changes: `if_python.c` et. al. were removed.
- **term.c** changes: the Neovim TUI uses libtermkey to read terminal sequences; Vim's `term.c` was removed.
- Most **GUI-related** changes: Neovim GUIs are implemented external to the core C codebase.
- Anything else might be relevant; err on the side of caution, and post an issue if you aren't sure. 

To mark a patch as "Not Applicable", append `NA` next to the commented-out patch number in `version.c`.

Quickstart
----------

1. Pull down the Neovim source (`git clone https://github.com/neovim/neovim.git`)
2. Run `./scripts/vim-patch.sh -l` to see the list of missing Vim patches.
3. Choose a patch from the list (usually the oldest one), e.g. `8.0.0123`.
4. Run `./scripts/vim-patch.sh -p 8.0.0123`
    - The script guides you with further instructions.

It's strongly recommended to work on the _oldest_ patch from the list (just make sure someone didn't already start working on it), because some patches might depend on others. You're most likely going to encounter merge conflicts regardless, but this way such conflicts are kept to a minimum.


Pull requests
-------------

_Note:_ **[vim-patch.sh](https://github.com/neovim/neovim/blob/master/scripts/vim-patch.sh)** automates these steps for you. Use it!

- The pull request *title* should include `vim-patch:8.0.xxxx` (no whitespace) 
- The [*commit message*](https://github.com/neovim/neovim/commit/4ccf1125ff569eccfc34abc4ad794044c5ab7455) should include:
    - A token indicating the Vim patch number, formatted as follows: <br/>
     `vim-patch:8.0.0123` (no whitespace)
    - A URL pointing to the Vim commit:
        - https://github.com/vim/vim/commit/c8020ee825b9d9196b1329c0e097424576fc9b3a
    - The original Vim commit message, including author

**Reviewers:** [hint for reviewing `runtime/` patches](https://github.com/neovim/neovim/pull/1744#issuecomment-68202876)

N/A ("Not Applicable") patches
------------------------------

Many Vim patches are not applicable to Neovim. We regularly update version.c to reflect this, with a single pull request. If you find NA patches, 

* find the existing "NA patches" pull request, 
* or create a new one with the intention of maintaining that pull request for a few weeks. 

The title of the pull request should be:

    version.c: mark NA patches

so that it is easy to find. See [PR #4634](https://github.com/neovim/neovim/pull/4634) for example.

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
| `vim_strncpy` `strncpy`                 | `xstrlcpy`         |
| `vim_strcat` `strncat`                  | `xstrlcat`         |
| `vim_islower` `vim_isupper`             | `mb_islower` `mb_isupper` |
| `vim_tolower` `vim_toupper`             | `mb_tolower` `mb_toupper` |

| Data type | Format (Vim source) | Portable format (Nvim source) |
|:----------|:--------------------|:------------------------------|
| `long long`    | `"%lld"`             | `"%" PRId64`                  |
| `size_t`  | `"%ld"`             | `"%zu"`                       |

- See also: https://github.com/neovim/neovim/pull/1729#discussion_r22423779
- Vim's `ga_init2` was renamed to `ga_init` and the original `ga_init` is gone.
- "Old style" Vim tests (`src/testdir/*.in`) should be converted to Lua tests (see [#1286](https://github.com/neovim/neovim/issues/1286) and [#1328](https://github.com/neovim/neovim/pull/1328)). See [Checklist for migrating legacy tests][checklist]. 
    - However, please _do not_ convert "new style" Vim tests (`src/testdir/*.vim`) to Lua. The "new style" Vim tests are faster than the old ones, and converting them takes time and effort better spent elsewhere. Just copy them to `src/nvim/testdir/*.vim` and update `src/nvim/testdir/Makefile`.
- Conditions that check `enc_utf8` are obsolete (only the "true" case is applicable).

Documentation differences
-------------------------

The following should be removed from all imported documentation, and not be used in new documentation:

- `{not in Vi}` : we don't care about compatibility with Vi (see [`818f7ae`][vi-annotations]).
- `{Only when compiled with ...}` - the vast majority of features have been made non-optional (see [Introduction](Introduction#legacy-support-and-compile-time-features))

[vi-annotations]: https://github.com/neovim/neovim/commit/818f7aefd2fe7eacd7135c5e3154934f24c85ca7

[memset]: https://github.com/neovim/neovim/pull/1635
[checklist]: Unit-tests#checklist-for-migrating-legacy-tests