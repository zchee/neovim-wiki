This document gives an overview of how we'll be porting vim to run on top of libuv, which will be the first major step taken by neovim.

Vim has some functions for talking to the OS. These are the mch_* functions defined in [src/os_unix.c](https://github.com/neovim/neovim/blob/master/src/nvim/os_unix.c) (and in many other OS-specific files that were removed before the initial import). Most of the OS interaction is done using these functions, so porting vim for libuv will mostly be a job of reimplementing those functions into a new 'os' module (which lives in the 'os' subdirectory). It is also important  that we modify any code that makes system calls directly (I've seen a few of those) to use this module instead.

Some functions were already ported by @rjw57 in his [low hanging fruit PR](https://github.com/neovim/neovim/pull/115), anyone interested in helping might wanna start by reading it.

Since vim is completely dependent on blocking I/O, most of the functions will be implemented using a combination of mutexes and condition variables, with a background thread doing the actual I/O (this is the thread that runs libuv event loop and watchers). In some cases it might not be necessary to use a background thread as shown by @rjw57 in his PR.

User input reading (implemented mostly by mch_inchar) was ported to libuv in [#395](https://github.com/neovim/neovim/pull/395).

Everyone is encouraged to start a similar topic branch and try to port a function or two from `os_unix.c`, but create an issue with a relevant name so others will know that you are working on it. For example, let's say you want to port the function `mch_can_exe`, create an issue named 'libuv - porting mch_can_exe'. Feel free to send PR if all tests pass.

Try to split functions in `os_unix.h` into "categories" to avoid very big files. For example, functions that mess with filesystem should probably go into `os/fs.c`.

Avoid messing with any code that checks or uses signals (eg: those scattered `got_int` checks) because signal handling will be completely refactored.