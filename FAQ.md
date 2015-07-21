### What should I know to switch from Vim to Neovim?

See the [Transitioning from Vim to Neovim](Transitioning-from-Vim-to-Neovim) page.

### I'm using a development version of Neovim and something broke, what do I do?

See the [Following HEAD](Following-HEAD) page.

### How do I use [feature]?

There's a good chance `feature` is already documented under [`:help nvim_intro.txt`](http://neovim.io/doc/user/nvim_intro.html).

### Can I use Lua/Ruby-based Vim plugins?

No; the legacy interfaces required by plugins such as [neocomplete](https://github.com/Shougo/neocomplete.vim) (`if_lua`) and [LustyExplorer](https://github.com/sjbach/lusty) (`if_ruby`) are not (yet) supported in Neovim.

### How can I use true colors in the terminal?

Add this to your `.nvimrc`:

```vim
:let $NVIM_TUI_ENABLE_TRUE_COLOR=1
```

See [this gist](https://gist.github.com/XVilka/8346728) for more information about true colors, such as what terminals support it.

### How can I change the cursor shape in the terminal?

Add this to your `.nvimrc`:

```vim
:let $NVIM_TUI_ENABLE_CURSOR_SHAPE=1
```

This makes the cursor a pipe in insert-mode, and a block in normal-mode. The environment variable is a temporary measure; finer-grained control may be supported in the future.

The escape sequences `t_SI` and `t_EI` (which are [non-standard](https://groups.google.com/d/msg/vim_dev/biVcXiYcLRw/zumrjo6gP4oJ)) are ignored, as are most terminal codes. 

Note about gnome-terminal 3.6.2 (libvte-2.90-9): https://github.com/neovim/neovim/issues/2537

### When will Windows be supported?

See [#810](https://github.com/neovim/neovim/pull/810) and [#1749](https://github.com/neovim/neovim/issues/1749).

### I have a technical question

See the [Technical FAQ](https://github.com/neovim/neovim/wiki/Technical-FAQ) page.

### I'm confused, where do I get more help?

See the [Community](http://neovim.io/community/) page on the website. The Gitter and IRC channels are recommended for the fastest turnaround time.

### Who is that `marvim` guy on Gitter/IRC?

That's a bot that links the Gitter and IRC rooms, the name of the real person talking is prefixed to whatever marvim relays. It tends to break, so don't assume you are being listened to in both channels.