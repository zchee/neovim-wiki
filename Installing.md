**Note**: If you want support for Python plugins such as YouCompleteMe, you must install a Python module in addition to Neovim itself. See [`:h nvim-python-quickstart`](http://neovim.org/doc/user/nvim_python.html#nvim-python-quickstart) for more information.

# Packaged Installation

If you're on one of the following systems, you can get Neovim right away!
If not, you can still [install Neovim manually](#manual-installation).

Note that the Neovim binary to run is called `nvim`, not `neovim`.

### OS X / [Homebrew](http://brew.sh)

```sh
brew tap neovim/homebrew-neovim
brew install --HEAD neovim
```

To **upgrade** from a previous version:

```sh
brew update
brew reinstall --HEAD neovim
```

### Linux / [Linuxbrew](http://brew.sh/linuxbrew/)

```sh
brew tap neovim/homebrew-neovim
brew install --HEAD neovim
```

To **upgrade** from a previous version:

```sh
brew update
brew reinstall --HEAD neovim
```

**Note**: If you encounter the error `CMAKE_USE_SYSTEM_CURL is ON but a curl is not found`, then you're missing the dependency for cURL that allows downloads over TLS. Refer back to your distro's section in [Linuxbrew Dependencies](https://github.com/Homebrew/linuxbrew#dependencies) to fix this.

### Ubuntu

Neovim has been added to a [Personal Package Archive](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable) which allows you to install it using `apt-get` on Ubuntu [12.04 and later](https://wiki.ubuntu.com/Releases).

Run the following commands:

```sh
sudo add-apt-repository ppa:neovim-ppa/unstable
sudo apt-get update
sudo apt-get install neovim
```

To install the Python module:

```sh
sudo apt-get install python-dev python-pip
pip install --user neovim
```

If you want to use Neovim for some (or all) of the editor alternatives, use the following commands:

```sh
sudo update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60
sudo update-alternatives --config vi
sudo update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60
sudo update-alternatives --config vim
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
sudo update-alternatives --config editor
```
### Arch Linux

Neovim can be installed using the PKGBUILD [`neovim-git`](https://aur.archlinux.org/packages/neovim-git), available on the [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository). The Python module has been packaged as [`python2-neovim`](https://aur.archlinux.org/packages/python2-neovim).

### CRUX

A CRUX port is available under [`6c37/neovim`](https://github.com/6c37/crux-ports), along with ports for other dependencies of Neovim.

### Gentoo Linux

A snapshot ebuild is now available in Gentoo's official portage repository: 

    emerge -a app-editors/neovim

A "live" ebuild can be found in [yngwin's developer overlay](http://cgit.gentooexperimental.org/dev/yngwin.git/tree/app-editors/neovim).

### openSUSE

Third-party packages are available for openSUSE 13.1/13.2/Factory, you can install them through the [1 Click Install](http://software.opensuse.org/package/neovim?search_term=Neovim) or manually using

```sh
zypper ar http://download.opensuse.org/repositories/home:/ruiabreuferreira:/neovim/openSUSE_13.1/
zypper in neovim
```

Adjust the URL if you're using openSUSE Factory or 13.2.

### Fedora / RHEL

See http://copr.fedoraproject.org/coprs/gaurdro/neovim/. It's built using the [Copr](https://copr.fedoraproject.org/) automated build system, which is completely unsupported. Additionally, there's no guarantee of how long your package will be available after the build finishes.

### Slackware

http://slackbuilds.org/apps/neovim/

### NixOS

Neovim can be installed from the [unstable channel](http://nixos.org/nixos/manual/#sec-upgrading) using the following command:

    nix-env -iA neovim

# Manual Installation

If no package is available for your operating system, you can perform a manual installation. This involves building Neovim and its dependencies, so you must first make sure that all build prerequisites are satisfied (see [build prerequisites](Building-Neovim#build-prerequisites)).

Afterwards, you can install Neovim into `/usr/local` by running `make install` (which generally requires root privileges).

To install Neovim to a directory of your choice, run the following command instead:

    make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=$HOME/neovim" install

If you appended `$HOME/neovim/bin` to your `$PATH`, you should be able to see the following:

```
which -a nvim
{path to your $HOME}/neovim/bin/nvim
```

**Note**: If you want to change the install location after you have already executed `make`, you need to remove the `build` directory to delete CMake's cache so it regenerates it on the next invocation of `make`:

```sh
# Install to `/usr/local`
make install
# Install to other location: need to remove `build` directory!
rm -r ./build
make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=$HOME/other/location" install
```

Alternatively, `nvim` can be run directly from the build directory:

```sh
# Compile
make
# You might want to define an alias for this in your shell's configuration file,
# or just export the `$VIMRUNTIME` environment variable.
env VIMRUNTIME="$(realpath runtime)" build/bin/nvim
# Generate help tags (from inside nvim)
:helptags $VIMRUNTIME/doc
```

See [Building Neovim](Building-Neovim) for more options and some pointers in case of [build errors](Building-Neovim#troubleshootingfaq).