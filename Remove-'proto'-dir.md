### Done! (this task was masterfully completed by @scott-linder at #137)

Vim uses a single global header(vim.h) that is included in every module and includes all other headers. This is bad for documentation(no obvious way of knowing the dependencies of a module) and incremental building(changing any header file will cause every module to be rebuilt)

If you want to help, any effort in that direction will be appreciated. The simplest way I found to do this is by replacing every file in the 'proto' directory by a proper header in the 'src' directory. 

For an example, here are the steps to remove 'buffer.pro' from the 'proto' directory

- move src/proto/buffer.pro to src/buffer.h
- wrap buffer.h into an include guard (NEOVIM_BUFFER_H)
- include "buffer.h" on the top of every file that fails to compile

When sending a PR, use a title like this: 'Replace buffer.pro by buffer.h'

If some scripting master think they can do this automatically in one single step, post a comment in the issue so others won't waste their time.


