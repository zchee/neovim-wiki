**Why Lua was chosen for writing tests and implementing vimscript instead of python/ruby/javascript/<fill with your favorite scripting language> ?**

Lua is a very small language, yet it provides everything we need to implement a language like vimscript, which was created to configure and script the editor. The biggest advantage that languages like python or ruby have over Lua is their huge library collection, but that isn't a factor for our main use case which is to remove many thousands of C sloc by using Lua as a Vimscript runtime. If you are still not convinced about lua, you might want to read [this post](http://www.altdevblogaday.com/2013/02/19/why-lua/).

**Lua and Vimscript are distinct languages with different semantics, how can lua be used as a runtime for vimscript?**

The idea is to first make Neovim completely scriptable by Lua. Unlike the Lua interface to vim, this new implementation needs to have the same power as Vimscript, with APIs for defining syntax rules, etc. Then a Vimscript -> Lua translator will be implemented, with the generated code targeting the new Lua API

**Right now only vimscript is parsed, now there will will an additional pass for parsing lua. Won't that make the editor slower?**

We'll be using [Luajit](http://luajit.org/), which the fastest scripting runtime out there(just google it). There will be a small overhead in parsing an additional language, but that will be insignificant near the great runtime performance improvement, especially because vimscript is known to be one of the slowest scripting languages(python is significantly faster than it). There is a good chance that plugins will run  faster, improving the editor performance.

**Ok but why write tests in [Moonscript](http://moonscript.org/)?**

Moonscript is a very nice DSL for writing BDD-like specs, which is how the tests are being written. It also compiles to lua, removing dependency on another runtime for running tests. Another advantage is that Luajit includes a nice [ffi module](http://luajit.org/ext_ffi_api.html) that is great for unit testing C code.