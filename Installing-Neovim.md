**Before upgrading to a new version, ALWAYS check the [Following HEAD](Following-HEAD) page.**

# Install from package

If you're on one of the following systems, you can get Neovim right away!
If not, you can still [install Neovim manually](#install-from-source).

Note that the Neovim binary to run is called `nvim`, not `neovim`.

## [Homebrew](http://brew.sh) (OS X) / [Linuxbrew](http://brew.sh/linuxbrew/) (Linux)

See the [README of `neovim/homebrew-neovim`](https://github.com/neovim/homebrew-neovim/blob/master/README.md) for installation instructions.

## Ubuntu

Neovim has been added to a [Personal Package Archive](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable) which allows you to install it using `apt-get` on Ubuntu [12.04 and later](https://wiki.ubuntu.com/Releases).

To be able to use **add-apt-repository** you may need to install software-properties-common:

    sudo apt-get install software-properties-common

Run the following commands:

    sudo add-apt-repository ppa:neovim-ppa/unstable
    sudo apt-get update
    sudo apt-get install neovim

Prerequisites for the Python modules:

    sudo apt-get install python-dev python-pip python3-dev python3-pip

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

If you want to use Neovim for some (or all) of the editor alternatives, use the following commands:

    sudo update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60
    sudo update-alternatives --config vi
    sudo update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60
    sudo update-alternatives --config vim
    sudo update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
    sudo update-alternatives --config editor

## Arch Linux

Neovim can be installed from the community repository:

    sudo pacman -Syu neovim

Alternatively, Neovim can be also installed using the PKGBUILD [`neovim-git`](https://aur.archlinux.org/packages/neovim-git), available on the [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository).

For installing the Python modules, you have two options:

 * Install the packages from the community repository:

        sudo pacman -S python2-neovim python-neovim

 * Install `pip` and follow the instructions at [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html):

        sudo pacman -S python-pip python2-pip

## CRUX

A CRUX port is available under [`6c37/neovim`](https://github.com/6c37/crux-ports-git), along with ports for other dependencies of Neovim.

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

## Gentoo Linux

A snapshot ebuild is now available in Gentoo's official portage repository:

    emerge -a app-editors/neovim

A "live" ebuild can be found in [yngwin's developer overlay](http://cgit.gentooexperimental.org/dev/yngwin.git/tree/app-editors/neovim).

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

## Exherbo Linux

A "scm" exheres is currently available in repository `::exony`:

    cave resolve app-editors/neovim::exony

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

## Fedora 21/22
 
http://copr.fedoraproject.org/coprs/dperson/neovim/

    dnf -y install dnf-plugins-core
    dnf -y copr enable dperson/neovim
    dnf -y install neovim

It's built using the [Copr](https://copr.fedoraproject.org/) automated build system, which is unsupported. There's no guarantee of how long your package will be available after the build finishes.

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

## Slackware

See [neovim on SlackBuilds](http://slackbuilds.org/apps/neovim/).

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

## NixOS

Neovim can be installed from the [unstable channel](http://nixos.org/nixos/manual/#sec-upgrading) using the following command:

    nix-env -iA neovim

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

## Freebsd

Neovim can be installed [from the ports tree](https://www.freshports.org/editors/neovim/):

    cd /usr/ports/editors/neovim/ && make install clean

Or installed using [`pkg(8)`](https://www.freebsd.org/cgi/man.cgi?query=pkg&sektion=8&apropos=0&manpath=FreeBSD+10.2-RELEASE):

    pkg install neovim

## Android

[Termux on the Google Play store](https://play.google.com/store/apps/details?id=com.termux) offers a Neovim package.

## Windows

Windows support is (currently) experimental. To try it out, you need `nvim.exe` and a front-end such as Neovim-QT.

1. Go to https://ci.appveyor.com/project/equalsraf/neovim/branch/tb-mingw
    - Click the `Win64` build (near the bottom, with this label: `Environment: GENERATOR=Visual Studio 14 Win64, DEPS_PATH=deps64`).
    - View the _Artifacts_ tab.
    - Download `Neovim.zip`.
2. Download and unzip the latest [Neovim-QT build](https://github.com/equalsraf/neovim-qt/releases).
3. Copy `nvim.exe` into `neovim-qt/`. 
4. Copy `share/nvim/runtime/*` (the _contents of_ `runtime/`) into `neovim-qt/`.
5. Double-click `nvim-qt.exe`

### Symlinking instead of copying Neovim files into Neovim-QT

This is an alternative way of installing if you prefer to keep the Neovim and Neovim-QT files separated for easier upgrading. This replaces step 3 and 4 in the above instruction.

Run `cmd.exe` as an administrator, then execute the following commands in order:
```
cd C:\Program Files\Neovim-QT
mklink nvim.exe ..\Neovim\bin\nvim.exe
for %f in (..\Neovim\share\nvim\runtime\*) do mklink "%~nxf" "..\Neovim\share\nvim\runtime\%~nxf"
for /d %f in (..\Neovim\share\nvim\runtime\*) do mklink /d "%~nxf" "..\Neovim\share\nvim\runtime\%~nxf"
```

### .vimrc file in Windows

If you already have Vim installed you can copy or symlink `%userprofile%\_vimrc` to `%userprofile%\AppData\Local\nvim\init.vim` to get the same settings as you already use in Vim.

# Install from source

Instead of using a pre-built package, you can build and install Neovim from source.

See [Building-Neovim](https://github.com/neovim/neovim/wiki/Building-Neovim) first; once that's done 

    make
    sudo make install

That installs to the standard software location for your operation system (`/usr/local`, `C:/Program Files`, etc.). To choose a different location, see below.

- Alternatively, you can run `build/bin/nvim` directly. Just run `make` (instead of `make install`). Then run this command in `nvim` itself: `:helptags $VIMRUNTIME/doc`

## Install to custom location

To install Neovim to a custom directory, set `CMAKE_INSTALL_PREFIX` in the build command:

    rm -r build/
    make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=$HOME/neovim"
    make install
    export PATH="$HOME/neovim/bin:$PATH"

Note that the `rm -r build/` step above is needed if you've built Neovim before, as the install location will be the same as before since CMake caches build information

## Uninstall a source build

To uninstall Neovim, just delete the `CMAKE_INSTALL_PREFIX` directory that you specified in the [_Install to custom location_](#install-to-custom-location) section above.

See [Building Neovim](Building-Neovim) for more options. See [Troubleshooting](Troubleshooting) if you encounter [build](Troubleshooting#build-issues) or [installation errors](Troubleshooting#installation-issues).