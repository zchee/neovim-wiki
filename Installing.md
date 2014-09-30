# Packaged Install

If you're on one of these systems, you can get Neovim right away!

### OS X / [homebrew](http://brew.sh)

    brew install --HEAD https://raw.github.com/neovim/neovim/master/neovim.rb

If you'd like to upgrade a previous homebrew install to the latest version of neovim, just run:

    brew reinstall --HEAD https://raw.github.com/neovim/neovim/master/neovim.rb

### Linux / [Linuxbrew](http://brew.sh/linuxbrew/)

    brew install --HEAD https://raw.github.com/neovim/neovim/master/neovim.rb

Substitute `reinstall` for the `install` command to upgrade from a previous version.

Note: If you have the following error: `CMAKE_USE_SYSTEM_CURL is ON but a curl is not found`, you are missing the dependency for cURL that allows SSL downloads. Refer back to your distro's section in the [Linuxbrew Dependencies](https://github.com/Homebrew/linuxbrew#dependencies) to fix this.

### Ubuntu

Neovim has been added to a [Personal Package Archive](https://launchpad.net/~rudenko/+archive/ubuntu/neovim) which allows you to install it using `apt-get` for versions [12.04 and on](https://wiki.ubuntu.com/Releases).

Just run the following commands:

```bash
sudo add-apt-repository ppa:rudenko/neovim
sudo apt-get update
sudo apt-get install neovim 
```

### Arch Linux

Package can be installed from [AUR](https://aur.archlinux.org/packages/neovim-git/)

### Gentoo Linux

Package can be installed from [science overlay](http://gpo.zugaina.org/app-editors/neovim)

### openSUSE

Third-party packages are available for openSUSE 13.1/Factory, you can install them through the [1 Click Install](http://software.opensuse.org/package/neovim?search_term=Neovim) or manually using

    zypper ar http://download.opensuse.org/repositories/home:/ruiabreuferreira/openSUSE_13.1/ home:ruiabreuferreira
    zypper in neovim

# Manual Install

### Dependencies

<a name="for-debianubuntu"></a>
#### Ubuntu/Debian

    sudo apt-get install libtool autoconf automake cmake libncurses5-dev g++ pkg-config unzip

<a name="for-centos-rhel"></a>
#### CentOS/RHEL/Fedora

If you're using CentOS/RHEL 6 you need at least autoconf version 2.69 for
compiling the libuv dependency. See https://github.com/joyent/libuv/issues/1158.

    sudo yum -y install autoconf automake cmake gcc gcc-c++ libtool ncurses-devel pkgconfig

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

A few lua packages are required for the build process. Normally these packages will be installed via [luarocks](http://luarocks.org/) (invoked by cmake automatically), but sometimes this will fail. There are two common causes for this:

- luarocks servers are down
- you need to install the 'unzip' command-line utility, if this is the case luarocks will report something like this: `Warning: Failed searching manifest: Failed loading manifest: Failed extracting manifest file`

To fix the first error, a luarocks mirror can be used:

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
- [lua-MessagePack](http://fperrad.github.io/lua-MessagePack/)

For running tests, these are also required:

- [busted](http://olivinelabs.com/busted/)

Keep in mind that some of those packages have their own dependencies which also have to be installed

### Building

You can build the `nvim` executable immediately by just calling `make` (which will invoke `cmake` as required):

```bash
make
```

If you decide to try another compiler, you can try something like:

```bash
rm -rf ./build && make CC="/path/to/my/compiler"
```

See [Building Neovim](Building-Neovim) for more options.

### Installing

After building, the Neovim binary file will be in `./build/bin/nvim`. 

If you want to install the binary file in a specific location in your system (for example, `~/usr/bin/nvim`):

```
cmake -DCMAKE_INSTALL_PREFIX:PATH=~/foo/
make install
```

If you added `~/foo/bin` to your `$PATH`, you should be able to see the following:

```
$ which -a nvim
{path to your $HOME}/foo/bin/nvim
```