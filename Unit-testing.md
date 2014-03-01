Automated testing is essential for a project that aims to receive contributions from the community, it assists the project in growing faster without worrying about broken features. See [this](https://groups.google.com/forum/#!forum/neovim) for a better explanation. Pull requests that commit unit tests for existing functions will be given priority.

The act of testing individual functions is referred here as 'unit testing', even if the function being tested calls the operating system. This is explained here because some may consider as 'unit tests' only those tests that verify a function, method or class in complete isolation, normally using fake code to mock interfaces for external systems needed by the tested code.

For now we'll keep things simple and test the whole function as it is, performing verifications on external systems touched by the function. With time, after we have isolated all system functions in the 'os' directory, we may be able to implement a mock for the 'os' module, so we can perform verifications without touching the operating system(The mock would probably be implementation in moonscript or lua, called from C). 

In neovim, unit testing will be done by compiling it as a shared library that can be loaded and called by luajit's [ffi module](http://luajit.org/ext_ffi.html). The ffi module is capable of parsing very basic C headers(no conditional directives or macro expansions), and we'll make use of this to avoid writing any glue C code(Still requires merging #215).

Each module will have a separate test script(written in moonscript) in the test/unit directory. It might be possible to get started real fast by looking at existing [examples](https://github.com/neovim/neovim/tree/master/test/unit), but to get a deeper understanding of how this works, the best place is the ffi module [documentation](http://luajit.org/ext_ffi.html).

Here are some guidelines for writing tests:

- Use [bdd](http://en.wikipedia.org/wiki/Behavior-driven_development)'s idiom of writing specs, it yields to better organization and readability of tests(they look like specifications, right?). So describe what you're testing(and the environment if applicable) and create specs that assert it's behavior.
- For testing functions that have side effects visible only in global variables, create accessors for the modified variables. For example, say you are testing a function in misc1.c, create a file 'test/unit/accessors/misc1.c' and add a function that retrieves the value of the global variable. The 'accessors' directory will only be compiled for the shared library, of course(This still needs to be configured in cmake).
- If something is too troublesome to test, ignore for now as it's probably going to be refactored.

