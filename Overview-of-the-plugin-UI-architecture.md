(The features described here are not all implemented)

The msgpack-rpc API allow clients to connect and interact with a running
Neovim instance. Here are some of the things that can be acomplished by clients:

- Execute any vim command
- Evaluate vimscript expressions
- Manipulate buffers, windows and tabpages
- Receive/handle editor events

On top of that, the remote API has been designed for easy extensibility, so there
will always be new possibilities.

It's possible to test the current API interactively using the python REPL and
the [client library](https://github.com/neovim/python-client), but that isn't
very useful for extending the editor. Normally a Neovim plugin will have the
following pseudo code running:

```
while true
    handle(next_vim_event())
```

If you think about it, it's pretty much how vim plugins currently work: They
register autocommands to be executed whenever something interesting happen. The
difference is that Neovim can also propagate events to other processes and
receive commands asynchronously, and this opens some interesting possibilities
for plugins:

- They can be written in any programming language.
- They are sandboxed so there's less chance of the editor crashing due to bugs.
- They can perform background work without blocking the editor

#### UI programs

UIs will be pretty much like other plugins, except that they work as a bridge
between the user and the editor. Here's the pseudo code of a UI program:

```
while true
    handle(next_vim_or_user_event())
```

It's almost the same as a non-UI plugin, but they also have to listen
for user events(keypresses, mouse clicks, etc) and translate these to the
connected Neovim instance, which in turn will emit 'redraw' events to be
propagated back to the user.
