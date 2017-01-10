- Before upgrading to a new version, **always check [Following HEAD](Following-HEAD).**
- If you're wondering where to put your config (`vimrc`) see [here](https://github.com/neovim/neovim/wiki/FAQ#where-should-i-put-my-config-vimrc).
- To start Neovim, run `nvim` (not `neovim`).

# Install from package

Packages are listed below. (You can also [build Neovim from source](#install-from-source).)

## macOS / OS X

### VimR packages

The VimR project provides [bz2 archives](https://github.com/qvacua/vimr/releases) for macOS which include a pre-built `nvim` binary.

### [Homebrew](http://brew.sh) (OS X) / [Linuxbrew](http://linuxbrew.sh/) (Linux)

    brew install neovim/neovim/neovim

See the [neovim/homebrew-neovim README](https://github.com/neovim/homebrew-neovim/blob/master/README.md) for a complete reference.

### [Macports](https://www.macports.org/)

    sudo port selfupdate
    sudo port install neovim

## Debian

Neovim is in [Debian](https://packages.debian.org/search?keywords=neovim).

    sudo apt-get install neovim

Python (`:python`) support is also installable via the Debian package manager.

    sudo apt-get install python-neovim
    sudo apt-get install python3-neovim

## Ubuntu

Neovim has been added to a [Personal Package Archive](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable) which allows you to install it using `apt-get` on Ubuntu [12.04 and later](https://wiki.ubuntu.com/Releases).

To be able to use **add-apt-repository** you may need to install software-properties-common:

    sudo apt-get install software-properties-common

If you're using an older version Ubuntu you have to use:

    sudo apt-get install python-software-properties

Run the following commands:

    sudo add-apt-repository ppa:neovim-ppa/unstable
    sudo apt-get update
    sudo apt-get install neovim

Prerequisites for the Python modules:

    sudo apt-get install python-dev python-pip python3-dev python3-pip

If you're using an older version Ubuntu you have to use:

    sudo apt-get install python-dev python-pip python3-dev
    sudo apt-get install python3-setuptools
    sudo easy_install3 pip

For instructions on how to install the Python modules, see [`:help provider-python`].

If you want to use Neovim for some (or all) of the editor alternatives, use the following commands:

    sudo update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60
    sudo update-alternatives --config vi
    sudo update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60
    sudo update-alternatives --config vim
    sudo update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
    sudo update-alternatives --config editor

Note, however, that special interfaces, like `view` for `nvim -R`, are not supported.  (See [#1646](https://github.com/neovim/neovim/issues/1646) and [#2008](https://github.com/neovim/neovim/pull/2008).)


## Arch Linux

Neovim can be installed from the community repository:

    sudo pacman -S neovim

Alternatively, Neovim can be also installed using the PKGBUILD [`neovim-git`](https://aur.archlinux.org/packages/neovim-git), available on the [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository).

The Python modules are available from the community repository:

    sudo pacman -S python2-neovim python-neovim

The Ruby module (currently only supported in `neovim-git`) is available from the AUR as [`ruby-neovim`](https://aur.archlinux.org/packages/ruby-neovim).


## Gentoo Linux

An ebuild is available in Gentoo's official portage repository:

    emerge -a app-editors/neovim

## Exherbo Linux

Exhereses for scm and released versions are currently available in repository `::medvid`. Python client (with GTK+ GUI included) and Qt5 GUI are also available as suggestions:

    cave resolve app-editors/neovim --take dev-python/neovim-python --take app-editors/neovim-qt

## Fedora

### >= 25

Neovim and the Python modules are available in the official Fedora repositories starting with Fedora 25:

    dnf -y install neovim
    dnf -y install python2-neovim python3-neovim

### <= 24

    dnf -y copr enable dperson/neovim
    dnf -y install neovim
    dnf -y install python3-neovim python3-neovim-gui

## CentOS 7 / RHEL 7
 
http://copr.fedoraproject.org/coprs/dperson/neovim/

    yum -y install epel-release
    curl -o /etc/yum.repos.d/dperson-neovim-epel-7.repo https://copr.fedorainfracloud.org/coprs/dperson/neovim/repo/epel-7/dperson-neovim-epel-7.repo 
    yum -y install neovim

It's built using the [Copr](https://copr.fedoraproject.org/) automated build system, which is unsupported. There's no guarantee of how long the package will be available.

## Slackware

See [neovim on SlackBuilds](http://slackbuilds.org/apps/neovim/).

For instructions on how to install the Python modules, see [`:help provider-python`].

## Nix

Neovim can be installed with:

    nix-env -iA nixpkgs.neovim

To install the Python modules:

    nix-env -iA nixpkgs.python35Packages.neovim

Replace python35 with python27 for the python 2 packages.

## NixOS

Neovim can be installed with:

    nix-env -iA nixos.neovim

To install the Python modules:

    nix-env -iA nixos.python35Packages.neovim

Replace python35 with python27 for the python 2 packages.

## CRUX

A CRUX port is available under [`6c37/neovim`](https://github.com/6c37/crux-ports), along with ports for other dependencies of Neovim.

For instructions on how to install the Python modules, see [`:help provider-python`].

## FreeBSD

Neovim can be installed using [`pkg(8)`](https://www.freebsd.org/cgi/man.cgi?query=pkg&sektion=8&apropos=0&manpath=FreeBSD+10.2-RELEASE):

    pkg install neovim

or [from the ports tree](https://www.freshports.org/editors/neovim/):

    cd /usr/ports/editors/neovim/ && make install clean

## Void-Linux

Neovim can be installed using the xbps package manager

    sudo xbps-install -S neovim

## Solus

Neovim can be installed using the default package manager in Solus (eopkg):

    sudo eopkg install neovim

## Android

[Termux on the Google Play store](https://play.google.com/store/apps/details?id=com.termux) offers a Neovim package.

## Windows

Windows support is (currently) experimental. To try it out, you need `nvim.exe` and a front-end such as Neovim-Qt.

1. Download the latest [32bit build](https://ci.appveyor.com/api/projects/neovim/neovim/artifacts/build/Neovim.zip?branch=master&job=Configuration%3A%20MINGW_32) or [64bit build](https://ci.appveyor.com/api/projects/neovim/neovim/artifacts/build/Neovim.zip?branch=master&job=Configuration%3A%20MINGW_64)
2. Unzip `Neovim.zip` in `C:\Program Files (x86)\nvim\` or if 64bit version in `C:\Program Files\nvim\` (If you can't or don't want to install in `C:\Program Files (x86)\nvim\` set $VIMRUNTIME to the correct folder + /share/nvim/runtime)
3. Add the binary folder (`C:\Program Files (x86)\nvim\bin` or if 64bit version `C:\Program Files\nvim\bin`) to your PATH.
4. You should now be able to run `nvim` from the console (but it will block after a message).
5. Now download and unzip the latest [Neovim-Qt build](https://github.com/equalsraf/neovim-qt/releases).
6. Double-click `nvim-qt.exe`.
7. If you are missing `VCRUNTIME140.dll`, install the [Visual Studio 2015 C++ redistributable](https://support.microsoft.com/en-us/kb/2977003) (be sure to get x86_64 or x86 depending on your system).

### .vimrc file in Windows

If you already have Vim installed you can copy or symlink `%userprofile%\_vimrc` to `%userprofile%\AppData\Local\nvim\init.vim` to get the same settings as you already use in Vim.

# Install from source

If a package is not provided for your platform, see [Building-Neovim](https://github.com/neovim/neovim/wiki/Building-Neovim).  Once you've built Neovim, install it with the following commands:

    make
    sudo make install

For Unix-like systems this installs Neovim to `/usr/local`, while for Windows to `C:\Program Files`. Note, however, that this can complicate uninstallation. The following example avoids this by isolating an installation under `$HOME/neovim`:

    rm -r build/
    make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX=$HOME/neovim"
    make install
    export PATH="$HOME/neovim/bin:$PATH"

Note that the `rm -r build/` step above is needed if you've built Neovim before, as the install location will be the same as before since CMake caches build information.

## Uninstall

To uninstall Neovim installed with `make install`:

```sh
rm /usr/local/bin/nvim
rm -r /usr/local/share/nvim/
```

Or if you specified `CMAKE_INSTALL_PREFIX` at install-time, just _delete that directory_.

---

- See [Building Neovim](Building-Neovim) for more options. 
- See [FAQ](FAQ) for common problems.

[`:help provider-python`]: https://neovim.io/doc/user/provider.html#provider-python