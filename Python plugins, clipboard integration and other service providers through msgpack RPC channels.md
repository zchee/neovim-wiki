One of the project's initial goals was to simplify maintenance by externalizing non-essential editor features out of the core, and PR [#895](https://github.com/neovim/neovim/pull/895) brought an important development on this area: The infrastructure necessary to call blocking functions from C through the msgpack-RPC API. Here are some immediate benefits of this feature:

- Support for scripting in other languages can be implemented with very small
  C changes. For example, [this commit](https://github.com/neovim/neovim/commit/486c8e37c17e4aa89fa9ef7e0c682b659a5a8a82) implements python support.
- GUI-specific functionality such as clipboard and dialog functions can be
  removed from C, and implemented using high-level abstractions/languages
  provided by GUI toolkits.
- Externalization features such as spell checking and cryptography, which are
  already provided by many open source projects.
- The ability to use external programs as "libraries", which is great for
  implementing functions on top of platforms such as node.js, which do not
  support classic embedding through shared libraries.

Besides implementing the necessary infrastructure, [#895](https://github.com/neovim/neovim/pull/895) also exposed extension points for two features that were previously missing from Neovim: clipboard
integration and support for python plugins.

For now clipboard is implemented through the python plugin host using the 'xerox' module, but in the future this will be a job for GUIs, which already have a direct connection to the OS-specific clipboard system.

Python scripting is also experimental and disabled by default. This is because the python client currently suffers from some performance issues due to the synchronization code used to make the API thread-safe, and it becomes noticeable when using plugins that need high API throughput. This will be fixed in the next release of the client, which will be implemented using lightweight threads

An important characteristic of the current python interface is that it doesn't support the new python features added in vim 7.4(mainly the bindeval function), so it won't work with plugins that use these features.

For instructions on how to enable python and clipboard in nvim, use the internal help system: `:help nvim-intro`
