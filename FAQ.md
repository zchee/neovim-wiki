### I am a Vim user, and I want to try out Neovim... what is the quickest way to set it up?

Link your previous configuration so Neovim can use it:

~~~
ln -s ~/.vimrc ~/.nvimrc
ln -s ~/.vim ~/.nvim
~~~

If you use python plugins, make sure to install [the python package](http://neovim.io/doc/user/nvim_python.html):

~~~
pip install neovim
pip3 install neovim
~~~

#### OK, but now I get some errors... what is going on?

Your configuration might not be entirely compatible. For a full list of differences between Vim and Neovim, please consult [this document](http://neovim.io/doc/user/vim_diff.html#vim-differences).

Just to give an example: the `ttymouse` option was removed in Neovim (you shouldn't need it). If you use it in Vim, you might want to guard it in your configuration, like this:

~~~ vim
if !has('nvim')
    set ttymouse=xterm2
endif
~~~

Likewise, if you wanted to have Neovim specific configuration, you could do it like this:

~~~ vim
if has('nvim')
     tnoremap <Esc> <C-\><C-n>
endif
~~~

Btw, this makes the `Escape` key leave [terminal mode](http://neovim.io/doc/user/nvim_terminal_emulator.html#nvim-terminal-emulator).

For a more granular approach, use the [`exists()`](http://neovim.io/doc/user/eval.html#exists%28%29) function:
```vim
if exists(':tnoremap')
...
endif
```

#### Can I use Lua/Ruby-based Vim plugins?

No; the legacy interfaces required by plugins such as [neocomplete](https://github.com/Shougo/neocomplete.vim) (`if_lua`) and [LustyExplorer](https://github.com/sjbach/lusty) (`if_ruby`) are not (yet) supported in Neovim.

#### How do you manage your plugins?

Just like in Vim. The most common plugin managers (vim-plug, NeoBundle, Vundle, VAM) are all supported.

### How do I use [feature]?

There's a good chance `[feature]` is already documented under [`:help nvim_intro.txt`](http://neovim.io/doc/user/nvim_intro.html).

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

### I have some technical questions...

Look in the [Technical FAQ](https://github.com/neovim/neovim/wiki/Technical-FAQ), perhaps there's an answer.

### I'm confused, I need more help...

Join [the gitter room](https://gitter.im/neovim/neovim), someone will help you out (at least, someone usually does ;)). There's also an IRC chatroom (`#neovim` at freenode). 

#### Who is that `marvim` guy at gitter/IRC? He's *everywhere*!

That's a bot that links the gitter and IRC rooms, the name of the real person talking is prefixed to whatever marvin relays. (The bot tends to break, so don't assume you are being listened to in both channels).