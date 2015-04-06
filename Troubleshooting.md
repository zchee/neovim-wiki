## Build related issues

If you run into an error not explained here and manage to resolve it, feel free to add it below!

### General build issues

Run `make distclean && make` to rule out a stale build environment causing the failure.

### Neovim is slow

Make sure you're running an optimized build of `nvim`. To check this, run this:

    nvim --version | grep 'Build type'

This should yield one of the following:

```
Build type: RelWithDebInfo
Build type: MinSizeRel
Build type: Release
```

If it yields `Build type: Debug`, then see (Building-Neovim#optimized-builds)[Building-Neovim#optimized-builds]. If you're using a third-party package, please inform the maintainer.

### CMake errors

`configure_file Problem configuring file`
- This is probably a permissions issue, which can happen if you run `sudo make` and then later try an unprivileged `make`. To fix this, run `rm -rf build` and try again.

### Lua packages

The Lua packages required by the build process should be automatically installed by [LuaRocks](http://luarocks.org/) (invoked by CMake automatically), but sometimes this will fail. Generally, this means either:

- The LuaRocks servers are down.
- The program `unzip` isn't found. If this is the case, LuaRocks will report something like this: `Warning: Failed searching manifest: Failed loading manifest: Failed extracting manifest file`.

To avoid the first error, a LuaRocks mirror can be used:

```
cat >> .deps/usr/etc/luarocks/config-5.1.lua << "EOF"
rocks_servers={ 
  "http://luarocks.giga.puc-rio.br/" 
}
EOF
make cmake
```

Failing the above, you can always try installing the following packages manually:

- [LPeg](http://www.inf.puc-rio.br/~roberto/lpeg/)
- [lua-MessagePack](http://fperrad.github.io/lua-MessagePack/)
- [busted](http://olivinelabs.com/busted/) (required for running tests, e.g., `make test`)

Keep in mind that some of those packages have their own dependencies which also have to be installed, and the version you install hasn't necessarily been tested to work with Neovim.