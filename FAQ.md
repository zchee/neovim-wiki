**Note:** `:CheckHealth` detects and resolves many of the problems in this FAQ. Try it!

---

### Something broke after upgrading Neovim?

Check [Following-HEAD](https://github.com/neovim/neovim/wiki/Following-HEAD) for a list of breaking changes.

### How stable is the development (pre-release) version?

The [unstable (pre-release)](https://github.com/neovim/neovim/releases/tag/nightly) version of Neovim ("HEAD", i.e. the `master` branch) is used to aggressively stage new features and changes. It's usually stable, but will occasionally break your workflow. We depend on HEAD users to report "blind spots" that were not caught by automated tests.

Use the [stable (release)](https://github.com/neovim/neovim/releases/latest) version for a more predictable experience.

### Where should I put my config (`vimrc`)?

The default config file location is:

    ~/.config/nvim/init.vim

If you're using Windows 10, config file is located in:

    ~\AppData\Local\nvim\init.vim

You can copy your existing vimrc there, or symlink to it. [`:help nvim-from-vim`](http://neovim.io/doc/user/nvim.html#nvim-from-vim)

### Can I use Ruby-based Vim plugins (e.g. [LustyExplorer](https://github.com/sjbach/lusty))?

Yes, starting with Neovim 0.1.5 [PR #4980](https://github.com/neovim/neovim/pull/4980) the legacy Vim `if_ruby` interface is supported.

### Can I use Lua-based Vim plugins (e.g. [neocomplete](https://github.com/Shougo/neocomplete.vim))?

No. Starting with Neovim 0.2 [PR #4411](https://github.com/neovim/neovim/pull/4411) Lua is built-in, but the legacy Vim `if_lua` interface is not supported.

### How can I use true colors in the terminal?

Add this to your `init.vim`:

```vim
set termguicolors
```

See [this gist](https://gist.github.com/XVilka/8346728) for more information about true colors, such as what terminals support it.

### How to change cursor _shape_ in the terminal?

- For Nvim 0.1.7 or older: see the note about `NVIM_TUI_ENABLE_CURSOR_SHAPE` in `man nvim`.
- For Nvim 0.2 or newer: cursor styling is controlled by the `guicursor` option.
  - To _disable_ cursor styling, see `:help 'guicursor'`.
  - If you want a non-blinking cursor, use `blinkon0`. See `:help 'guicursor'`.
  - `guicursor` is enabled by _default_ only if Nvim is certain it won't cause problems. If you know that cursor shaping works on your terminal, set `guicursor` in your init.vim.
    ```
    :set guicursor=n-v-c:block-Cursor/lCursor-blinkon0,i-ci:ver25-Cursor/lCursor,r-cr:hor20-Cursor/lCursor
    ```
- The Vim terminal options `t_SI` and `t_EI` are ignored, like all other `t_XX` options. 
- Old versions of libvte (gnome-terminal, roxterm, terminator, ...) do not support cursor style control codes. [#2537](https://github.com/neovim/neovim/issues/2537)
- **Note:** some plugins like "ctrlp" override `guicursor` even when it is empty. To totally disable cursor updates, you can set `VTE_VERSION="100"`. 
    - But it would be better to fix the plugin: it should not modify `guicursor` if it is empty.

### How to change cursor _color_ in the terminal?

Currently, `guicursor`-driven cursor color **only works if `termguicolors` is set.** In the future, non-truecolor terminals may also be supported.

### Cursor style isn't restored after exiting Nvim

Terminals do not provide a way to query the cursor style. Use a `VimLeave` autocommand to set the cursor style when Nvim exits:

    au VimLeave * set guicursor=a:block-blinkon0

### Cursor shape doesn't change in tmux

Add this to your `.tmux.config`:

    set -g -a terminal-overrides ',*:Ss=\E[%p1%d q:Se=\E[2 q'

See [#3165](https://github.com/neovim/neovim/pull/3165) for discussion.

### Is Windows supported?

Yes, starting with the [`0.2` release](https://github.com/neovim/neovim/milestones/0.2).
See the [Install](https://github.com/neovim/neovim/wiki/Installing-Neovim#windows) page. 

### How to use the Windows clipboard from WSL?

    sudo ln -s /mnt/d/Neovim/bin/win32yank.exe /usr/bin/win32yank

See [#6227](https://github.com/neovim/neovim/issues/6227).

### What happened to --remote and friends?

The code for that family of command-line arguments was removed. It may eventually be reimplemented using the Neovim API, but until then [`neovim-remote`](https://github.com/mhinz/neovim-remote) can be used instead.

See [#1750](https://github.com/neovim/neovim/issues/1750) for more information.

# Runtime issues

### `clipboard: provider is not available`

Make sure that [Neovim can find its runtime](#neovim-cant-find-its-runtime).

### Copying to X11 primary selection with the mouse doesn't work

`clipboard=autoselect` is [not implemented yet](https://github.com/neovim/neovim/issues/2325). You may find this _partial_ workaround to be useful:

    vnoremap <LeftRelease> "*ygv

Note that this is only a partial workaround. It [doesn't work](https://github.com/neovim/neovim/issues/7013) for double-click (word selection) nor triple-click (line selection). But it's better than nothing.

### My CTRL-H mapping doesn't work

This was fixed in Neovim **0.2**.
If you are running Neovim **0.1.7 or older**, adjust your terminal's "kbs" (key_backspace) terminfo entry:

```
infocmp $TERM | sed 's/kbs=^[hH]/kbs=\\177/' > $TERM.ti
tic $TERM.ti
```

(Feel free to delete the temporary `*.ti` file created after running the above commands).

### `<Home>` or some other "special" key doesn't work

Make sure `$TERM` is set correctly.

- For screen or tmux, `TERM` should be `screen-256color`  (_Not_ `xterm-256color`)
- In other cases if "256" does not appear in the string it's probably wrong. Try `TERM=xterm-256color`.

### `:!` and `system()` do weird things with interactive processes

Interactive commands are supported by `:terminal` in Neovim. But `:!` and `system()` do not support interactive commands, primarily because Neovim UIs use stdio for msgpack communication, but also for performance, reliability, and consistency across platforms (see [`:help gui-pty`](http://vimhelp.appspot.com/gui_x11.txt.html#gui-pty)). 

See also [#1496](https://github.com/neovim/neovim/issues/1496)

### Python support isn't working

Run `:CheckHealth` (available in 0.1.5) inside Neovim for automatic diagnosis.

Additional hints:

- If you are using pyenv or virtualenv for the [`neovim` python module](https://pypi.python.org/pypi/neovim/), you must set `g:python_host_prog` and/or `g:python3_host_prog` to the virtualenv's interpreter path.
- Read [`:help provider-python`](https://neovim.io/doc/user/provider.html#provider-python). 
- Be sure you have the **latest version** of the `neovim` Python module.

```sh
pip install setuptools
pip  install --upgrade neovim
pip2 install --upgrade neovim
pip3 install --upgrade neovim
```

- Try with `nvim -u NORC` to make sure your `init.vim` isn't causing a problem. If you get `E117: Unknown function`, that means [Neovim can't find its runtime](#neovim-cant-find-its-runtime).

### Neovim can't find its runtime

This is the case if `:help nvim` shows `E149: Sorry, no help for nvim`.

Make sure that `$VIM` and `$VIMRUNTIME` point to Neovim's (as opposed to Vim's) runtime by checking `:echo $VIM` and `:echo $VIMRUNTIME`. This should give something like `/usr/share/nvim` resp. `/usr/share/nvim/runtime`.

Also make sure that you don't accidentally overwrite your runtimepath (`:set runtimepath?`), which includes the above `$VIMRUNTIME` by default (see `:help 'runtimepath'`).

### `E518: Unknown option: [option]`

Some very old/unnecessary options have been removed from Neovim. See [`:help nvim-features-removed`](http://neovim.io/doc/user/vim_diff.html#nvim-features-removed) for the complete list.

### Neovim is slow

Make sure you're running an optimized build of `nvim`. `:CheckHealth nvim` should report
one of these "build types":

```
Build type: RelWithDebInfo
Build type: MinSizeRel
Build type: Release
```

If it reports `Build type: Debug` and you're building Neovim from source, see [Building Neovim#optimized-builds](Building-Neovim#optimized-builds).<br/>
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

This is a [common problem](https://www.google.com/?q=tmux%20vim%20escape%20delay) 
in `tmux` / `screen` (see also [tmux/#131](https://github.com/tmux/tmux/issues/131#issuecomment-145853211)). The corresponding timeout needs to be tweaked to a low value (10-20ms).

`.tmux.conf`:

    set -g escape-time 10

`.screenrc`:

    maptimeout 10

#### "Why doesn't this happen in Vim?"

It *does* happen (try `vim -N -u NONE`), but *if you hit a key quickly after ESC* then Vim interprets the ESC as ESC instead of ALT (META). You won't notice the delay unless you closely observe the cursor. The tradeoff is that Vim won't understand ALT (META) key-chords, so for example `nnoremap <M-a>` won't work. ALT (META) key-chords always work in Nvim. See also `:help xterm-cursor-keys` in Vim.

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

### Why not use JSON for RPC?

- JSON cannot easily/efficiently handle binary data
- JSON specification is ambiguous: http://seriot.ch/parsing_json.php

### Why was Lua chosen for writing tests and implementing VimL?

Lua is a very small language, but it provides everything we need to implement a language like VimL, which was created to configure and script the editor. The biggest advantage that languages like Python or Ruby have over Lua are their huge library collections, but that isn't a factor for our main use case which is to remove thousands of lines of C by using Lua as a VimL runtime.

See also these articles about Lua:

- [Why Lua](https://web.archive.org/web/20150219224654/http://blog.datamules.com/blog/2012/01/30/why-lua/)
- [Redis and scripting](http://oldblog.antirez.com/post/redis-and-scripting.html)

### Lua and VimL are distinct languages with different semantics, how can Lua be used as a runtime for VimL?

The idea is to make Neovim completely scriptable using Lua. Unlike the Lua interface to Vim, this new implementation needs to have the same power as VimL, with APIs for defining syntax rules, etc. Then a VimL-to-Lua translator will be implemented, with the generated code targeting the new Lua API.

### Won't it be slower to translate VimL to Lua, instead of executing VimL directly?

We'll use [LuaJIT](http://luajit.org/), the fastest scripting runtime out there. Parsing an additional language will create some overhead, but that will be insignificant compared to the runtime performance improvements, because Vimscript is so slow. Plugins may even run faster.

**Update (2016):** [PR #243](https://github.com/neovim/neovim/pull/243) implements the VimL-to-Lua translator. But it is blocked indefinitely by [technical concerns](https://github.com/neovim/neovim/pull/243#issuecomment-153318119). Much of the work in that PR will be re-used/re-purposed (viz. [`typval_T`/`vim_to_object` refactor](https://github.com/neovim/neovim/pull/4607) and [`eval.c` refactor](https://github.com/neovim/neovim/pull/5119)).

### Are plugin authors encouraged to port their plugins from Vimscript to Lua? Do you plan on supporting Vimscript indefinitely? ([#1152](https://github.com/neovim/neovim/issues/1152))

We don't anticipate any reason to deprecate Vimscript, which is a valuable [DSL](https://en.wikipedia.org/wiki/Domain-specific_language) for text-editing tasks. Maintaining Vimscript compatibility is less costly than a mass migration of existing Vim plugins.

Porting from Vimscript to Lua just for the heck of it gains nothing. Neovim is emphatically a *fork of Vim* in order to leverage the work already spent on thousands of Vim plugins, while enabling *new* types of plugins and integrations.