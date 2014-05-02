### C programming techniques and Neovim-specific guidance

[`typeof(<var>)` vs `typeof(<type>)`](https://github.com/neovim/neovim/pull/558#discussion_r11767481)
> something you have to be really careful about: the difference between arrays and pointers [...]
> be judicious: if the variable is simple, use `sizeof(variable)`, if the variable is complex, use `sizeof(the_actual_type)`

[Conversion of signed variables to unsigned (in files not checked by `-Wconversion`)](https://github.com/neovim/neovim/pull/558#issuecomment-40863654)

#### Types

(to be filled in)

##### Unsigned or signed? Beware of integer over- and underflow

##### Fixed-size vs. generic types

Should we use `(u)intX_t` and friends over `char`, `short`, `int`, `long` et al.? ...

### Tools

There are handy tools that can help while creating, maintaining and transforming a codebase, as we are doing with Neovim. Some handy articles:

- [Modern source-to-source transformation with Clang and libTooling](http://eli.thegreenplace.net/2014/05/01/modern-source-to-source-transformation-with-clang-and-libtooling/)
- [How Should You Write a Fast Integer Overflow Check?](http://blog.regehr.org/archives/1139)
