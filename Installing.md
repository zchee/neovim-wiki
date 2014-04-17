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

<a name="for-centos-rhel"></a>
#### CentOS/RHEL/Fedora

If you're using CentOS/RHEL 6 you need at least autoconf version 2.69 for
compiling the libuv dependency. See https://github.com/joyent/libuv/issues/1158.

    sudo yum -y install autoconf automake cmake gcc libtool ncurses-devel pkgconfig

<a name="for-opensuse"></a>
### openSUSE

    sudo zypper install libtool autoconf automake cmake ncurses-devel gcc-c++

<a name="for-freebsd-10"></a>
#### FreeBSD 10

    sudo pkg install cmake libtool sha automake pkgconf libuv luajit unzip wget

Note: if you have cmake installed already, you may need to re-install it.  The
port had to be updated to support SSL for file downloads, so you may not have
that feature. If you see the download complaining about an md5sum mismatch, and
the actual md5sum is `d41d8cd98f00b204e9800998ecf8427e`, then this is your issue
(that's the md5sum of an empty file). Also, make sure you have wget installed.
Luarocks has bad interactions with curl, at least under FreeBSD, and will die with
a PANIC in LuaJIT when trying to install a rock.

<a name="for-arch-linux"></a>
#### Arch Linux

    sudo pacman -S base-devel cmake ncurses pkg-config luajit unzip

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

<a name="lua-packages"></a>
#### Lua packages

A few lua packages are required for the build process. Normally these packages will be installed automatically via [luarocks](http://luarocks.org/), but sometimes this will fail(by hanging forever with no feedback) because luarocks.org servers are down. If you experience something similar, try using a mirror and running `make cmake` again:

```sh
cat >> .deps/usr/etc/luarocks/config-5.1.lua << "EOF"
rocks_servers={ 
  "http://luarocks.giga.puc-rio.br/" 
}
EOF
make cmake
```

Failing the above, you can always try installing the following packages manually:

- [lpeg](http://www.inf.puc-rio.br/~roberto/lpeg/)
- [lua-cmsgpack](https://github.com/antirez/lua-cmsgpack)
- [busted](http://olivinelabs.com/busted/)(for testing)
- [moonscript](http://moonscript.org/)(for testing)

Keep in mind that some of those packages have their own dependencies which also have to be installed

### Building

To generate the `Makefile`s without building:

```bash
make cmake
```

Alternatively, you can build the executable immediately by just calling make (which will invoke `cmake` as required):

```bash
make
```

If you decide to try another compiler, you can try something like:

```bash
rm -rf ./build && make CC="/path/to/my/compiler"
```

To build and run the tests:

```bash
make test
```

