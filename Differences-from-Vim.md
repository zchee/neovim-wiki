## **IMPORTANT**

This page is only an addendum to [`:help vim-differences`](http://neovim.io/doc/user/vim_diff.html#vim-differences), which should be the first place to check.

## Features

* Neovim has a built-in terminal emulator, which can be accessed using `:term[inal]`. To exit terminal mode, press `<C-\><C-n>`. `:tmap` and `:tnoremap` can be used to create terminal mode mappings.
* Neovim always ships with all features, in contrast to Vim which may have certain features removed/added at compile-time. This is like if Vim's "HUGE" build was the only Vim release type (except Neovim is smaller than Vim's "HUGE" build).
* `:python` and `:python3` are always available (if your system has both Python 2 & 3) and may be used side-by-side in plugins. [#718](https://github.com/neovim/neovim/issues/718#issuecomment-47589739)
    * If `python` is available on your `$PATH`, and the [`neovim` python package](https://pypi.python.org/pypi/neovim/) is installed, Python plugins will work. You don't need to worry about [link-time details](https://github.com/Valloric/YouCompleteMe/issues/8#issuecomment-34374807) or [ABI incompatibilities](https://groups.google.com/d/msg/vim_use/l8TY2EiXNwk/A9Ef-ozbjKoJ).