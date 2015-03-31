**Note**: If you use Python plugins such as [YouCompleteMe](https://github.com/Valloric/YouCompleteMe), see [`:help nvim-python-quickstart`](http://neovim.org/doc/user/nvim_python.html#nvim-python-quickstart).

# Packaged Installation

If you're on one of the following systems, you can get Neovim right away!
If not, you can still [install Neovim manually](#manual-installation).

Note that the Neovim binary to run is called `nvim`, not `neovim`.

### OS X / [Homebrew](http://brew.sh)

```
brew tap neovim/homebrew-neovim
brew install --HEAD neovim
```

For troubleshooting hints, see the README of [neovim/homebrew-neovim](https://github.com/neovim/homebrew-neovim).

To **upgrade** from a previous version:

```
brew update
brew reinstall --HEAD neovim
```

### Linux / [Linuxbrew](http://brew.sh/linuxbrew/)

```
brew tap neovim/homebrew-neovim
brew install --HEAD neovim
```

For troubleshooting hints, see the README of [neovim/homebrew-neovim](https://github.com/neovim/homebrew-neovim).

To **upgrade** from a previous version:

```
brew update
brew reinstall --HEAD neovim
```

**Note**: If you encounter the error `CMAKE_USE_SYSTEM_CURL is ON but a curl is not found`, then you're missing the dependency for cURL that allows downloads over TLS. Refer to your operating system's section in [Linuxbrew Dependencies](https://github.com/Homebrew/linuxbrew#dependencies) to fix this.

### Ubuntu

Neovim has been added to a [Personal Package Archive](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable) which allows you to install it using `apt-get` on Ubuntu [12.04 and later](https://wiki.ubuntu.com/Releases).

Run the following commands:

```
sudo add-apt-repository ppa:neovim-ppa/unstable
sudo apt-get update
sudo apt-get install neovim
```

To install the Python module:

```
sudo apt-get install python-dev python-pip
pip install --user neovim
```

If you want to use Neovim for some (or all) of the editor alternatives, use the following commands:

```
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

```
zypper ar http://download.opensuse.org/repositories/home:/ruiabreuferreira:/neovim/openSUSE_13.2/home:ruiabreuferreira:neovim.repo

zypper in neovim
```

Adjust the URL if you're using openSUSE Factory or 13.2.

### Fedora / RHEL

See http://copr.fedoraproject.org/coprs/gaurdro/neovim/. It's built using the [Copr](https://copr.fedoraproject.org/) automated build system, which is unsupported. There's no guarantee of how long your package will be available after the build finishes.

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

```
# Install to `/usr/local`
make install
# Install to other location: need to remove `build` directory!
rm -r ./build
make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=$HOME/other/location" install
```

Alternatively, `nvim` can be run directly from the build directory:

```
# Compile
make
# You might want to define an alias for this in your shell's configuration file,
# or just export the `$VIMRUNTIME` environment variable.
env VIMRUNTIME="$(realpath runtime)" build/bin/nvim
# Generate help tags (from inside nvim)
:helptags $VIMRUNTIME/doc
```

See [Building Neovim](Building-Neovim) for more options and some pointers in case of [build errors](https://github.com/neovim/neovim/wiki/Building-Neovim#troubleshooting).

<a name="troubleshooting"</a>
# Troubleshooting

### Homebrew/Linuxbrew

See [Homebrew#troubleshooting](https://github.com/neovim/homebrew-neovim#troubleshooting).