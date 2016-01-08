This document is meant for people who wish to run a development build of Neovim, i.e., the most recent commit.
Its purpose is only to document breaking changes, so should NOT be used as a reference for new features—that's what [`:help nvim`](http://neovim.io/doc/user/nvim.html) is for. 

If you haven't already, see [Building Neovim](Building-Neovim)
or [Installing Neovim](Installing-Neovim), depending on your preferred installation method.

------------

### 2016/01/08

You might notice that `:version` reports `v0.1.2-...` instead of `v0.1.1-...`. This does not mean `v0.1.2` was released, but that the version now better conforms to http://semver.org/. See [#3839](https://github.com/neovim/neovim/issues/) for details.

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