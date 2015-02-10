### Why Lua was chosen for writing tests and implementing vimscript instead of python/ruby/javascript/(fill with your favorite scripting language) ?

Lua is a very small language, yet it provides everything we need to implement a language like Vimscript, which was created to configure and script the editor. The biggest advantage that languages like python or ruby have over Lua is their huge library collection, but that isn't a factor for our main use case which is to remove many thousands of C sloc by using Lua as a Vimscript runtime. If you are still not convinced about Lua, you might want to read [this post](http://blog.datamules.com/blog/2012/01/30/why-lua/).

### Lua and Vimscript are distinct languages with different semantics, how can lua be used as a runtime for vimscript?

The idea is to first make Neovim completely scriptable by Lua. Unlike the Lua interface to vim, this new implementation needs to have the same power as Vimscript, with APIs for defining syntax rules, etc. Then a Vimscript -> Lua translator will be implemented, with the generated code targeting the new Lua API

### Right now only vimscript is parsed, now there will be an additional pass for parsing Lua. Won't that make the editor slower?

We'll be using [Luajit](http://luajit.org/), which is the fastest scripting runtime out there (just google it). Parsing an additional language will cause a small overhead, but that will be insignificant next to the great runtime performance improvement, especially because Vimscript is known to be one of the slowest scripting languages (python is significantly faster than it). There is a good chance that plugins will run faster, improving the editor performance.

### Are plugin authors encouraged to port their plugins from VimL to Lua? Do you plan to support VimL indefinitely? [#1152](https://github.com/neovim/neovim/issues/1152)

We don't anticipate any reason to deprecate VimL, which is a valuable DSL for text-editing tasks. Also, maintaining a VimL front-end is less costly than a mass migration of the many existing VimL plugins.

Porting from VimL to Lua just for the heck of it gains nothing. Neovim is emphatically a *fork of Vim* in order to leverage the work already baked-into thousands of existing Vim plugins, while enabling *new* types of plugins and integrations.