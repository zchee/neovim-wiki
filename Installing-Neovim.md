# Packaged Installation

If you're on one of the following systems, you can get Neovim right away!
If not, you can still [install Neovim manually](#manual-installation).

Note that the Neovim binary to run is called `nvim`, not `neovim`.

## [Homebrew](http://brew.sh) (OS X) / [Linuxbrew](http://brew.sh/linuxbrew/) (Linux)

See the [README of `neovim/homebrew-neovim`](https://github.com/neovim/homebrew-neovim/blob/master/README.md) for installation instructions.

## Ubuntu

Neovim has been added to a [Personal Package Archive](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable) which allows you to install it using `apt-get` on Ubuntu [12.04 and later](https://wiki.ubuntu.com/Releases).

Run the following commands:

```
sudo add-apt-repository ppa:neovim-ppa/unstable
sudo apt-get update
sudo apt-get install neovim
```

Prerequisites for the Python modules:

```
sudo apt-get install python-dev python-pip python3-dev python3-pip
```

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

If you want to use Neovim for some (or all) of the editor alternatives, use the following commands:

```
sudo update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60
sudo update-alternatives --config vi
sudo update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60
sudo update-alternatives --config vim
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
sudo update-alternatives --config editor
```

## Arch Linux

Neovim can be installed using the PKGBUILD [`neovim-git`](https://aur.archlinux.org/packages/neovim-git), available on the [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository).

For installing the Python modules, you have two alternatives:

 * Use the [`python2-neovim`](https://aur.archlinux.org/packages/python2-neovim) and [`python-neovim`](https://aur.archlinux.org/packages/python-neovim) PKGBUILDs.
 * Install `pip` and follow the instructions at [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html):

```
sudo pacman -S python-pip python2-pip
```

## CRUX

A CRUX port is available under [`6c37/neovim`](https://github.com/6c37/crux-ports), along with ports for other dependencies of Neovim.

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

## Gentoo Linux

A snapshot ebuild is now available in Gentoo's official portage repository:

```
emerge -a app-editors/neovim
```

A "live" ebuild can be found in [yngwin's developer overlay](http://cgit.gentooexperimental.org/dev/yngwin.git/tree/app-editors/neovim).

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

## Exherbo Linux

A "scm" exheres is currently available in repository `::exony`:

```
$ cave resolve app-editors/neovim::exony
```

## Fedora 21/22
 
http://copr.fedoraproject.org/coprs/dperson/neovim/

```
dnf copr enable dperson/neovim
dnf install neovim
```

It's built using the [Copr](https://copr.fedoraproject.org/) automated build system, which is unsupported. There's no guarantee of how long your package will be available after the build finishes.

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

## Slackware

See [neovim on SlackBuilds](http://slackbuilds.org/apps/neovim/).

For instructions on how to install the Python modules, see [`:help nvim_python`](http://neovim.io/doc/user/nvim_python.html).

# Manual Installation

If no package is available for your operating system, you can perform a manual installation. This involves building Neovim and its dependencies, so you must first make sure that all build prerequisites are satisfied (see [build prerequisites](Building-Neovim#build-prerequisites)).

Afterwards, you can install Neovim into `/usr/local` by running `make install` (which generally requires root privileges).

To install Neovim to a directory of your choice, run the following command instead:

```
$ make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=$HOME/neovim" install
```

If you appended `$HOME/neovim/bin` to your `$PATH`, running `which -a nvim` should print the following:

```
{path to your $HOME}/neovim/bin/nvim
```

--------------

If you want to change the install location after you have already executed `make`, you need to remove the `build` directory to delete CMake's cache, so it regenerates it on the next invocation of `make`:

```
rm -r ./build
make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=$HOME/other/location" install
```

Alternatively, `nvim` can be run directly from the build directory. You might want to define an alias for this in your shell's configuration file, or just export the `$VIMRUNTIME` environment variable:

```
env VIMRUNTIME="$(realpath runtime)" build/bin/nvim
```

After that, run the following from inside `nvim`:

```vim
:helptags $VIMRUNTIME/doc
```

See [Building Neovim](Building-Neovim) for more options. See [Troubleshooting](Troubleshooting) if you encounter [build](Troubleshooting#build-issues) or [installation errors](Troubleshooting#installation-issues).