- Before upgrading to a new version, **always check [Following HEAD](Following-HEAD).**
- If you're wondering where to put your config (`vimrc`) see [here](https://github.com/neovim/neovim/wiki/FAQ#where-should-i-put-my-config-vimrc).

# Install from package

If you're on one of the following systems, you can get Neovim right away!
If not, you can still [install Neovim manually](#install-from-source).

Note that the Neovim binary to run is called `nvim`, not `neovim`.

## [Homebrew](http://brew.sh) (OS X) / [Linuxbrew](http://linuxbrew.sh/) (Linux)

See the [README of `neovim/homebrew-neovim`](https://github.com/neovim/homebrew-neovim/blob/master/README.md) for installation instructions.

## [Macports](https://www.macports.org/) (OS X)

Run the following commands:

    sudo port selfupdate
    sudo port install neovim

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

## Debian

Neovim and the Python client are available as [Debian packages](https://packages.debian.org/search?keywords=neovim).

## Arch Linux

Neovim can be installed from the community repository:

    sudo pacman -S neovim

Alternatively, Neovim can be also installed using the PKGBUILD [`neovim-git`](https://aur.archlinux.org/packages/neovim-git), available on the [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository).

The Python modules are available from the community repository:

    sudo pacman -S python2-neovim python-neovim

The Ruby module (currently only supported in `neovim-git`) is available from the AUR as [`ruby-neovim`](https://aur.archlinux.org/packages/ruby-neovim).


## Gentoo Linux

A snapshot ebuild is now available in Gentoo's official portage repository:

    emerge -a app-editors/neovim

A "live" ebuild can be found in [yngwin's developer overlay](http://cgit.gentooexperimental.org/dev/yngwin.git/tree/app-editors/neovim).

For instructions on how to install the Python modules, see [`:help provider-python`].

## Exherbo Linux

Exhereses for scm and released versions are currently available in repository `::medvid`. Python client (with GTK+ GUI included) and Qt5 GUI are also available as suggestions:

    cave resolve app-editors/neovim --take dev-python/neovim-python --take app-editors/neovim-qt

## Fedora 22/23/24
 
http://copr.fedoraproject.org/coprs/dperson/neovim/

    dnf -y install dnf-plugins-core
    dnf -y copr enable dperson/neovim
    dnf -y install neovim

It's built using the [Copr](https://copr.fedoraproject.org/) automated build system, which is unsupported. There's no guarantee of how long your package will be available after the build finishes.

For instructions on how to install the Python modules, see [`:help provider-python`].

When installing Python packages, ensure that you have the python2-greenlet-devel package installed.

## CentOS 7
 
http://copr.fedoraproject.org/coprs/dperson/neovim/

    yum -y install epel-release
    curl -o /etc/yum.repos.d/dperson-neovim-epel-7.repo https://copr.fedorainfracloud.org/coprs/dperson/neovim/repo/epel-7/dperson-neovim-epel-7.repo 
    yum -y install neovim

It's built using the [Copr](https://copr.fedoraproject.org/) automated build system, which is unsupported. There's no guarantee of how long your package will be available after the build finishes.

For instructions on how to install the Python modules, see [`:help provider-python`].

When installing Python packages, ensure that you have the python2-greenlet-devel package installed.


## Slackware

See [neovim on SlackBuilds](http://slackbuilds.org/apps/neovim/).

For instructions on how to install the Python modules, see [`:help provider-python`].

## NixOS

Neovim can be installed from the [unstable channel](http://nixos.org/nixos/manual/#sec-upgrading) using the following command:

    nix-env -iA neovim

For instructions on how to install the Python modules, see [`:help provider-python`].

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

Neovim can be installed using the default package manager in Solus (PiSi):

    sudo pisi install neovim

## Android

[Termux on the Google Play store](https://play.google.com/store/apps/details?id=com.termux) offers a Neovim package.

## Windows

Windows support is (currently) experimental. To try it out, you need `nvim.exe` and a front-end such as Neovim-Qt.

1. Download the latest [32bit build](https://ci.appveyor.com/api/projects/equalsraf/neovim/artifacts/build/Neovim.zip?branch=tb-mingw&job=Configuration%3A%20MINGW_32)) or [64bit build](https://ci.appveyor.com/api/projects/equalsraf/neovim/artifacts/build/Neovim.zip?branch=tb-mingw&job=Configuration%3A%20MINGW_32)
2. Unzip `Neovim.zip` to a new directory (e.g. `C:/Neovim`)
3. Add the binary folder (`C:/Neovim/bin`) to your PATH.
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

For Unix-like systems this installs Neovim to `/usr/local`, while for Windows to `C:/Program Files`. Note, however, that this can complicate uninstallation. The following example avoids this by isolating an installation under `$HOME/neovim`:

    rm -r build/
    make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=$HOME/neovim"
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