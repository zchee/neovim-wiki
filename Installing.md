# Packaged Install

If you're on one of these systems, you can get Neovim right away! (If not, don't worry: you can still [install Neovim manually](#user-content-manual-install).)

### OS X / [homebrew](http://brew.sh)

    brew install --HEAD https://raw.github.com/neovim/neovim/master/neovim.rb

If you'd like to upgrade a previous homebrew install to the latest version of neovim, just run:

    brew reinstall --HEAD https://raw.github.com/neovim/neovim/master/neovim.rb

### Linux / [Linuxbrew](http://brew.sh/linuxbrew/)

    brew install --HEAD https://raw.github.com/neovim/neovim/master/neovim.rb

Substitute `reinstall` for the `install` command to upgrade from a previous version.

Note: If you have the following error: `CMAKE_USE_SYSTEM_CURL is ON but a curl is not found`, you are missing the dependency for cURL that allows SSL downloads. Refer back to your distro's section in the [Linuxbrew Dependencies](https://github.com/Homebrew/linuxbrew#dependencies) to fix this.

### Ubuntu

 [*(broken since September 2014)*](https://launchpad.net/~rudenko/+archive/ubuntu/neovim/+builds?build_text=&build_state=all)

Neovim has been added to a [Personal Package Archive](https://launchpad.net/~rudenko/+archive/ubuntu/neovim) which allows you to install it using `apt-get` for versions [12.04 and on](https://wiki.ubuntu.com/Releases).

Just run the following commands:

```bash
sudo add-apt-repository ppa:rudenko/neovim
sudo apt-get update
sudo apt-get install neovim 
```

### Arch Linux

Package can be installed from [AUR](https://aur.archlinux.org/packages/neovim-git/).

### Gentoo Linux

Package can be installed from [science overlay](http://gpo.zugaina.org/app-editors/neovim).

### openSUSE

Third-party packages are available for openSUSE 13.1/13.2/Factory, you can install them through the [1 Click Install](http://software.opensuse.org/package/neovim?search_term=Neovim) or manually using

    zypper ar http://download.opensuse.org/repositories/home:/ruiabreuferreira:/neovim/openSUSE_13.1/
    zypper in neovim

Similarly adjust the URL for Factory or 13.2.

### Slackware

http://slackbuilds.org/apps/neovim/

# Manual Install

If no package is available for your operating system, you can perform a manual installation. This involves building Neovim and its dependencies, so you first need to make sure that all required build prerequisites are installed (see [build prerequisites](Building-Neovim#build-prerequisites)).

Afterwards, you can build and install Neovim into `/usr/local` by calling `make install` (which will invoke `cmake` as required).

To install Neovim to a directory of your choice, execute the following command instead:

```bash
make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=~/neovim" install
```

If you added `~/neovim/bin` to your `$PATH`, you should be able to see the following:

```
$ which -a nvim
{path to your $HOME}/neovim/bin/nvim
```

Please note that if you want to change the install location after you have already executed `make`, you need to remove the `build` directory to get rid of CMake's cache:

```bash
# Install to `/usr/local`
make install
# Install to other location: need to remove `build` directory!
rm -rf ./build
make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=~/other/location" install
```

See [Building Neovim](Building-Neovim) for more options and some pointers in case of [build errors](Building-Neovim#troubleshootingfaq).