## Quick install

If you're on one of the following OSes, good news! You can get neovim right away!

### OS X / [homebrew](http://brew.sh)

    brew install --HEAD https://raw.github.com/neovim/neovim/master/neovim.rb

### Arch Linux

Package can be installed from [AUR](https://aur.archlinux.org/packages/neovim-git/)

## Manual install

### Dependencies

<a name="for-debianubuntu"></a>
#### Ubuntu/Debian

    sudo apt-get install libtool autoconf automake cmake libncurses5-dev g++ pkg-config

You may also need to install luajit and/or luarocks.

<a name="for-centos-rhel"></a>
#### CentOS/RHEL/Fedora

If you're using CentOS/RHEL 6 you need at least autoconf version 2.69 for
compiling the libuv dependency. See https://github.com/joyent/libuv/issues/1158.

    sudo yum -y install autoconf automake cmake gcc libtool ncurses-devel pkg-config

<a name="for-freebsd-10"></a>
#### FreeBSD 10

    sudo pkg install cmake libtool sha automake pkgconf libuv luajit

<a name="for-arch-linux"></a>
#### Arch Linux

    sudo pacman -S base-devel cmake ncurses pkg-config luajit

<a name="for-os-x"></a>
#### OS X

* Install [Xcode](https://developer.apple.com/) and [Homebrew](http://brew.sh)
  or [MacPorts](http://www.macports.org)
* Install libtool, automake and cmake:

  Via MacPorts:

      sudo port install libtool automake cmake pkgconfig luajit luarocks
      
  Via Homebrew:

      brew install libtool automake cmake pkg-config

If you run into wget certificate errors, you may be missing the root SSL
certificates or have not set them up correctly:

  Via MacPorts:

      sudo port install curl-ca-bundle
      echo CA_CERTIFICATE=/opt/local/share/curl/curl-ca-bundle.crt >> ~/.wgetrc

  Via Homebrew:

      brew install curl-ca-bundle
      echo CA_CERTIFICATE=$(brew --prefix curl-ca-bundle)/share/ca-bundle.crt >> ~/.wgetrc


### Building

To generate the `Makefile`s:

    make cmake

To build and run the tests:

    make test

