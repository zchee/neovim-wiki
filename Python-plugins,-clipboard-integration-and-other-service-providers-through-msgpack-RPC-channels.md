(The information presented here will only be correct after #895 is merged)

One of the project's initial goals was to simplify maintenance by externalizing
non-essential editor features out of the core, and PR #895 brings an important
development on this area: The infrastructure necessary to call blocking
functions from C through the msgpack-RPC API. Here are some immediate benefits
brought by this feature:

- Support for scripting in other languages can be implemented with very small
  C changes
- GUI-specific functionality such as clipboard and dialog functions can be
  removed from C, and implemented using high-level abstractions/languages
  provided by GUI toolkits.
- Externalization features such as spell checking and cryptography, which are
  already provided by many open source projects.
- The ability to use external programs as "libraries", which is great for
  implementing functions on top of platforms such as node.js, which do not
  support classic embedding through shared libraries.

Besides implementing the necessary infrastructure, #895 also exposes extension
points for two features that were previously missing from Neovim: clipboard
integration and support for python plugins.

For now clipboard is implemented through the python plugin host using the
'xerox' module, but in the future this will be a job for GUIs, which already have
a direct connection to the OS-specific clipboard system.

Python scripting is also experimental and disabled by default. This is because
the python client currently suffers from some performance issues due to the
synchronization code used to make the API thread-safe, and it becomes visible
when using plugins that need high API throughput. This
will be fixed in the next release of the client, which will be implemented using
lightweight threads

Another important characteristic of the current python interface is that it
doesn't support the new python features added in vim 7.4(mainly the bindeval
function), so it won't work with plugins that use these features.

With that said, here are the steps necessary to make Neovim run python plugins:

- Make sure you have python installed. python3 is not supported yet(This is a
  limitation of the python client).
- Install the python client: `pip install neovim`
- On the top of your vimrc(before any code that checks for `has('python')`),
  add this snippet:

```vim
if has('neovim')
  let s:python_host_init = 'python -c "import neovim; neovim.start_host()"'
  let &initpython = s:python_host_init
endif
```

The `python_host_init` variable contains the shell command which bootstraps the
python interpreter, and the command is called the first time a python command
is used(`has('python')` will return true if the command is executable). The
string must be .in the same format as the `shell` option(:help 'shell').

For now, clipboard also depends on python(This will change once we have GUIs working):

- Install the 'xerox' module: `pip install xerox`
- Create a ~/.vim/pythonx/nvim_clipboard.py file with the following contents:

```
import xerox

class NvimClipboard(object):
    def __init__(self, vim):
        self.provides = ['clipboard_get', 'clipboard_set']

    def clipboard_get(self):
        return xerox.paste().split('\n')
    
    def clipboard_set(self, lines):
        xerox.copy('\n'.join(lines))
```

The following option is available to simplify clipboard integration:

```vim
if has('neovim')
  set unnamedclip " Automatically use clipboard as storage for the unnamed register
endif
```

The python script above implements the "clipboard provider", and it's automatically loaded when the python host is started. If you load python plugins in your vimrc, that will happen transparently after the first call to the `python` command, but it's also possible to configure Neovim to bootstrap the python host the first time the clipboard register is needed. Here's a vimrc snippet that automatically activates clipboard or python plugins(independently of each other):

```vim
if has('neovim')
  let s:python_host_init = 'python -c "import neovim; neovim.start_host()"'
  let &initpython = s:python_host_init
  let &initclipboard = s:python_host_init
  set unnamedclip " Automatically use clipboard as storage for the unnamed register
endif
```

### Troubleshooting python/clipboard issues

Here are common causes for errors:

- The python client is outdated, try `pip uninstall neovim && pip install neovim`
- The clipboard module(nvim_clipboard.py) was not found, possible causes:
  - The filename doesn't start with 'nvim_'. This is a requirement of the python plugin host, which will only 
    load modules prefixed with 'nvim_'
  - The file was not installed in the right directory. It must be in a directory that is automatically found
    by the module loader used in the classic python-vim bridge(runtime/pythonx or runtime/python2)
- In some distros(eg: archlinux) 'python' refers to python3. If that's your case, try `let s:python_host_init = 'python2 -c "import neovim; neovim.start_host()"'` as the bootstrap command


The logs will probably contain useful debugging information . ~/.nvimlog contains Neovim-specific messages(such as problems before the python host is initialized). Here's the typical ~/.nvimlog output when python/clipboard are correctly initialized(they will be if python plugins are loaded in your vimrc)

```
2014/07/17 11:19:15 [info @ provider_register:96] 18093 - Registered channel 1 as the provider for "python_execute"
2014/07/17 11:19:15 [info @ provider_register:96] 18093 - Registered channel 1 as the provider for "python_execute_file"
2014/07/17 11:19:15 [info @ provider_register:96] 18093 - Registered channel 1 as the provider for "python_do_range"
2014/07/17 11:19:15 [info @ provider_register:96] 18093 - Registered channel 1 as the provider for "python_eval"
2014/07/17 11:19:15 [info @ provider_register:96] 18093 - Registered channel 1 as the provider for "clipboard_get"
2014/07/17 11:19:15 [info @ provider_register:96] 18093 - Registered channel 1 as the provider for "clipboard_set"
2014/07/17 11:19:15 [info @ main_loop:556] 18093 - Starting Neovim main loop.
```

To enable logging on the python process, set the NEOVIM_PYTHON_LOG_FILE environment variable, eg:

```
NEOVIM_PYTHON_LOG_FILE=python.log nvim
```

As explained, not all python plugins will perform well(or even work) with
Neovim. One example is YouCompleteMe, which gets really slow for big files.
[This branch](https://github.com/tarruda/YouCompleteMe/tree/nvim2) contains a
patch that improves YCM performance with Neovim, it can be used as a
temporary workaround for YCM users until the problems with the python client are fixed

If you are running into performance problems with other python plugins, it's
possible to create a cProfile report using the NEOVIM_PYTHON_PROFILE
environment variable:

```
NEOVIM_PYTHON_PROFILE=1 nvim && cat .nvim-python-client.profile
```