### Something broke, help!

See the [Following HEAD](Following-HEAD) page.

### Where should I put my config (`vimrc`)?

The default config file location is:

    ~/.config/nvim/init.vim

You can copy your existing vimrc there, or symlink to it. [`:help nvim-from-vim`](http://neovim.io/doc/user/nvim_from_vim.html)

### Can I use Lua/Ruby-based Vim plugins?

Not yet. The legacy interfaces required by plugins such as [neocomplete](https://github.com/Shougo/neocomplete.vim) (`if_lua`) and [LustyExplorer](https://github.com/sjbach/lusty) (`if_ruby`) are not (yet) supported in Neovim.

### How can I use true colors in the terminal?

Add this to your `init.vim`:

```vim
set termguicolors
```

See [this gist](https://gist.github.com/XVilka/8346728) for more information about true colors, such as what terminals support it.

### How can I change the cursor shape in the terminal?

Add this to your `init.vim`:

```vim
:let $NVIM_TUI_ENABLE_CURSOR_SHAPE=1
```

This makes the cursor a pipe in insert-mode, and a block in normal-mode. The environment variable is a temporary measure; finer-grained control may be supported in the future.

The escape sequences `t_SI` and `t_EI` (which are [non-standard](https://groups.google.com/d/msg/vim_dev/biVcXiYcLRw/zumrjo6gP4oJ)) are ignored, as are most terminal codes. 

Note about gnome-terminal 3.6.2 (libvte-2.90-9): [#2537](https://github.com/neovim/neovim/issues/2537)

### When will Windows be supported?

See [#810](https://github.com/neovim/neovim/pull/810) and [#1749](https://github.com/neovim/neovim/issues/1749).

### What happened to --remote and friends?

The code for that family of command-line arguments was removed. It may eventually be reimplemented using the Neovim API, but for now the script [`nvim-remote`](https://github.com/mhinz/nvim-remote) can be used instead.

See [#1750](https://github.com/neovim/neovim/issues/1750) for more information.


# Runtime issues

### Something broke after updating to a newer version

See the [Following-HEAD](https://github.com/neovim/neovim/wiki/Following-HEAD) page, which documents breaking changes as they happen.

### `clipboard: provider is not available`

Make sure that [Neovim can find its runtime](#neovim-cant-find-its-runtime).

### My CTRL-H mapping doesn't work

Set `kbs=\177` in your terminal's terminfo/termcap:

```
infocmp $TERM | sed 's/kbs=^[hH]/kbs=\\177/' > $TERM.ti
tic $TERM.ti
```

See [#2048](https://github.com/neovim/neovim/issues/2048) for more information.

### `<Home>` or some other "special" key doesn't work

Make sure `$TERM` is set to something reasonable.

- If you're using screen or tmux, `TERM` should be `screen-256color`  (*Not* `xterm-256color`)
- In other cases if "256" does not appear in the string it's probably wrong. Try `TERM=xterm-256color`.

### `:!` and `system()` do weird things with interactive processes

Interactive commands are supported by `:terminal` in Neovim. But `:!` and `system()` do not support interactive commands, primarily because Neovim UIs use stdio for msgpack communication, but also for performance, reliability, and consistency across platforms (see [`:help gui-pty`](http://vimhelp.appspot.com/gui_x11.txt.html#gui-pty)). 

### Python support isn't working

- Read [`:help nvim-python`](http://neovim.io/doc/user/nvim_python.html). 
- Be sure you have the **latest version** of the `neovim` Python module.

```sh
pip  install --upgrade neovim
pip2 install --upgrade neovim
pip3 install --upgrade neovim
```

- If you still have problems, try the following commands (in Neovim) to see which Python interpreter is detected:

```vim
:let [interp, errors] = provider#pythonx#Detect(2)  " Can also be used to check for Python 3.
:echo interp  " If empty, Neovim didn't find a suitable Python interpreter.
:echo errors  " Shows which Python interpreters Neovim checked.
```

- Try with `nvim -u NORC` to make sure your `init.vim` isn't causing a problem. If you get `E117: Unknown function`, that means [Neovim can't find its runtime](#neovim-cant-find-its-runtime).
- Try [nvim-python-doctor](https://github.com/tweekmonster/nvim-python-doctor) for a detailed, robust diagnosis.

### Neovim can't find its runtime

This is the case if `:help nvim` shows `E149: Sorry, no help for nvim`.

Make sure that `$VIM` and `$VIMRUNTIME` point to Neovim's (as opposed to Vim's) runtime by checking `:echo $VIM` and `:echo $VIMRUNTIME`. This should give something like `/usr/share/nvim` resp. `/usr/share/nvim/runtime`.

Also make sure that you don't accidentally overwrite your runtimepath (`:set runtimepath?`), which includes the above `$VIMRUNTIME` by default (see `:help 'runtimepath'`).

### `E518: Unknown option: [option]`

Some options have been removed from Neovim, so you'll encounter this error if you try to use them.
See [`:help nvim-features-removed`](http://neovim.io/doc/user/vim_diff.html#nvim-features-removed) for a list of all such options, and [FAQ#how-can-i-tell-if-im-running-nvim-or-vim](https://github.com/neovim/neovim/wiki/FAQ#how-can-i-tell-if-im-running-nvim-or-vim) to avoid such errors.

### Neovim is slow

Make sure you're running an optimized build of `nvim`. To check this, run this:

    nvim --version | grep 'Build type'

This should yield one of the following:

```
Build type: RelWithDebInfo
Build type: MinSizeRel
Build type: Release
```

If it yields `Build type: Debug` and you're building Neovim from source, then see [Building Neovim#optimized-builds](Building-Neovim#optimized-builds).<br/>
If you're using a third-party package, please inform the maintainer.

### Colors aren't displayed correctly

From a shell, run `TERM=xterm-256color nvim`. If colors are displayed correctly, then export that value of `TERM` in your user profile (usually `~/.profile`):

```
export TERM=xterm-256color
```

If you're using `tmux`, instead add this to your `tmux.conf`:

```tmux
set -g default-terminal "screen-256color"
```

Some `tmux` users may need to instead use:

```tmux
set -g default-terminal "screen-256color-bce"
```

For GNU `screen`, [configure your `.screenrc`](https://wiki.archlinux.org/index.php/GNU_Screen#Use_256_colors):

    term screen-256color

**Note:** Neovim ignores `t_Co` and other terminal codes.

### Neovim can't read UTF-8 characters

Run the following from the command line:
```
locale | grep -E '(LANG|LC_CTYPE|LC_ALL)=(.*\.)?(UTF|utf)-?8'
```
If there's no results, then you might not be using a UTF-8 locale. See the following issues: [#1601](https://github.com/neovim/neovim/issues/1601) [#1858](https://github.com/neovim/neovim/issues/1858) [#2386](https://github.com/neovim/neovim/issues/2386)

### `ESC` in tmux or GNU Screen is delayed

This is [common problem](https://www.google.com/?q=tmux%20vim%20escape%20delay) 
in tmux (or screen). Set the escape-time to a low value (10-20ms) in `.tmux.conf`:

    set -g escape-time 10

or in `.screenrc`:

    maptimeout 10

See also: https://github.com/tmux/tmux/issues/131#issuecomment-145853211

# Installation issues

### Generating helptags failed

If re-installation fails with `Generating helptags failed`, try removing the previously installed runtime directory (if `CMAKE_INSTALL_PREFIX` is not set during building, the default is `/usr/local/share/nvim`):

```
# rm -r /usr/local/share/nvim
```

# Build issues

### General build issues

Run `make distclean && make` to rule out a stale build environment causing the failure.

### Proxy issues [#2482](https://github.com/neovim/neovim/issues/2482)

If your machine is behind a network proxy and you see this error:

    Error: Failed installing dependency: https://rocks.moonscript.org/penlight-1.3.2-2.rockspec 
    Error fetching file: Failed downloading http://stevedonovan.github.io/files/penlight-1.3.2-core.zip 

this can be fixed by setting the [`https_proxy` environment variable (for cURL)](http://curl.haxx.se/docs/manpage.html).

### Settings in `local.mk` don't take effect

CMake caches build settings, so you might need to run `rm -r build && make` after modifying `local.mk`.

### CMake errors

`configure_file Problem configuring file`

This is probably a permissions issue, which can happen if you run `make` as the root user, then later run an unprivileged `make`. To fix this, run `rm -rf build` and try again.

`A suitable Lua interpreter was not found.`

This can be caused by a local LuaRocks installation. Try unsetting the `LUA_PATH` and `LUA_CPATH` environment variables (via `unset`) before building.

### Lua packages

The Lua packages required by the build process should be automatically installed by [LuaRocks](http://luarocks.org/) (invoked by CMake automatically), but sometimes this will fail. Generally, this means either:

- The LuaRocks servers are down.
- The program `unzip` isn't found. If this is the case, LuaRocks will report something like this: `Warning: Failed searching manifest: Failed loading manifest: Failed extracting manifest file`.
- The `CDPATH` environment variable is interfering with the build, so it should be unset prior to running `make`.

To avoid the first error, a LuaRocks mirror can be used by creating the file `.deps/usr/etc/luarocks/config-5.1.lua` with the following contents:

```
rocks_servers={ 
 "http://luarocks.giga.puc-rio.br/" 
}
```

After that, run `make cmake`.

Failing the above, you can always try installing the following packages manually:

- [LPeg](http://www.inf.puc-rio.br/~roberto/lpeg/)
- [lua-MessagePack](http://fperrad.github.io/lua-MessagePack/)
- [busted](http://olivinelabs.com/busted/) (required for running tests, e.g., `make test`)

Keep in mind that some of those packages have their own dependencies which also have to be installed, and the version you install hasn't necessarily been tested to work with Neovim.

# Design

### Why was Lua chosen for writing tests and implementing Vimscript?

Lua is a very small language, but it provides everything we need to implement a language like Vimscript, which was created to configure and script the editor. The biggest advantage that languages like Python or Ruby have over Lua are their huge library collections, but that isn't a factor for our main use case which is to remove thousands of lines of C by using Lua as a Vimscript runtime.

If you are still not convinced about Lua, you might want to read [this post](https://web.archive.org/web/20150219224654/http://blog.datamules.com/blog/2012/01/30/why-lua/).

### Lua and Vimscript are distinct languages with different semantics, how can Lua be used as a runtime for Vimscript?

The idea is to first make Neovim completely scriptable using Lua. Unlike the Lua interface to Vim, this new implementation needs to have the same power as Vimscript, with APIs for defining syntax rules, etc. Then a Vimscript -> Lua translator will be implemented, with the generated code targeting the new Lua API.

### Right now only Vimscript is parsed, but in the future there will be an additional pass for parsing Lua. Won't that make the editor slower?

We'll be using [LuaJIT](http://luajit.org/), which is the fastest scripting runtime out there. Parsing an additional language will create some overhead, but that will be insignificant compared to the large runtime performance improvements, especially since Vimscript is so slow (most Python implementations are significantly faster). There is a good chance that plugins will run faster, improving the editor performance.

### Are plugin authors encouraged to port their plugins from Vimscript to Lua? Do you plan on supporting Vimscript indefinitely? ([#1152](https://github.com/neovim/neovim/issues/1152))

We don't anticipate any reason to deprecate Vimscript, which is a valuable [DSL](https://en.wikipedia.org/wiki/Domain-specific_language) for text-editing tasks. Also, maintaining a Vimscript front-end is less costly than a mass migration of the many existing Vimscript plugins.

Porting from Vimscript to Lua just for the heck of it gains nothing. Neovim is emphatically a *fork of Vim* in order to leverage the work already spent on thousands of existing Vim plugins, while enabling *new* types of plugins and integrations.