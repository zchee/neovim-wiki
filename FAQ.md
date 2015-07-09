### How do I use [feature]?

There's a good chance `[feature]` is already documented under [`:help nvim_intro.txt`](http://neovim.io/doc/user/nvim_intro.html).

### Can I use Lua/Ruby-based Vim plugins?

No; the legacy interfaces required by plugins such as [neocomplete](https://github.com/Shougo/neocomplete.vim) (`if_lua`) and [LustyExplorer](https://github.com/sjbach/lusty) (`if_ruby`) are not (yet) supported in Neovim.

### How can I tell if I'm running `nvim` or `vim`?

```vim
if has('nvim')
...
endif
```

For a more granular approach, use the [`exists()`](http://neovim.io/doc/user/eval.html#exists%28%29) function:

```vim
if exists(':tnoremap')
...
endif
```

### How can I use true colors in the terminal?

```vim
:let $NVIM_TUI_ENABLE_TRUE_COLOR=1
```

See [this gist](https://gist.github.com/XVilka/8346728) for more information about true colors, such as what terminals support it.

### How can I change the cursor shape in the terminal?

```vim
:let $NVIM_TUI_ENABLE_CURSOR_SHAPE=1
```

This enables a narrow cursor in insert-mode, and a wide cursor in normal-mode. The environment variable is a temporary measure, and finer-grained control may be supported in the future.

`t_SI` and `t_EI` (which are [non-standard](https://groups.google.com/d/msg/vim_dev/biVcXiYcLRw/zumrjo6gP4oJ)) are ignored, as are most terminal codes. 

Note about gnome-terminal 3.6.2 (libvte-2.90-9): https://github.com/neovim/neovim/issues/2537

### When will Windows be supported?

See [#810](https://github.com/neovim/neovim/pull/810) and [#1749](https://github.com/neovim/neovim/issues/1749).

### Why was Lua chosen for writing tests and implementing Vimscript?

Lua is a very small language, but it provides everything we need to implement a language like Vimscript, which was created to configure and script the editor. The biggest advantage that languages like Python or Ruby have over Lua are their huge library collection, but that isn't a factor for our main use case which is to remove thousands of lines of C by using Lua as a Vimscript runtime. If you are still not convinced about Lua, you might want to read [this post](http://blog.datamules.com/blog/2012/01/30/why-lua/).

### Lua and Vimscript are distinct languages with different semantics, how can Lua be used as a runtime for Vimscript?

The idea is to first make Neovim completely scriptable using Lua. Unlike the Lua interface to Vim, this new implementation needs to have the same power as Vimscript, with APIs for defining syntax rules, etc. Then a Vimscript -> Lua translator will be implemented, with the generated code targeting the new Lua API.

### Right now only Vimscript is parsed, but in the future there will be an additional pass for parsing Lua. Won't that make the editor slower?

We'll be using [LuaJIT](http://luajit.org/), which is the fastest scripting runtime out there. Parsing an additional language will create some overhead, but that will be insignificant compared to the large runtime performance improvements, especially since Vimscript is so slow (most Python implementations are significantly faster). There is a good chance that plugins will run faster, improving the editor performance.

### Are plugin authors encouraged to port their plugins from Vimscript to Lua? Do you plan on supporting Vimscript indefinitely? ([#1152](https://github.com/neovim/neovim/issues/1152))

We don't anticipate any reason to deprecate Vimscript, which is a valuable [DSL](https://en.wikipedia.org/wiki/Domain-specific_language) for text-editing tasks. Also, maintaining a Vimscript front-end is less costly than a mass migration of the many existing Vimscript plugins.

Porting from Vimscript to Lua just for the heck of it gains nothing. Neovim is emphatically a *fork of Vim* in order to leverage the work already spent on thousands of existing Vim plugins, while enabling *new* types of plugins and integrations.