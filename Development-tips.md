# Building Neovim

If you just pulled the Neovim source and want to get a working `nvim` binary,

    make

pulls down third-party dependencies (such as libuv and luajit) into `.deps/`, and builds them. If you're missing a dependency such as `libtool`, the configure script will let you know, then you try `make` again.  

Now that you have dependencies, you can try other build targets. Some suggestions are below.

### Building a "release" build (optimized, NDEBUG)

    rm build/ ; make clean && make CMAKE_BUILD_TYPE=MinSizeRel

"MinSizeRel" is CMake jargon for "minimum-sized release". 

### Custom Makefile 
You can customize the build process locally on your machine by creating `local.mk` which is referenced at the top of the main `Makefile` (and listed in `.gitignore`). **A new target in `local.mk` overrides the default make-target.**

Here's a sample `local.mk` which adds a target to force a rebuild but *does not* override the default-target:
```make
all:

rebuild:
	rm -rf build && make
```

# YouCompleteMe
Those browsing through the source or working on PRs might find [this](https://gist.github.com/tarruda/8736305) useful.

# Code Linting
If you are using Syntastic you can use https://gist.github.com/gilligan/9326904 to add clint.py as checker
for C files. Note that clint.py needs to be in your path and that you will have to modify g:syntastic_c_checkers because it'll otherwise use gcc or make as default. See the syntastic documentation for details on that.

# Debugging

### Using the vim-lldb plugin
Get the plugin: https://github.com/gilligan/vim-lldb
In order to get started:
  1. Start neovim in a shell
  2. Open some neovim source file
  3. :Ltarget attach nvim
  4. Go to some line you are interested in and do :Lbreakpoint

### Using `gdb` in the terminal
Use two terminals, one for the debugging session, and one for the neovim instance that will be debugged.
In the terminal for `neovim`, start a `gdbserver` instance on a specific port like this:

    gdbserver :666 build/nvim

This will start a remote debugging session for the binary `build/nvim` on port `666`.

You then need to attach to this debugging session in the other terminal:

    gdb build/nvim

Once you've entered `gdb`, you need to attach to the remote session:

    target remote localhost:666

You are now attached to the remote debugging session. 
Try setting a breakpoint and start the application:

- `br main` to set the breakpoint.
- `c` to continue running the application

You can now step through source, and you'll see the results in the other window.

### tmux
It might be convenient to use your own makefile to quickly start debugging sessions using the above `gdbserver` method. This example will create the debugging session when you type `make debug`.
This assumes that you have `Makefile` in your github projects parent directory.

```
.PHONY: dbg-start dbg-attach debug build

build:
	@$(MAKE) -C neovim

dbg-start: build
	@tmux new-window -n 'dbg-neovim' 'sudo gdbserver :666 ./neovim/build/src/vim -D'

dbg-attach:
	@tmux new-window -n 'dbg-cgdb' 'cgdb -x gdb_start.cmd ./neovim/build/src/vim'

debug: dbg-start dbg-attach
```

Here `gdb_start.cmd` includes `gdb` commands to be called when the debugger starts. It needs to attach to the server started in the `dbg-start` rule. Here's an example:

```
target remote localhost:666
br main
```

