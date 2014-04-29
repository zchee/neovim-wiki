## Reference for C programming techniques and Neovim-specific guidance

[`typeof(<var>)` vs `typeof(<type>)`](https://github.com/neovim/neovim/pull/558#discussion_r11767481)
> something you have to be really careful about: the difference between arrays and pointers [...]
> be judicious: if the variable is simple, use `sizeof(variable)`, if the variable is complex, use `sizeof(the_actual_type)`

[conversion of signed variables to unsigned, on files not checked by `-Wconversion`](https://github.com/neovim/neovim/pull/558#issuecomment-40863654)