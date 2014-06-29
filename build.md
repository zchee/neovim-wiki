# Building Neovim

If you just pulled the Neovim source and want to get a working `nvim` binary,

    make

pulls down third-party dependencies (such as libuv and luajit) into `.deps/`, and builds them. If you're missing a dependency such as `libtool`, the configure script will let you know, then you try `make` again.  

Now that you have dependencies, you can try other build targets. Some suggestions are below.

### Run the legacy integration tests

    make test

### Run the unit tests

    make unittest

### Build a "release" build (optimized, NDEBUG)

    rm -rf build/ ; make clean && make CMAKE_BUILD_TYPE=MinSizeRel

`MinSizeRel` is CMake jargon for "minimum-sized release".  `Release` and `RelWithDebInfo` are also choices.

Alternative:

    rm -rf build/ ; make cmake CFLAGS='-Wno-error -DNDEBUG -O3 -U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=1' && make

- `-U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=1` is required because of [#223](https://github.com/neovim/neovim/issues/223).
- To see the full build output (including flags send to the compiler by make/CMake), change the `make` step to `VERBOSE=1 make`

### Custom Makefile 
You can customize the build process locally on your machine by creating `local.mk` which is referenced at the top of the main `Makefile` (and listed in `.gitignore`). **A new target in `local.mk` overrides the default make-target.**

Here's a sample `local.mk` which adds a target to force a rebuild but *does not* override the default-target:
```make
all:

rebuild:
	rm -rf build && make
```