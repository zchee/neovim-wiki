- Before upgrading to a new version, **always check [Following HEAD](Following-HEAD).**

---

- [Quick start](#quick-start)
- [Running tests](#running-tests)
- [Building](#building)
- [Windows / MSVC](#windows--msvc)
- [Localization](#localization)
- [Compiler options](#compiler-options)
- [Xcode and MSVC project files](#xcode-and-msvc-project-files)
- [Custom Makefile](#custom-makefile)
- [Third-party dependencies](#third-party-dependencies)
- [Build prerequisites](#build-prerequisites)

## Quick start

1. Verify that you have the [build prerequisites](#build-prerequisites) installed.
2. Clone [`neovim/neovim`](https://github.com/neovim/neovim).
    - If you want the **stable release**: `git checkout stable`
3. Build Neovim by running `make`. (On BSD use `gmake`. On Windows see [MSVC](#windows--msvc).)
    - Set `CMAKE_INSTALL_PREFIX` if you want to **install to a custom location**. See [Installing Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim#install-from-source).

Other notes:

- Third-party dependencies (libuv, LuaJIT, etc.) are downloaded automatically to `.deps/`. See [FAQ](FAQ#build-issues) if you have issues.
- If you plan to develop Neovim, install [ninja](https://ninja-build.org/) for faster builds. It will be used automatically.

Now that you have the dependencies, you can try other build targets, explained below.

## Running tests

See [test/README.md](https://github.com/neovim/neovim/blob/master/test/README.md)

## Building

_Just `make` in the root of the repo will download and build all the needed dependencies and put the `nvim` executable at `build/bin`. Without installing, you can run it like this: `VIMRUNTIME=runtime ./build/bin/nvim`._

The build type determines the level of used compiler optimisations and debug information:

- `Release`: Full compiler optimisations and no debug information. Expect the best performance from this build type. Often used by package maintainers.
- `Debug`: Full debug information; little optimisations. Use this for development to get meaningful output from debuggers like gdb or lldb. This is the default, if `CMAKE_BUILD_TYPE` is not specified.
- `RelWithDebInfo` ("Release With Debug Info"): Enables many optimisations and adds enough debug info so that when nvim ever crashes, you can still get a backtrace.

So, for a release build, just use:

```
make CMAKE_BUILD_TYPE=Release
```

Afterwards, the `nvim` executable can be found at `build/bin`. To verify the build type after compilation, run `./build/bin/nvim --version | grep ^Build`.

To install the executable to a certain location, use:

```
make CMAKE_INSTALL_PREFIX=$HOME/local/nvim install
```

Cmake, our main build sytem, caches a lot of things in `build/CMakeCache.txt`. If you ever want to change `CMAKE_BUILD_TYPE` or `CMAKE_INSTALL_PREFIX`, run `rm -rf build` first.

By default (`USE_BUNDLED=1`), Nvim downloads and statically links its needed dependencies. In order to be able to use a debugger on these libraries, you might want to compile them with debug informations as well:

```
make distclean
VERBOSE=1 DEBUG=1 make deps
```

(Here, `make distclean` is basically a shortcut for `rm -rf build .deps`.)

## Windows / MSVC

1. [Install Visual Studio](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community) (2017 or later) with the _Desktop development with C++_ workload.
    - On 32-bit Windows you need [this workaround].(https://developercommunity.visualstudio.com/content/problem/212989/ninja-binary-format.html)
1. Open the Neovim project. Visual Studio automatically starts the build...
1. **IMPORTANT:** Select `x86-Release` configuration instead of `x64-{Debug,Release}`.
    - You can build with the `x64-Release` configuration if `cmake -G "Visual Studio 15 2017 Win64"` is used to build the dependencies. But the Debug configurations will not work because certain dependencies need to be linked with release version of the C runtime.
1. If the build fails, it may be because VS started the build with `x64-{Debug,Release}` before you switched to `x86-Release`.
    - Right-click _CMakeLists.txt → Delete Cache_.
    - Right-click _CMakeLists.txt → Generate Cache_.

## Windows / CLion

1. Install [CLion](https://www.jetbrains.com/clion/).
1. Open the Neovim project in CLion.
1. Select _Build → nvim.exe_.


## Localization

#### Localization build

A normal build will create `.mo` files in `build/src/nvim/po`.

* If you see `msgfmt: command not found`, you need to install [`gettext`](http://en.wikipedia.org/wiki/Gettext). On most systems the package is just called `gettext`.

#### Localization check

To check the translations for `$LANG`, run `make -C build check-po-$LANG`. Examples:

    make -C build check-po-de
    make -C build check-po-pt_BR

- Use `ninja` instead of `make` if applicable.
- `check-po-$LANG` generates a detailed report in `./build/src/nvim/po/check-${LANG}.log`. 
  (The report is generated by `nvim`, not by `msgfmt`.)

#### Localization update

To update the `src/nvim/po/$LANG.po` file with the latest strings, run the following:

    make -C build update-po-$LANG

- Replace `make` with `ninja` if applicable.
- **Note:** run `src/nvim/po/cleanup.vim` after updating.

## Compiler options

To see the chain of includes, use the `-H` option ([#918](https://github.com/neovim/neovim/issues/918)):

```
echo '#include "./src/nvim/buffer.h"' | \
> clang -I.deps/usr/include -Isrc -std=c99 -P -E -H - 2>&1 >/dev/null | \
> grep -v /usr/
```

- `grep -v /usr/` is used to filter out system header files
- `-save-temps` can be added as well to see expanded macros or commented assembly

## Xcode and MSVC project files

CMake has a `-G` option for exporting to multiple [project file formats](http://www.cmake.org/cmake/help/v2.8.8/cmake.html#section_Generators), such as Xcode and Visual Studio. 

For example, to use Xcode's static analysis GUI ([#167](https://github.com/neovim/neovim/issues/167#issuecomment-36136018)), you need to generate an Xcode project file from the Neovim makefile (where `neovim/` is the top-level Neovim source code directory containing the main `Makefile`):

    cmake -G Xcode neovim

then open the resulting project file in Xcode.

## Custom Makefile

You can customize the build process locally by creating a `local.mk`, which is referenced at the top of the main `Makefile`. It's listed in `.gitignore` so it can be used across branches. **A new target in `local.mk` overrides the default make-target.**

Here's a sample `local.mk` which adds a target to force a rebuild but *does not* override the default-target:

```make
all:

rebuild:
	rm -rf build
	make
```

## Third-party dependencies

Reference the **[Debian package](https://packages.debian.org/sid/source/neovim)** (or alternatively the [Homebrew formula](https://github.com/Homebrew/homebrew-core/blob/master/Formula/neovim.rb#L16-L27)) for the precise list of dependencies/versions.

To build the bundled dependencies using CMake:

```sh
mkdir .deps
cd .deps
cmake ../third-party
make
```

By default the libraries and headers are placed in `.deps/usr`. Now you can build Nvim:

```sh
mkdir build
cd build
cmake ..
make
```

### How to build without "bundled" dependencies

1. Install the dependencies manually. For example on Debian/Ubuntu:
   ```
   sudo apt install gperf libluajit-5.1-dev libunibilium-dev libmsgpack-dev libtermkey-dev libvterm-dev libjemalloc-dev lua5.1 lua-lpeg lua-mpack lua-bitop
   ```
2. Do the "CMake dance": create a `build` directory, switch to it and run CMake:
   ```
   mkdir build
   cd build
   cmake ..
   ```
3. Run `make`, `ninja`, or whatever build tool you [told CMake to generate for](#xcode-and-msvc-project-files).
   - Using `ninja` is strongly recommended.


## Build prerequisites

General requirements (see [#1469](https://github.com/neovim/neovim/issues/1469#issuecomment-63058312)):

- Clang or GCC version `4.4+`
- CMake version `2.8.12+`, built with TLS/SSL support
  - Optional: to get the latest CMake there are [installers](https://github.com/Kitware/CMake/releases) or a [Python package](https://pypi.org/project/cmake/) (`pip install cmake`)

Platform-specific requirements are listed below.

#### Ubuntu / Debian

    sudo apt-get install ninja-build gettext libtool libtool-bin autoconf automake cmake g++ pkg-config unzip

Note: `libtool-bin` is only required for Ubuntu 16.04/Debian Jessie and newer.

#### CentOS / RHEL / Fedora

If you're using CentOS/RHEL 6 you need at least autoconf version 2.69 for
compiling the libuv dependency. See https://github.com/joyent/libuv/issues/1158.

    sudo yum -y install ninja-build libtool autoconf automake cmake gcc gcc-c++ make pkgconfig unzip patch

#### openSUSE

    sudo zypper install ninja libtool autoconf automake cmake gcc-c++ gettext-tools

#### Arch Linux

    sudo pacman -S base-devel cmake unzip ninja

#### Nix or NixOS

Starting from nixos 18.03, the neovim binary resides in the `neovim-unwrapped` nix package (the `neovim` package being just a wrapper to setup runtime options like ruby/python support):

    cd path/to/neovim/src

Drop into nix shell to pull in the neovim dependencies

    nix-shell '<nixpkgs>' -A neovim-unwrapped

Configure and Build

```
cmakeConfigurePhase
buildPhase
```

Tests are not available by default because of some unfixed failures. You can enable them via adding this package in your overlay:
``` 
  neovim-dev = (super.pkgs.neovim-unwrapped.override  {
    doCheck=true;
  }).overrideAttrs(oa:{
    cmakeBuildType="debug";

    nativeBuildInputs = oa.nativeBuildInputs ++ [ self.pkgs.valgrind ];
    shellHook = ''
      export NVIM_PYTHON_LOG_LEVEL=DEBUG
      export NVIM_LOG_FILE=/tmp/log
      export VALGRIND_LOG="$PWD/valgrind.log"
    '';
  });
```
and replacing neovim-unwrapped by neovim-dev: `$ nix-shell '<nixpkgs>' -A neovim-dev`


#### FreeBSD

    sudo pkg install cmake gmake libtool sha automake pkgconf unzip wget gettext

If you get an error regarding a sha256sum mismatch, where
the actual sha256sum is `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`, then this is your issue (that's the sha256sum of an empty file). Also, make sure you have wget installed.
LuaRocks has bad interactions with cURL, at least under FreeBSD, and will die with
a PANIC in LuaJIT when trying to install a rock.

#### OpenBSD

```
doas pkg_add gmake cmake libtool unzip autoconf-2.69p2 automake-1.15p0
export AUTOCONF_VERSION=2.69
export AUTOMAKE_VERSION=1.15
```

For older versions of OpenBSD than 6.1, the `autoconf-2.69` and `automake-1.15` ports may have different `p` suffixes.

The build sometimes fails when using the top level Makefile, apparently due to some third-party component [#2445-comment](https://github.com/neovim/neovim/issues/2445#issuecomment-108124236). The following instructions use CMake

```
mkdir .deps
cd .deps
cmake ../third-party/
gmake
cd ..
mkdir build
cd build
cmake ..
gmake
```

#### macOS

* Install [Xcode](https://developer.apple.com/) and [Homebrew](http://brew.sh)
  or [MacPorts](http://www.macports.org)
* Install Xcode commandline tools `xcode-select --install`
* Install other dependencies:
  * via MacPorts:
    ```
    sudo port install ninja libtool autoconf automake cmake pkgconfig gettext
    ```
  * via Homebrew:
    ```
    brew install ninja libtool automake cmake pkg-config gettext
    ```
* If you see **wget certificate errors** (for macOS *before* version 10.10/Yosemite):
  * via MacPorts:
    ```
    sudo port install curl-ca-bundle
    echo CA_CERTIFICATE=/opt/local/share/curl/curl-ca-bundle.crt >> ~/.wgetrc
    ```
  * via Homebrew:
    ```
    brew install curl-ca-bundle
    echo CA_CERTIFICATE=$(brew --prefix curl-ca-bundle)/share/ca-bundle.crt >> ~/.wgetrc
    ```
* If you see `'stdio.h' file not found` 
    ```
    open /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg
    ```

##### Building for older macOS versions

To build for older macOS versions, e.g. for 10.13, on a newer macOS, you have to set the macOS deployment target

```
make CMAKE_BUILD_TYPE=Release MACOSX_DEPLOYMENT_TARGET=10.13 DEPS_CMAKE_FLAGS="-DCMAKE_CXX_COMPILER=$(xcrun -find c++)"
```

Note that if we do not explicitly set the C++ compiler, the compiler will not be found when the deployment target is set.

#### cygwin

Install all dependencies the normal way, then build neovim the normal way for a random CMake application (i.e. do not use the `Makefile` that automatically downloads and builds "bundled" dependencies)

The cygport repo contains cygport files (like APKBUILD, PKGBUILD, etc.) for all the dependencies not available in the cygwin distribution, and describes any special commands or arguments needed to build. the cygport definitions also try to describe the required dependencies for each one.
unless custom commands are provided, cygport just calls autogen/cmake, make, make install, etc. in a clean, consistent way.

https://github.com/cascent/neovim-cygwin was built on cygwin 2.9.0. Newer libuv should require slightly less patching and some ssp stuff changed in cygwin 2.10.0 so that might change things too when building neovim.


#### Windows / MSYS2

From the MSYS2 shell install these packages

```
pacman -S \
    mingw-w64-x86_64-{gcc,libtool,cmake,make,perl,python2,pkg-config,unibilium} \
    gperf
```

Now from the windows console (cmd.exe) setup the PATH and build

```cmd
set PATH=c:\msys64\mingw64\bin;%PATH%
set CC=gcc
```

Build using the `MinGW Makefiles` generator

```cmd
mkdir .deps
cd .deps
cmake  -G "MinGW Makefiles" ..\third-party\
mingw32-make
cd ..
mkdir build
cd build
cmake -G "MinGW Makefiles" -DGPERF_PRG="C:\msys64\usr\bin\gperf.exe" ..
mingw32-make
```

For 32bit builds adjust the package names and paths accordingly.