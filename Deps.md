Dependencies
============

Forks
=====

For some dependencies we maintain temporary "forks", which are simply private branches with a few extra patches, while we wait for the upstream project to merge the patches. This is done instead of maintaining the patches as (fragile) CMake `PATCH_COMMAND` steps.

* For Windows OS some of these patches are required. 
* For all other cases, Nvim builds against and supports both the "vanilla" dependency (without Nvim's patches) and typically much older versions.

In all cases the Nvim patches live on the `nvim` branch of each forked repo. 

The complete list of these forked dependencies is as follows:

* https://github.com/neovim/libuv
	* Compare `nvim` branch to upstream: https://github.com/libuv/libuv/compare/v1.x...neovim:nvim
* https://github.com/neovim/unibilium
	* Compare `nvim` branch to upstream: 
* https://github.com/neovim/libvterm
	* Compare `nvim` branch to upstream: https://github.com/neovim/libvterm/compare/3f62ac6b7bdffda39d68f723fb1806dfd6d6382d..nvim
* https://github.com/neovim/libtermkey
	* Compare `nvim` branch to upstream: 
