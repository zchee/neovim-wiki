## Building Neovim

See the [Building Neovim](Building-Neovim) page.

## Navigating the code

- The `contrib/` folder contains a [YouCompleteMe configuration](https://github.com/neovim/neovim/tree/master/contrib/YouCompleteMe) tailored to Neovim.

## Code Linting
If you are using Syntastic you can use https://gist.github.com/gilligan/9326904 to add clint.py as checker
for C files. Note that clint.py needs to be in your path and that you will have to modify g:syntastic_c_checkers because it'll otherwise use gcc or make as default. See the syntastic documentation for details on that.

## Debugging

### Core dump

Core dumps by default are [disabled on Ubuntu](http://stackoverflow.com/a/18368068/152142) and OS X. 

    ulimit -c unlimited

to enable core dumping. If you then reproduce a segfault in `nvim`, it will "dump core". Typically this means a `core` file will appear in the current directory (or check `/var/log/apport.log` to see where it was written). You can then get a backtrace from the `core` with:

    gdb -q -n -ex bt -batch ./build/bin/nvim core > backtrace.txt

### Using `lldb` to step through unit tests

```bash
$ lldb .deps/usr/bin/luajit -- .deps/usr/bin/busted_bootstrap --lpath="./build/?.lua" --pattern=.moon test
```

### Using the `vim-lldb` plugin

  1. Install the plugin: https://github.com/gilligan/vim-lldb
  2. Open a C source file
  3. `:Ltarget attach nvim`
  4. Go to some line you are interested in, then do `:Lbreakpoint`

### Using `gdb` in the terminal

Open two terminals, one for the debugging session, and one for the Neovim instance that will be debugged.
In the terminal for `nvim`, start a `gdbserver` instance on a specific port like this:

    gdbserver :6666 build/bin/nvim

You then need to attach to this debugging session in the other terminal:

    gdb build/bin/nvim

Once you've entered `gdb`, you need to attach to the remote session:

    target remote localhost:6666

You are now attached to the remote debugging session. Try setting a breakpoint and start the application:

- `br main` to set the breakpoint.
- `c` to continue running the application

You can now step through source, and you'll see the results in the other window.

### Using `gdb` in tmux

Consider using a [custom makefile](https://github.com/neovim/neovim/wiki/Building-Neovim#custom-makefile) to quickly start debugging sessions using the above `gdbserver` method. This example will create the debugging session when you type `make debug`. This assumes that you have `Makefile` in the top-level directory.

```
.PHONY: dbg-start dbg-attach debug build

build:
	@$(MAKE) -C neovim

dbg-start: build
	@tmux new-window -n 'dbg-neovim' 'sudo gdbserver :6666 ./build/bin/nvim -D'

dbg-attach:
	@tmux new-window -n 'dbg-cgdb' 'cgdb -x gdb_start.sh ./build/bin/nvim'

debug: dbg-start dbg-attach
```

Here `gdb_start.sh` includes `gdb` commands to be called when the debugger starts. It needs to attach to the server started by the `dbg-start` rule. For example:

```
target remote localhost:6666
br main
```
