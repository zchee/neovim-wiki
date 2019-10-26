You can use [doxygen](http://doxygen.nl) to create callgraphs of all the functions in neovim as well as annotated source code with cross references (currently neovim does not use any doxygen comments so that is all you can get out of it for now).

In order to do that you will have to run the doxygen command with a an appropriate configuration file in the neovim root directory like so

```doxygen configfile```

You can create a default configuration file with doxygen using the `-g` flag

```doxygen -g configfilename```

In order to create the callgraphs you will need to set the following options in your doxygen config file

```
# This first one is optional
PROJECT_NAME           = "Neovim"
OPTIMIZE_OUTPUT_FOR_C  = YES
EXTRACT_ALL            = YES
EXTRACT_STATIC         = YES
# Set only the dirs you want
INPUT                  = src/ test/
RECURSIVE              = YES
SOURCE_BROWSER         = YES
HAVE_DOT               = YES
# Set according to your system
DOT_NUM_THREADS        = 3
CALL_GRAPH             = YES
CALLER_GRAPH           = YES
```
(The default config file with the above changes applied can be found [here](http://sillymon.ch/data/graphconfig))

Note that you will need the ```dot``` program (from the [graphviz](http://www.graphviz.org/) tool collection) to be installed when starting doxygen. Doxygen will call it to generate the graphs.

**Attention:** The above configuration will result in doxygen running for about 30 minutes and generating around 2.1GB worth of documentation. A reasonably recent version of the callgraphs should be accessible [here](http://sillymon.ch/neovim/html/index.html) if you do not want to generate them yourself.