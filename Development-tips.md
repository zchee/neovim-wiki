## Building Neovim

See the [Building Neovim](Building-Neovim) page.

## Navigating the code

- The `contrib/` folder contains a [YouCompleteMe configuration](https://github.com/neovim/neovim/tree/master/contrib/YouCompleteMe) tailored to Neovim.

## Code linting

If you are using [Syntastic][syntastic], you can use https://gist.github.com/gilligan/9326904 to add `clint.py` as a checker for C files. Note that `clint.py` needs to be in your `PATH` and that you will have to modify `g:syntastic_c_checkers`, otherwise it will default to GCC or make.

See [Syntastic's documentation][syntastic-docs] for information.

## Experimenting with the API

You can write a simple shell that grabs the API metadata and allows you to send commands to Neovim:

https://github.com/splinterofchaos/neovim-cpp-client-experiment/blob/master/src/vim-shell.cpp

## Debugging

### Core dumps

Core dumps are [disabled  by default on Ubuntu](http://stackoverflow.com/a/18368068/152142), OS X, CentOS and others. Run:

    ulimit -c unlimited

to enable core dumping. If you then reproduce a segfault in `nvim`, it will "dump core". Typically this means a `core` file will appear in the current directory (or check `/var/log/apport.log` to see where it was written). You can then get a backtrace from the `core` with:

    gdb -q -n -ex bt -batch ./build/bin/nvim core > backtrace.txt

### Using `lldb` to step through unit tests

```
lldb .deps/usr/bin/luajit -- .deps/usr/bin/busted --lpath="./build/?.lua" test/unit/
```

### Using `gdb` (quick start)

To attach to a running `nvim` process with a pid of 1234:

    gdb build/bin/nvim 1234

The `gdb` interactive prompt will appear. At any time you can:

- `break foo` to set a breakpoint on the `foo()` function
- `n` to **step over** the next statement
    - `<Enter>` to repeat the last command
- `s` to **step into** the next statement
- `c` to **continue**
- `finish` to **step out** of the current function
- `p zub` to print the value of `zub` 
- `bt` to see a **backtrace** (callstack) from the current location
- `CTRL-x CTRL-a` to **show a TUI view of the source file** in the current debugging context. This can be extremely useful as it avoids the need for a gdb "frontend".
    - `<up>` and `<down>` to scroll the source file view

### Using `gdbserver`

You may want to connect multiple `gdb` clients to the same running `nvim` process, or you may want to connect to a remote `nvim` process with a local `gdb`. Using `gdbserver`, you can attach to a single process and control it from multiple `gdb` clients. 

Open a terminal and start `gdbserver` attached to `nvim` like this:

    gdbserver :6666 build/bin/nvim

`gdbserver` is now listening on port 6666. You then need to attach to this debugging session in another terminal:

    gdb build/bin/nvim

Once you've entered `gdb`, you need to attach to the remote session:

    target remote localhost:6666

### Using `gdbserver` in `tmux`

Consider using a [custom makefile](Building-Neovim#custom-makefile) to quickly start debugging sessions using the `gdbserver` method mentioned above. This example will create the debugging session when you type `make debug`.

```make
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

[syntastic]: https://github.com/scrooloose/syntastic
[syntastic-docs]: https://raw.githubusercontent.com/scrooloose/syntastic/master/doc/syntastic.txt