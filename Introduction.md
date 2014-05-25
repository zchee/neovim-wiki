Vim is a powerful text editor with a big community that is constantly
growing.  Even though the editor is about two decades old, people still extend
and want to improve it, mostly using vimscript or one of the supported scripting
languages.

## Problem

Over its more than 20 years of life, vim has accumulated about 300k lines of
scary C89 code that very few people understand or have the guts to mess with.

Another issue is that as the only person responsible for maintaining vim's big
codebase, Bram Moolenaar has to be extra careful before accepting patches,
because once merged, the new code will be his responsibility.

These problems make it very difficult to have new features and bug fixes merged
into the core. Vim just can't keep up with the development speed of its plugin
ecosystem.

## Solution

Neovim is a project that seeks to aggressively refactor vim source code in order
to achieve the following goals:

- Simplify maintenance to improve the speed that bug fixes and features get
  merged.
- Split the work between multiple developers.
- Enable the implementation of new/modern user interfaces without any
  modifications to the core source.
- Improve the extensibility power with a new plugin architecture based on
  coprocesses. Plugins will be written in any programming language without
  any explicit support from the editor.

By achieving those goals new developers will soon join the community,
consequently improving the editor for all users.

It is important to emphasize that this is not a project to rewrite vim from
scratch or transform it into an IDE (though the new features provided will
enable IDE-like distributions of the editor). The changes implemented here
should have little impact on vim's editing model or vimscript in general. Most
vimscript plugins should continue to work normally.

The following topics contain brief explanations of the major changes (and
motivations) that will be performed in the first iteration:

* [Migrate to a CMake-based build](#build)
* [Legacy support and compile-time features](#legacy)
* [Platform-specific code](#platform)
* [New plugin architecture](#plugins)
* [New GUI architecture](#gui)
* [Development on GitHub](#development)

<a name="build"></a>
### Migrate to a CMake-based build

The source tree has dozens (if not hundreds) of files dedicated to building vim
with on various platforms with different configurations, and many of these files
look abandoned or outdated. Most users don't care about selecting individual
features and just compile using `--with-features=huge`, which still generates an
executable that is small enough even for lightweight systems by today's
standards.

All those files will be removed and vim will be built using [CMake][], a modern
build system that generates build scripts for the most relevant platforms.

[CMake]: http://cmake.org/

<a name="legacy"></a>
### Legacy support and compile-time features

Vim has a significant amount of code dedicated to supporting legacy systems and
compilers. All that code increases the maintenance burden and will be removed.

Most optional features will no longer be optional (see above), with the
exception of some broken and useless features (e.g. NetBeans and Sun WorkShop
integration) which will be removed permanently. Vi emulation will also be
removed (setting `nocompatible` will be a no-op).

These changes won't affect most users. Those that only have a C89 compiler
installed or use vim on legacy systems such as Amiga, BeOS or MS-DOS will
have two options:

- Upgrade their software
- Continue using vim

<a name="platform"></a>
### Platform-specific code

Most of the platform-specific code will be removed and [libuv][] will be used to
handle system differences.

libuv is a modern multi-platform library with functions to perform common system
tasks, and supports most unixes and windows, so the vast majority of vim's
community will be covered.

[libuv]: https://github.com/joyent/libuv

<a name="plugins"></a>
### New plugin architecture

All code supporting embedded scripting language interpreters will be replaced by
a new plugin system that will support extensions written in any programming
language.

Compatibility layers will be provided for vim plugins written in some of the
currently supported scripting languages such as Python or Ruby. Most plugins
should work on neovim with little modifications, if any.

This is how the new plugin system will work:

- Plugins are long-running programs/jobs (coprocesses) that communicate with vim
  through stdin/stdout using msgpack-rpc or json-rpc.
- Vim will discover and run these programs at startup, keeping two-way
  communication channels with each plugin through its lifetime.
- Plugins will be able to listen to events and send commands to vim
  asynchronously.

This system will be built on top of a job control mechanism similar to the one
implemented by the [job control patch][].

Here's an idea of how a plugin session might work using [json-rpc][] (json-rpc version omitted):

```js
plugin -> neovim: {"id": 1, "method": "listenEvent", "params": {"eventName": "keyPressed"}}
neovim -> plugin: {"id": 1, "result": true}
neovim -> plugin: {"method": "event", "params": {"name": "keyPressed", "eventArgs": {"keys": ["C"]}}}
neovim -> plugin: {"method": "event", "params": {"name": "keyPressed", "eventArgs": {"keys": ["Ctrl", "Space"]}}}
plugin -> neovim: {"id": 2, "method": "showPopup", "params": {"size": {"width": 10, "height": 2} "position": {"column": 2, "line": 3}, "items": ["Completion1", "Completion2"]}}
plugin -> neovim: {"id": 2, "result": true}}
```

That shows a hypothetical conversation between neovim and a completion plugin
which displays completions when the user presses Ctrl+Space. The above scheme
gives neovim near limitless extensibility and also improves stability as plugins
will be automatically isolated from the main executable.

This system can also easily emulate the current scripting language interfaces
to vim. For example, a plugin can emulate the Python interface by running
Python scripts sent by vim in its own context and by exposing a `vim` module
with an API matching the current one. Calls to the API would simply be
translated to json-rpc messages sent to vim.

[job control patch]: https://groups.google.com/forum/#!topic/vim_dev/QF7Bzh1YABU
[json-rpc]: http://www.jsonrpc.org/specification

<a name="development"></a>
### Development on GitHub

Development happens in the [Neovim GitHub organization][]; the code is
split across several repositories, unlike the current Vim source tree.

There are separate repositories for GUIs, plugins, runtime files (official
vimscript) and distributions. This lets the editor receive improvements much
faster, because the patches don't have to go through a single person for approval.

Travis CI is used for continuous integration, so pull requests are
automatically checked.

[Neovim GitHub organization]: https://github.com/neovim

