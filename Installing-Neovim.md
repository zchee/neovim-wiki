- Before upgrading to a new version, **always check [Following HEAD](Following-HEAD).**
- To start Neovim, run `nvim` (not `neovim`).
- If you're wondering where to put your config (`vimrc`) see [here](https://github.com/neovim/neovim/wiki/FAQ#where-should-i-put-my-config-vimrc).

---

# Install from package

Packages are listed below. (You can also [build Neovim from source](#install-from-source).)

## Windows

The Neovim package for Windows includes the Neovim-Qt GUI.

If you have [chocolatey](https://chocolatey.org) installed you can just do:
- `choco install neovim` for **Release (v0.2):**
- `choco install neovim --pre` for **Development (pre-release):** 
 
 **Or:**

1. Choose a package:
    - **Release (v0.2):** [nvim-win32.zip](https://github.com/neovim/neovim/releases/download/v0.2.0/nvim-win32.zip) or [nvim-win64.zip](https://github.com/neovim/neovim/releases/download/v0.2.0/nvim-win64.zip)
    - **Development (pre-release):** [win32 build](https://ci.appveyor.com/api/projects/neovim/neovim/artifacts/build/Neovim.zip?branch=master&job=Configuration%3A%20MINGW_32) or [win64 build](https://ci.appveyor.com/api/projects/neovim/neovim/artifacts/build/Neovim.zip?branch=master&job=Configuration%3A%20MINGW_64)
2. Unzip the package. Any location is fine, administrator privileges are _not_ required.
    - `$VIMRUNTIME` will be set to that location automatically.
3. Double-click `nvim-qt.exe`.

**Optional** steps:

- Add the `bin` folder (e.g. `C:\Program Files\nvim\bin`) to your PATH.
    - This makes it easy to run `nvim` and `nvim-qt` from anywhere.
- If you are missing `VCRUNTIME140.dll`, install the [Visual Studio 2015 C++ redistributable](https://support.microsoft.com/en-us/kb/2977003) (choose x86_64 or x86 depending on your system).
- If `:set spell` does not work, create the `C:/Users/foo/AppData/Local/nvim/site/spell` folder. 
  You can then copy your spell files over (for English, located 
  [here](https://github.com/vim/vim/blob/master/runtime/spell/en.utf-8.spl) and 
  [here](https://github.com/vim/vim/blob/master/runtime/spell/en.utf-8.sug));
- For Python 2/3 plugins, you need the `neovim` Python module. "Virtual envs" are recommended. After activating the virtual env, enter `pip install neovim` (in *both*). Edit your `init.vim` so that it contains the path to the env's Python executable:
    ```vim
    let g:python3_host_prog='C:/Users/foo/Envs/neovim3/Scripts/python.exe'
    let g:python_host_prog='C:/Users/foo/Envs/neovim/Scripts/python.exe'
    ```
    - Run `:CheckHealth` and read `:help provider-python`.
- **init.vim ("vimrc"):** If you already have Vim installed you can copy `%userprofile%\_vimrc` to `%userprofile%\AppData\Local\nvim\init.vim` to use your Vim config with Neovim.


## macOS / OS X

### Pre-built archives

The [Releases](https://github.com/neovim/neovim/releases) page provides pre-built binaries for macOS 10.8+.

    curl -LO https://github.com/neovim/neovim/releases/download/nightly/nvim-macos.tar.gz
    tar xzf nvim-macos.tar.gz
    ./nvim-osx64/bin/nvim

### [Homebrew](http://brew.sh) (macOS) / [Linuxbrew](http://linuxbrew.sh/) (Linux)

    brew install neovim/neovim/neovim

See the [homebrew-neovim README](https://github.com/neovim/homebrew-neovim#installation) for a complete reference.

### [Macports](https://www.macports.org/)

    sudo port selfupdate
    sudo port install neovim

## Linux

### Arch Linux

Neovim can be installed from the community repository:

    sudo pacman -S neovim

Alternatively, Neovim can be also installed using the PKGBUILD [`neovim-git`](https://aur.archlinux.org/packages/neovim-git), available on the [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository).

The Python modules are available from the community repository:

    sudo pacman -S python2-neovim python-neovim

The Ruby module (currently only supported in `neovim-git`) is available from the AUR as [`ruby-neovim`](https://aur.archlinux.org/packages/ruby-neovim).

### CentOS 7 / RHEL 7
 
http://copr.fedoraproject.org/coprs/dperson/neovim/

    yum -y install epel-release
    curl -o /etc/yum.repos.d/dperson-neovim-epel-7.repo https://copr.fedorainfracloud.org/coprs/dperson/neovim/repo/epel-7/dperson-neovim-epel-7.repo 
    yum -y install neovim

It's built using the [Copr](https://copr.fedoraproject.org/) automated build system, which is unsupported. There's no guarantee of how long the package will be available.

### CRUX

A CRUX port is available under [`6c37/neovim`](https://github.com/6c37/crux-ports), along with ports for other dependencies of Neovim.

For instructions on how to install the Python modules, see [`:help provider-python`].


### Debian

Neovim is in [Debian](https://packages.debian.org/search?keywords=neovim).

    sudo apt-get install neovim

Python (`:python`) support is also installable via the Debian package manager.

    sudo apt-get install python-neovim
    sudo apt-get install python3-neovim

### Exherbo Linux

Exhereses for scm and released versions are currently available in repository `::medvid`. Python client (with GTK+ GUI included) and Qt5 GUI are also available as suggestions:

    cave resolve app-editors/neovim --take dev-python/neovim-python --take app-editors/neovim-qt

### Fedora

Neovim is in [Fedora](https://admin.fedoraproject.org/pkgdb/package/rpms/neovim/) starting with Fedora 25:

    dnf -y install neovim
    dnf -y install python2-neovim python3-neovim

*Fedora 24 and older*

    dnf -y copr enable dperson/neovim
    dnf -y install neovim
    dnf -y install python3-neovim python3-neovim-gui

### Gentoo Linux

An ebuild is available in Gentoo's official portage repository:

    emerge -a app-editors/neovim

### Nix / NixOS

Neovim can be installed with:

    nix-env -iA nixpkgs.neovim

To install the Python modules:

    nix-env -iA nixpkgs.python35Packages.neovim

Replace python35 with python27 for the python 2 packages.

### OpenSUSE

Neovim can be installed with:

    sudo zypper in Neovim

To install the Python modules:
    
    sudo zypper in python3-neovim
    sudo zypper in python-neovim

### PLD Linux

Neovim is in [PLD Linux](https://github.com/pld-linux/neovim):

    poldek -u neovim
    poldek -u python-neovim python3-neovim
    poldek -u python-neovim-gui python3-neovim-gui

### Slackware

See [neovim on SlackBuilds](http://slackbuilds.org/apps/neovim/).

For instructions on how to install the Python modules, see [`:help provider-python`].


### Source Mage

Neovim can be installed using the Sorcery package manager:

    cast neovim

### Solus

Neovim can be installed using the default package manager in Solus (eopkg):

    sudo eopkg install neovim

### Ubuntu

Neovim has been added to a "Personal Package Archive" (PPA). This allows you to install it with `apt-get` on Ubuntu [12.04 and later](https://wiki.ubuntu.com/Releases). Choose **stable** or **unstable**:

- [https://launchpad.net/~neovim-ppa/+archive/ubuntu/**stable**](https://launchpad.net/~neovim-ppa/+archive/ubuntu/stable)
- [https://launchpad.net/~neovim-ppa/+archive/ubuntu/**unstable**](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable)

**Note:** currently only packages for Xenial (16.04) are available on **stable**. If you are using a different version of Ubuntu, use the **unstable** PPA. See [#5811](https://github.com/neovim/neovim/issues/5811#issuecomment-278999317) for more information.

To be able to use **add-apt-repository** you may need to install software-properties-common:

    sudo apt-get install software-properties-common

If you're using an older version Ubuntu you must use:

    sudo apt-get install python-software-properties

Run the following commands:

    sudo add-apt-repository ppa:neovim-ppa/stable
    sudo apt-get update
    sudo apt-get install neovim

Prerequisites for the Python modules:

    sudo apt-get install python-dev python-pip python3-dev python3-pip

If you're using an older version Ubuntu you must use:

    sudo apt-get install python-dev python-pip python3-dev
    sudo apt-get install python3-setuptools
    sudo easy_install3 pip

For instructions to install the Python modules, see [`:help provider-python`].

If you want to use Neovim for some (or all) of the editor alternatives, use the following commands:

    sudo update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60
    sudo update-alternatives --config vi
    sudo update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60
    sudo update-alternatives --config vim
    sudo update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
    sudo update-alternatives --config editor

Note, however, that special interfaces, like `view` for `nvim -R`, are not supported.  (See [#1646](https://github.com/neovim/neovim/issues/1646) and [#2008](https://github.com/neovim/neovim/pull/2008).)

### Void-Linux

Neovim can be installed using the xbps package manager

    sudo xbps-install -S neovim

## BSD

### FreeBSD

Neovim can be installed using [`pkg(8)`](https://www.freebsd.org/cgi/man.cgi?query=pkg&sektion=8&apropos=0&manpath=FreeBSD+10.2-RELEASE):

    pkg install neovim

or [from the ports tree](https://www.freshports.org/editors/neovim/):

    cd /usr/ports/editors/neovim/ && make install clean


## Android

[Termux on the Google Play store](https://play.google.com/store/apps/details?id=com.termux) offers a Neovim package.


## Install from source

If a package is not provided for your platform, see [Building-Neovim](https://github.com/neovim/neovim/wiki/Building-Neovim).  Once you've built Neovim, install it with the following commands:

    make
    sudo make install

For Unix-like systems this installs Neovim to `/usr/local`, while for Windows to `C:\Program Files`. Note, however, that this can complicate uninstallation. The following example avoids this by isolating an installation under `$HOME/neovim`:

    rm -r build/
    make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX=$HOME/neovim"
    make install
    export PATH="$HOME/neovim/bin:$PATH"

Note that the `rm -r build/` step above is needed if you've built Neovim before, as the install location will be the same as before since CMake caches build information.

### Uninstall

To uninstall Neovim installed with `make install`:

```sh
sudo rm /usr/local/bin/nvim
sudo rm -r /usr/local/share/nvim/
```

Or if you specified `CMAKE_INSTALL_PREFIX` at install-time, just _delete that directory_.

---

- See [Building Neovim](Building-Neovim) for more options. 
- See [FAQ](FAQ) for common problems.

[`:help provider-python`]: https://neovim.io/doc/user/provider.html#provider-python