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

Neovim can be installed using the PKGBUILD [`neovim-git`](https://aur.archlinux.org/packages/neovim-git), available on the [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository).

For installing the Python modules, you have two alternatives:

 * Use the [`python2-neovim`](https://aur.archlinux.org/packages/python2-neovim) and [`python-neovim`](https://aur.archlinux.org/packages/python-neovim) PKGBUILDs.
 * Install `pip` and follow the instructions at [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html):

```
sudo pacman -S python-pip python2-pip
```

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

## Android

[Termux on the Google Play store](https://play.google.com/store/apps/details?id=com.termux) offers a Neovim package.

## Windows

Windows support is (currently) experimental. To try it out, you need `nvim.exe` and a front-end such as Neovim-QT.

1. Go to https://ci.appveyor.com/project/equalsraf/neovim/branch/tb-mingw
    - Click the `Win64` build (near the bottom, with this label: `Environment: GENERATOR=Visual Studio 14 Win64, DEPS_PATH=deps64`).
    - View the _Artifacts_ tab.
    - Download `Neovim.zip`.
    - Unzip.
2. Download the latest [Neovim-QT build](https://github.com/equalsraf/neovim-qt/releases).
    - Unzip.
3. Copy `nvim.exe` into `neovim-qt/`.
4. Copy `share/nvim/runtime/*` (the _contents of_ `runtime/`) into `neovim-qt/`.
5. Double-click `nvim-qt.exe`

# Install from source

- _Note:_ To easily **uninstall** after building from source, you should install to a _custom location_ [as explained below](#install-to-custom-location).

Instead of using a pre-built package, you can build Neovim from source. This is usually easy, just make sure you have the [prerequisites](Building-Neovim#build-prerequisites). Then run:

    make
    sudo make install

That's it. By default, that installs to the standard software location for your operation system (`/usr/local`, `C:/Program Files`, etc.). To choose a different location, see below.

- Alternatively, you can run `build/bin/nvim` directly. Just run `make` (instead of `make install`). Then run this command in `nvim` itself: `:helptags $VIMRUNTIME/doc`

## Install to custom location

To install Neovim to a custom directory, set `CMAKE_INSTALL_PREFIX` in the build command:

    rm -r build/
    make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=$HOME/neovim"
    make install
    export PATH="$HOME/neovim/bin:$PATH"

_Note:_ The `rm -r build/` step above is needed if you already built Neovim before, otherwise the install location will be the same as before.

## Uninstall a source build

To uninstall Neovim, just delete the `CMAKE_INSTALL_PREFIX` directory that you specified in the [_Install to custom location_](#install-to-custom-location) section above.

See [Building Neovim](Building-Neovim) for more options. See [Troubleshooting](Troubleshooting) if you encounter [build](Troubleshooting#build-issues) or [installation errors](Troubleshooting#installation-issues).