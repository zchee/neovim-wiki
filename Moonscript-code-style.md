We still don't have a tool for enforcing a particular code style but contributors writing moonscript code are encouraged to follow these rules:

- Indent using 2 spaces
- No parenthesis for function calls. Functions without parameters can be called by appending a '!' to the name.
- Wrap function call expressions into parenthesis whenever:
  - It's not obvious when the call ends
  - You are accessing a property of the object returned by the expression

eg:
```moonscript
io.open (normalize_fname name), (normalize_mode 'w')
(io.open f1, 'w').close!
```

     

