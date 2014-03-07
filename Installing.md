## Dependencies

<a name="for-debianubuntu"></a>
### Ubuntu/Debian

    sudo apt-get install libtool autoconf automake cmake libncurses5-dev g++

<a name="for-centos-rhel"></a>
### CentOS/RHEL

If you're using CentOS/RHEL 6 you need at least autoconf version 2.69 for
compiling the libuv dependency. See joyent/libuv#1158.

<a name="for-freebsd-10"></a>
### FreeBSD 10

    sudo pkg install cmake libtool sha

<a name="for-arch-linux"></a>
### Arch Linux

    sudo pacman -S base-devel cmake ncurses

<a name="for-os-x"></a>
### OS X

* Install [Xcode](https://developer.apple.com/) and [Homebrew](http://brew.sh)
  or [MacPorts](http://www.macports.org)
* Install libtool, automake and cmake:

  Via MacPorts:

      sudo port install libtool automake cmake
      
  Via Homebrew:

      brew install libtool automake cmake

If you run into wget certificate errors, you may be missing the root SSL
certificates or have not set them up correctly:

  Via MacPorts:

      sudo port install curl-ca-bundle
      echo CA_CERTIFICATE=/opt/local/share/curl/curl-ca-bundle.crt >> ~/.wgetrc

  Via Homebrew:

      brew install curl-ca-bundle
      echo CA_CERTIFICATE=$(brew --prefix curl-ca-bundle)/share/ca-bundle.crt >> ~/.wgetrc


## Building

To generate the `Makefile`s:

    make cmake

To build and run the tests:

    make test

Using Homebrew on Mac:

    brew install --HEAD https://raw.github.com/neovim/neovim/master/neovim.rb
