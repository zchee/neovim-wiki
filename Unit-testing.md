Automated testing is essential for a project that aims to receive contributions from the community, it assists the project in growing faster without worrying about broken features. Pull requests that commit unit tests for existing functions will be given priority.

In Neovim, unit testing is achieved by compiling it as a shared library that can be loaded and called by luajit's [ffi module](http://luajit.org/ext_ffi.html). The ffi module is capable of parsing very basic C headers (no conditional directives or macro expansions), and we'll make use of this to avoid writing any glue C code. 

Each module must have a separate test script (written in moonscript or lua) in the test/unit directory. It might be possible to get started real fast by looking at existing [examples](https://github.com/neovim/neovim/tree/master/test/unit), but to get a deeper understanding of how this works, the best place is the ffi module [documentation](http://luajit.org/ext_ffi.html).

Here are some guidelines for writing tests:

- Use [bdd](http://en.wikipedia.org/wiki/Behavior-driven_development)'s idiom of writing specs, it yields to better organization and readability of tests(they look like specifications, right?). So describe what you're testing(and the environment if applicable) and create specs that assert it's behavior.
- For testing static functions or functions that have side effects visible only in module-global variables, create accessors for the modified variables. For example, say you are testing a function in misc1.c that modifies a static variable, create a file 'test/c-helpers/misc1.c' and add a function that retrieves the value after the function call. Files under test/c-helpers will only be compiled when building the test shared library.
- It's also possible to globally mock functions while running a test suite, this is useful to have more control over the environment for functions that have system side effects. See test/c-helpers/message.c.{mocks.h,defs.h} and test/unit/buffer_spec.lua for an example of how the `emsg` function is mocked in order to collect messages during function calls.
- Luajit needs to know about type and constant declarations used in function prototypes. The [helpers.moon](https://github.com/neovim/neovim/blob/master/test/unit/helpers.moon) file automatically parses types.h, so types used in the tested functions must be moved to it to avoid having to rewrite the declarations in the test files(Even though this is how it's currently done currently in the misc1/fs modules, but contributors are encouraged to refactor the declarations). Macro constants must be rewritten as enums so they can be 'visible' to the tests automatically.
- If something is too troublesome to test, ignore for now as it's probably going to be refactored.

