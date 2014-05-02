### C programming techniques and Neovim-specific guidance

[`typeof(<var>)` vs `typeof(<type>)`](https://github.com/neovim/neovim/pull/558#discussion_r11767481)
> something you have to be really careful about: the difference between arrays and pointers [...]
> be judicious: if the variable is simple, use `sizeof(variable)`, if the variable is complex, use `sizeof(the_actual_type)`

[Conversion of signed variables to unsigned (in files not checked by `-Wconversion`)](https://github.com/neovim/neovim/pull/558#issuecomment-40863654)

#### Types

(to be filled in)

##### Unsigned or signed? Beware of integer over- and underflow

There are a few very important things to keep in mind while choosing between signed and unsigned integral types:

Firstly, **Unsigned overflow is undefined**, while **signed overflow is defined**. This is an unfortunate historical oversight stemming from a time where it wasn't sure what [representation a signed integer would have](http://stackoverflow.com/questions/18195715/why-is-unsigned-integer-overflow-defined-behavior-but-signed-integer-overflow-is). The C standard decided that it shouldn't/couldn't specify what would happen when a signed integer overflows, because each representation would have different behaviour. In modern times, signed integers are always represented in [two's complement](http://en.wikipedia.org/wiki/Two's_complement) form, which has many advantages. 

What does this mean, defined vs. undefined? If an unsigned integer overflows, it wraps around back to zero (it's modulo addition), if a signed integer overflows, $deity only knows what will happen. More specifically: we _know_ what would happen if a two's complement signed integer would overflow, but [the compiler can do whatever it wants, because the standard says it is undefined](http://stackoverflow.com/a/18195756/558819). As a consequence, an optimizing compiler will often assume that a signed integer _cannot_ overflow (please insert mahkoh's undefined behaviour example here) and optimize out some if-branches or comparisons. This behaviour can cause loops to run forever. Note that if the conditions are not written carefully, even the well-defined wraparound overflow of unsigned integers can cause non-terminating loops, `(U)INTX_MAX/MIN` are your friends.

**Conclusion**: 

- if there is any chance of overflow, use unsigned arithmetic and guards, at least it is defined.
- if there is any chance of underflow, use signed arithmetic and even stronger guards.
- if there is a chance of both underflow and overflow, be extremely careful and paranoid (guards/asserts).

###### Guarded casting

##### Fixed-size vs. generic types

Should we use `(u)intX_t` and friends over `char`, `short`, `int`, `long` et al.? ...

### Tools

There are handy tools that can help while creating, maintaining and transforming a codebase, as we are doing with Neovim. Some handy articles:

- [Modern source-to-source transformation with Clang and libTooling](http://eli.thegreenplace.net/2014/05/01/modern-source-to-source-transformation-with-clang-and-libtooling/)
- [How Should You Write a Fast Integer Overflow Check?](http://blog.regehr.org/archives/1139)
