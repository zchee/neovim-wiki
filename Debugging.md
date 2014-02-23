# Debugging neovim
**THIS PAGE NEEDS ATTENTION**

## GNU/Linux
### Terminal using `gdb`
Use two terminals, one for the debugging session, and one for the neovim instance that will be debugged.
In the terminal for `neovim`, start a `gdbserver` instance on a specific port like this:

`gdbserver :666 build/vim`

This will start a remote debugging session for the binary `build/vim` on port `666`.

You then need to attach to this debugging session in the other terminal:

`gdb build/vim`

Once you entered `gdb`, you need to attach to the remote session:

`target remote localhost:666`

You are now attached to the remote debugging session. 
Try setting a breakpoint and start the application:

`br main` to set the breakpoint.

`c` to continue running the application

You can now step through source, and you'll see the results in the other window.

### Tmux
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