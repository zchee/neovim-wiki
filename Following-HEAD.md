This page documents changes which may require users to update configuration, plugins, or expectations.
Only **breaking changes** are mentioned here, this is **not** a reference for new features (see [`:help nvim`](http://neovim.io/doc/user/nvim.html) instead). 

If you don't have Neovim, see [Building Neovim](Building-Neovim) or [Installing Neovim](Installing-Neovim).

**Note:** Use `:CheckHealth` to detect and fix common problems.

------------

### 2017/05/08

Lua support ([#4411][4411]) has been merged.  This means that Lua is always available for scripting, but also means that nvim now requires either Lua or LuaJIT at runtime.  LuaJIT is the default, but one can build against Lua instead by passing `-DPREFER_LUA=ON` to cmake.

### 2017/04/03

Default 'mouse' setting changed from `mouse=a` to `mouse=` (empty). This will change again in the future after `mouse=a` is improved to make 80% of users happy. To continue using mouse, add this to your init.vim:

    set mouse=a

### 2017/04/02

Support for `$NVIM_TUI_ENABLE_CURSOR_SHAPE` was removed. Use the `guicursor` option to control cursor styling. See [FAQ](https://github.com/neovim/neovim/wiki/FAQ#how-can-i-change-the-cursor-shape-in-the-terminal). 

- To **disable** cursor style changes, set `guicursor` to empty:
  ```
  :set guicursor=
  ```
- **Note:** `guicursor` is enabled by _default_ only if Nvim is certain it won't cause problems on your terminal. If you know that cursor shaping works on your terminal, set `guicursor` in your init.vim:
  ```
  :set guicursor=n-v-c:block-Cursor/lCursor-blinkon0,i-ci:ver25-Cursor/lCursor,r-cr:hor20-Cursor/lCursor
  ```

### 2016/12/12

[#5529][5529] merged Vim's support for "partial functions" which made Nvim more strict about when the implicit `self` variable is available.  Functions that reference `self` (which is common with job callbacks) must either be declared as `dict` functions:

```vim
function! s:on_stdout(id, data, event) dict abort
```

or as part of the job options dictionary:

```vim
let s:opts = { ... }
function! s:opts.on_stdout(id, data, event) abort
```

Job callbacks also must have at least 3 parameters now. See https://github.com/neovim/neovim/issues/5763#issuecomment-266722407


### 2016/11/05

[`'encoding'`][encoding] cannot be changed to a value other than "utf-8", even during initialization. [#2905](https://github.com/neovim/neovim/pull/2905)

(Background: [#2929][2929] restricted `'encoding'` to be modifiable only during initialization. One year later, we've found no problems with UTF-8 as the internal encoding, and are now making this mandatory. This only affects the internals of Nvim, it doesn't affect file encodings or plugins.)

### 2016/08/11

`:oldfiles!` was removed in favor of restoring Vim's `:browse oldfiles` behavior.  [#5214](https://github.com/neovim/neovim/pull/5214)

### 2016/08/05

The `:Man` command is enabled by default (PR [#4449](https://github.com/neovim/neovim/pull/4449)), you no longer need

```vim
runtime! ftplugin/man.vim
``` 

in your `vimrc`.

### 2016/05/11

"True color" support now requires `set termguicolors` in your init.vim. `NVIM_TUI_ENABLE_TRUE_COLOR` is ignored. [#4690](https://github.com/neovim/neovim/pull/4690)

### 2016/02/14

`:filetype plugin indent on` and `:syntax on` are now executed by default [after your vimrc](https://github.com/neovim/neovim/blob/4bfac00aa389487c4f11d34e7a3e96e4a1116800/runtime/doc/starting.txt#L431-L444). 

* If your vimrc calls `:filetype`, Neovim will _not_ change your preference. 
* If your vimrc calls `:filetype off` or `:syntax off`, that will be respected.
* If `filetype plugin indent on` and/or `syntax on` is in your vimrc, you can delete those lines.

See `:help startup` for complete details.

### 2016/02/10

The [`DECSCUSR`](http://vt100.net/docs/vt510-rm/DECSCUSR) sequence is now sent "unwrapped" to the terminal; this affects tmux users in that cursor style changes are now localized to a tmux pane instead of being global to the parent terminal.

Depending on your terminal this may make break cursor style changes; if that happens then see `NVIM_TUI_ENABLE_CURSOR_SHAPE` in the nvim manual (`man 1 nvim`).

See [#3165](https://github.com/neovim/neovim/pull/3165) for more information.

### 2016/02/04

The `NVIM_TUI_ENABLE_TRUE_COLOR` environment variable no longer sets `has('gui_running')`. This means some (broken) colorschemes might look weird until they're fixed, but more importantly it _also_ means that various plugins that make decisions based on the result of `has('gui_running')` will not be misled into thinking the user is running outside of a terminal.

**Note:** [jellybeans](https://github.com/nanotech/jellybeans.vim) and [this molokai fork](https://github.com/justinmk/molokai) are known to work with true color even after the change . Colorschemes that _don't_ work after this change should be fixed (they should set `ctermfg`/`ctermbg` _and_ `guifg`/`guibg`, _without_ checking `has('gui_running')`)

See [#4155](https://github.com/neovim/neovim/pull/4155) for more information.

### 2016/01/14

The `'swapsync'` option has been removed. Swap files are now always `fsync(2)`'d after writing them.

See [#4009](https://github.com/neovim/neovim/pull/4009) for more information.

### 2016/01/08

You might notice that `:version` reports `v0.1.2-...` instead of `v0.1.1-...`. This does not mean `v0.1.2` was released, but that the version now better conforms to http://semver.org/.

See [#3839](https://github.com/neovim/neovim/pull/3839) for more information.

### 2015/12/12

The Getscript plugin has been removed, so the commands `GLVS`, `GetLatestVimScripts`, and `GetScripts` are no longer supported. Getscript users should consider migrating to a 3rd party plugin manager, such as [vim-plug][].

See [#2231][2231] and [#3826][3826] for more information.

[vim-plug]: https://github.com/junegunn/vim-plug
[2231]: https://github.com/neovim/neovim/issues/2231
[3826]: https://github.com/neovim/neovim/pull/3826

### 2015/11/11

The `-X` command-line flag, which was a no-op, has been removed.

See [#3641][3641] for more information.

[3641]: https://github.com/neovim/neovim/pull/3641

### 2015/11/07

The `open` command has been removed. It works the same as `visual`, so use that instead.

See [#3569][3569] for more information.

[3569]: https://github.com/neovim/neovim/pull/3569

### 2015/10/26

Neovim now supports XDG configuration. The **default config paths changed**, so `~/.nvimrc` and `~/.nvim/` will _not_ be found by default. See [`:help nvim-from-vim`](https://github.com/neovim/neovim/blob/42047acb4f07c689936b051864c6b4448b1b6aa1/runtime/doc/nvim_from_vim.txt#L12-L18) for quick migration steps.

tl;dr:

- Default user config directory is now `~/.config/nvim/` 
- Default "vimrc" location is now `~/.config/nvim/init.vim` 

### 2015/10/17

The [`'viminfo'`][viminfo] option is now an alias for [`'shada'`][shada]. [`'viminfo'`][viminfo] can no longer include `n` and it can no longer be shared with Vim.

See [#3469][3469] for more information.

[3469]: https://github.com/neovim/neovim/issues/3469
[viminfo]: http://neovim.io/doc/user/options.html#%27viminfo%27
[shada]: http://neovim.io/doc/user/options.html#%27shada%27

### 2015/09/09

The [`'encoding'`][encoding] option can no longer be changed after [initialization][].

See [#2929][2929] for more information.

[2929]: https://github.com/neovim/neovim/pull/2929
[encoding]: http://neovim.io/doc/user/options.html#%27encoding%27
[initialization]: http://neovim.io/doc/user/starting.html#initialization

### 2015/07/26

The behavior of the [`mkdir()`][mkdir] function has changed:

1. Assuming /tmp/foo does not exist and /tmp can be written to,
   `mkdir('/tmp/foo/bar', 'p', 0700)` will create both /tmp/foo and /tmp/foo/bar
   with the octal permissions 0700.
   Vim's mkdir() will create /tmp/foo with 0755.
2. If you try to create an existing directory with `'p'`, such as with `mkdir('/', 'p'))`, mkdir() will silently fail. In Vim this was an error.
3. Upon failure, mkdir() related error messages now include strerror() text.

See [#3041][3041] for more information.

[mkdir]: http://neovim.io/doc/user/eval.html#mkdir%28%29
[3041]: https://github.com/neovim/neovim/pull/3041

### 2015/07/20

The `Print` command has been removed. It works the same as `print`, so use that instead.

See [#3049][3049] for more information.

[3049]: https://github.com/neovim/neovim/pull/3049

### 2015/07/20

The default value for the `'history'` option has changed from `50` to `10000`.
To emulate the old behavior, add the following to your `nvimrc`:

```vim
set history=50
```

See [#2868][2868] and [#2676][2676] for more information.

[2868]: https://github.com/neovim/neovim/pull/2868
[2676]: https://github.com/neovim/neovim/issues/2676

### 2015/07/19

The POSIX `'cpoptions'` flags have been removed. The `VIM_POSIX` environment variable now has no effect.

Attempting to add any of the following flags to `'cpoptions'` will trigger an error: `\` `.` `/` `&` `|` `{` `#`

See [#2943][2943] for more information.

[2943]: https://github.com/neovim/neovim/pull/2943

### 2015/07/15

The [`tearoff`][tearoff] command has been removed. It was never actually implemented, so the only functional difference should be that

```vim
exists(':tearoff')
```
now returns `0` instead of `2`.

See [#3003][3003] and [#3007][3007] for more information.

[tearoff]: http://vimdoc.sourceforge.net/htmldoc/gui_w32.html#:tearoff
[E319]: http://neovim.io/doc/user/message.html#E319

[3003]: https://github.com/neovim/neovim/issues/3003
[3007]: https://github.com/neovim/neovim/pull/3007
[5529]: https://github.com/neovim/neovim/pull/5529
[4411]: https://github.com/neovim/neovim/pull/4411