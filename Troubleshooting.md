*If you run into an error not mentioned here and manage to resolve it, feel free to add it below.*

# Runtime issues

### CTRL-H doesn't work

See [#2048](https://github.com/neovim/neovim/issues/2048). This will be fixed for the first public release of Neovim.

### `:!` and `system()` do weird things with interactive processes

Interactive commands are supported by the `:terminal` command in Neovim. However, `:!` and `system()` do not support interactive commands, primarily because Neovim UIs use stdio for msgpack communication, but also for performance, reliability, and consistency across platforms (see [`:help gui-pty`](http://vimhelp.appspot.com/gui_x11.txt.html#gui-pty)). 

### Python support isn't working

Try executing the following commands from within Neovim to see which Python interpreter is detected by Neovim:

```vim
:let [interp, errors] = provider#pythonx#Detect(2)  " Can also be used to check for Python 3.
:echo interp  " If empty, Neovim didn't find a suitable Python interpreter.
:echo errors  " Shows which Python interpreters Neovim checked.
```

Also see [`:help nvim-python`](http://neovim.io/doc/user/nvim_python.html).

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

For GNU `screen`, [configure your `.screenrc`](https://wiki.archlinux.org/index.php/GNU_Screen#Use_256_colors):

    term screen-256color

**Note:** Neovim ignores `t_Co` and other terminal codes.

### Neovim can't read UTF-8 characters

Run the following from the command line:
```
locale | grep -E '(LANG|LC_CTYPE)=(.*\.)?UTF-8'
```
If there's no results, then you might not be using a UTF-8 locale. See the following issues: [#1601](https://github.com/neovim/neovim/issues/1601) [#1858](https://github.com/neovim/neovim/issues/1858) [#2386](https://github.com/neovim/neovim/issues/2386)

### Pressing `ESC` when running nvim in tmux inserts characters

Try setting your escape time to a low value (or even zero) in your `.tmux.conf`:

```tmux
set -g escape-time 10
```

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

### Lua packages

The Lua packages required by the build process should be automatically installed by [LuaRocks](http://luarocks.org/) (invoked by CMake automatically), but sometimes this will fail. Generally, this means either:

- The LuaRocks servers are down.
- The program `unzip` isn't found. If this is the case, LuaRocks will report something like this: `Warning: Failed searching manifest: Failed loading manifest: Failed extracting manifest file`.

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