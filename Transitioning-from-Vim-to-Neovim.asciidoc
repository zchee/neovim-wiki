Neovim is emphatically a fork of Vim, so compatibility between Vim should be pretty good.

### Getting started

To start the transition, link your previous configuration so Neovim can use it:

~~~
ln -s ~/.vimrc ~/.nvimrc
ln -s ~/.vim ~/.nvim
~~~

If you use Python plugins, make sure to install [the Python package](http://neovim.io/doc/user/nvim_python.html):

~~~
pip install --user neovim
pip3 install --user neovim
~~~

### OK, but now I get some errors... what is going on?

Your configuration might not be entirely compatible with Neovim. For a full list of differences between Vim and Neovim, see [this document](http://neovim.io/doc/user/vim_diff.html#vim-differences).

The `ttymouse` option, for example, was removed from Neovim (mouse support should work without it). If you use the same `vimrc` for Vim and Neovim, consider guarding `ttymouse` in your configuration, like so:

~~~ vim
if !has('nvim')
    set ttymouse=xterm2
endif
~~~

Conversely, if you have Neovim specific configuration items, you could do this:

~~~ vim
if has('nvim')
     tnoremap <Esc> <C-\><C-n>
endif
~~~

For a more granular approach, use the [`exists()`](http://neovim.io/doc/user/eval.html#exists%28%29) function:
```vim
if exists(':tnoremap')
     tnoremap <Esc> <C-\><C-n>
endif
```

### How do I manage my plugins?

Just like in Vim, the most common plugin managers (vim-plug, NeoBundle, Vundle, VAM) are all supported.