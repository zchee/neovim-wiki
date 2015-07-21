### Why was Lua chosen for writing tests and implementing Vimscript?

Lua is a very small language, but it provides everything we need to implement a language like Vimscript, which was created to configure and script the editor. The biggest advantage that languages like Python or Ruby have over Lua are their huge library collections, but that isn't a factor for our main use case which is to remove thousands of lines of C by using Lua as a Vimscript runtime.

If you are still not convinced about Lua, you might want to read [this post](http://blog.datamules.com/blog/2012/01/30/why-lua/).

### Lua and Vimscript are distinct languages with different semantics, how can Lua be used as a runtime for Vimscript?

The idea is to first make Neovim completely scriptable using Lua. Unlike the Lua interface to Vim, this new implementation needs to have the same power as Vimscript, with APIs for defining syntax rules, etc. Then a Vimscript -> Lua translator will be implemented, with the generated code targeting the new Lua API.

### Right now only Vimscript is parsed, but in the future there will be an additional pass for parsing Lua. Won't that make the editor slower?

We'll be using [LuaJIT](http://luajit.org/), which is the fastest scripting runtime out there. Parsing an additional language will create some overhead, but that will be insignificant compared to the large runtime performance improvements, especially since Vimscript is so slow (most Python implementations are significantly faster). There is a good chance that plugins will run faster, improving the editor performance.

### Are plugin authors encouraged to port their plugins from Vimscript to Lua? Do you plan on supporting Vimscript indefinitely? ([#1152](https://github.com/neovim/neovim/issues/1152))

We don't anticipate any reason to deprecate Vimscript, which is a valuable [DSL](https://en.wikipedia.org/wiki/Domain-specific_language) for text-editing tasks. Also, maintaining a Vimscript front-end is less costly than a mass migration of the many existing Vimscript plugins.

Porting from Vimscript to Lua just for the heck of it gains nothing. Neovim is emphatically a *fork of Vim* in order to leverage the work already spent on thousands of existing Vim plugins, while enabling *new* types of plugins and integrations.