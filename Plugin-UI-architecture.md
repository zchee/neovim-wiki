(The features described here are not all implemented)

A contributing factor to legacy Vim's huge codebase is its explicit support for
dozens of widget toolkits for GUI interfaces. Neovim avoids that by delegating
GUI implementation to external clients. The client(s) control the Neovim `nvim`
process via a msgpack-rpc API, which allows them to:

- Execute any vim command
- Evaluate vimscript expressions
- Manipulate buffers, windows and tabs
- Receive/handle editor events

On top of that, the remote API has been designed for easy extensibility, so there
will always be new possibilities. 

**A Neovim plugin is any program that talks to `nvim` through the remote API** (which can be reached via any arbitrary transport mechanism: TCP socket, named pipe, stdin/stdout, ...).

It's possible to test the current API interactively using the python REPL and
the [client library](https://github.com/neovim/python-client), but that isn't
very useful for extending the editor. A typical Neovim plugin will have the
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
    - Modern GUIs written in high-level languages that integrate better
      with the operating system (e.g., C#/WPF on Windows or Ruby/Cocoa on OS X).
- They are sandboxed so there's less chance of the editor (server) crashing due to bugs.
- They can perform background work without blocking the editor
- They can can emit **custom events** that may be handled directly by
  GUIs (enables implementation of advanced features such as Sublime's minimap).
- Multiple remote GUIs can attach/detach to share editing sessions.
- Simplified headless testing.
- Embedding the editor into other programs. In fact, a GUI can be seen as a
  program that embeds neovim.

#### UI programs

UIs are plugins that work as a bridge between the user and the editor. 
Here's pseudo-code of a UI program:

```
while true
    handle(next_vim_or_user_event())
```

It's almost the same as a non-UI plugin, except they must also listen
for user events (keypresses, mouse clicks, etc) and translate these to the
connected Neovim instance, which then emits 'redraw' events back to the user.

Here's a sample process tree:

```
Neovim <------ GUI 1 (attach/detach to running instances using tcp sockets)
  |  ^
  |  `--------GUI 2 (sharing the same session with GUI 1)
   `--> Plugin 1
  |
   `--> Plugin 2
  |
   `--> Plugin 3
```

Hypothetical GUI session:

```js
gui -> vim: {"id": 1, "method": "initClient", 
             "params": {"size": {"rows": 20, "columns": 25}}}
vim -> gui: {"id": 1, "result": {"clientId": 1}}
vim -> gui: {"method": "redraw", 
             "params": {"clientId": 1, "lines": {"5": "Welcome to neovim!"}}}
gui -> vim: {"id": 2, "method": "keyPress", 
             "params": {"keys": ["H", "e", "l", "l", "o"]}}
vim -> gui: {"method": "redraw", 
             "params": {"clientId": 1, "lines": {"1": "Hello", "5": ""}}}
```
