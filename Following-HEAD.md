This document is meant for people who wish to run a development build of Neovim, i.e., the most recent commit.
It's purpose is only to document breaking changes, so should NOT be used as a reference for new features; that's what [`:help nvim-intro`](http://neovim.io/doc/user/nvim_intro.html) is for.

If you haven't already, see either [Building Neovim](Building-Neovim)
or [Installing Neovim](Installing-Neovim), depending on your preferred installation method.

------------

### 2015/07/15

The [`:tearoff`][tearoff] command has been removed. It was never actually implemented, so the only functional difference should be that

```vim
exists(':tearoff')
```
now returns `0` instead of `2`. See [#3003][3003] and [#3007][3007] for more information.

[tearoff]: http://vimdoc.sourceforge.net/htmldoc/gui_w32.html#:tearoff
[E319]: http://neovim.io/doc/user/message.html#E319

[3003]: https://github.com/neovim/neovim/issues/3003
[3007]: https://github.com/neovim/neovim/pull/3007

### 2015/07/19

The POSIX `'cpoptions'` flags have been removed. The `VIM_POSIX` environment variable now has no effect.

Attempting to add any of the following flags to `'cpoptions'` will trigger an error: `\` `.` `/` `&` `|` `{` `#`

See [#2943][2943] for more information.

[2943]: https://github.com/neovim/neovim/pull/2943