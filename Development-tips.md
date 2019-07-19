## Navigating the code

- Browse **[Neovim on SourceGraph](https://sourcegraph.com/github.com/neovim/neovim)**
- Install **[universal-ctags](https://github.com/universal-ctags/ctags).** "Exuberant ctags" (the typical `ctags` binary provided by your distro) is unmaintained and won't recognize many function signatures in Neovim source.
- The `contrib` folder contains a [YouCompleteMe configuration](https://github.com/neovim/neovim/tree/master/contrib/YouCompleteMe) for Neovim.

## Other tools

- [hererocks](https://github.com/mpeterv/hererocks) (very similar to Python's `virtualenv`) is useful for installing Luarocks, LuaJIT, and Lua:
  ```
  curl -LO https://raw.githubusercontent.com/mpeterv/hererocks/latest/hererocks.py
  chmod u+x hererocks.py
  # Install LuaJit and LuaRocks 3.0 to the "myenv" directory.
  ./hererocks.py myenv --luajit latest -r3.0
  ```
- [croissant](https://github.com/giann/croissant) is a Lua REPL

## Experimenting with the API

You can write a simple shell that grabs the API metadata and allows you to send commands to Neovim:

https://github.com/splinterofchaos/neovim-cpp-client-experiment/blob/master/src/vim-shell.cpp

## Debugging

### Backtrace (Linux)

Core dumps are [disabled  by default on Ubuntu](http://stackoverflow.com/a/18368068/152142), CentOS and others. To enable core dumps:

    ulimit -c unlimited

On systemd-based systems getting a backtrace is as easy as:

    coredumpctl -1 gdb

It's an optional tool, so you may need to install it:

    sudo apt install systemd-coredump

The **full backtrace** is most useful, send us the `bt.txt` file:

    2>&1 coredumpctl -1 gdb | tee -a bt.txt
    thread apply all bt full

**On older systems** a `core` file will appear in the current directory. To get a backtrace from the `core` file:

    gdb build/bin/nvim core 2>&1 | tee backtrace.txt
    thread apply all bt full


### Backtrace (macOS / OSX)

If `nvim` crashes on macOS, you can see the backtrace in Console.app (under "User Diagnostic Reports").

    open -a Console

You may also want to [enable core dumps on macOS](https://developer.apple.com/library/mac/technotes/tn2124/_index.html#//apple_ref/doc/uid/DTS10003391-CH1-SECCOREDUMPS). The `/cores/` directory must exist and be writable.

### Using `gdb` to step through functional tests

Use `TEST_TAG` to run tests matching busted tags (of the form `#foo` e.g. `it("test #foo ...", ...)`):

```
GDB=1 TEST_TAG=foo make functionaltest
```

Then, in another terminal:

```
gdb build/bin/nvim
target remote localhost:7777
```

- See also [test/functional/helpers.lua](https://github.com/neovim/neovim/blob/3098b18a2b63a841351f6d5e3697cb69db3035ef/test/functional/helpers.lua#L38-L44).

### Using `lldb` to step through unit tests

```
lldb .deps/usr/bin/luajit -- .deps/usr/bin/busted --lpath="./build/?.lua" test/unit/
```

### Using `gdb`

To attach to a running `nvim` process with a pid of 1234:

    gdb -tui -p 1234 build/bin/nvim

The `gdb` interactive prompt will appear. At any time you can:

- `break foo` to set a breakpoint on the `foo()` function
- `n` to **step over** the next statement
    - `<Enter>` to repeat the last command
- `s` to **step into** the next statement
- `c` to **continue**
- `finish` to **step out** of the current function
- `p zub` to print the value of `zub` 
- `bt` to see a **backtrace** (callstack) from the current location
- `CTRL-x CTRL-a` or `tui enable` to **show a TUI view of the source file** in the current debugging context. This can be extremely useful as it avoids the need for a gdb "frontend".
    - `<up>` and `<down>` to scroll the source file view

#### gdb "reverse debugging"

- `set record full insn-number-max unlimited`
- `continue` for a bit (at least until `main()` is executed
- `record`
- provoke the bug, then use `revert-next`, `reverse-step`, etc. to rewind the debugger

### Using `gdbserver`

You may want to connect multiple `gdb` clients to the same running `nvim` process, or you may want to connect to a remote `nvim` process with a local `gdb`. Using `gdbserver`, you can attach to a single process and control it from multiple `gdb` clients. 

Open a terminal and start `gdbserver` attached to `nvim` like this:

    gdbserver :6666 build/bin/nvim 2> gdbserver.log

`gdbserver` is now listening on port 6666. You then need to attach to this debugging session in another terminal:

    gdb build/bin/nvim

Once you've entered `gdb`, you need to attach to the remote session:

    target remote localhost:6666

In case gdbserver puts the TUI as a background process, the TUI can become unable to read input from pty (and receives SIGTTIN signal) and/or output data (SIGTTOU signal). To force the TUI as the foreground process, you can add

    signal (SIGTTOU, SIG_IGN);
    if (!tcsetpgrp(data->input.in_fd, getpid())) {
        perror("tcsetpgrp failed");
    }

to tui.c:terminfo_start.

### Using `gdbserver` in `tmux`

Consider using a [custom makefile](Building-Neovim#custom-makefile) to quickly start debugging sessions using the `gdbserver` method mentioned above. This example `local.mk` will create the debugging session when you type `make debug`.

```make
.PHONY: dbg-start dbg-attach debug build

build:
	@$(MAKE) nvim

dbg-start: build
	@tmux new-window -n 'dbg-neovim' 'gdbserver :6666 ./build/bin/nvim -D'

dbg-attach:
	@tmux new-window -n 'dbg-cgdb' 'cgdb -x gdb_start.sh ./build/bin/nvim'

debug: dbg-start dbg-attach
```

Here `gdb_start.sh` includes `gdb` commands to be called when the debugger starts. It needs to attach to the server started by the `dbg-start` rule. For example:

```
target remote localhost:6666
br main
```

### Log file location

Nvim's low-level logs are written to `~/.local/share/nvim/log` (usually; see `:help $NVIM_LOG_FILE`).
Debug builds write INFO-level messages to this log file. You can specify the location with the `$NVIM_LOG_FILE` environment variable. Non-debug builds only log ERROR-level messages.


[syntastic]: https://github.com/scrooloose/syntastic
[syntastic-docs]: https://raw.githubusercontent.com/scrooloose/syntastic/master/doc/syntastic.txt