# `io` Module
This module provides basic input/output capabilities to the solus VM so that you can actually see what your program is doing. This also includes some other system info.

## `io.print(val: any)`
Prints the `str` representation of any value to the console
### Parameters
- `val`: Any valid value in the solus language
### Example
```sol
io.print("Hello!");
```

## `io.println(val: any)`
Prints the `str` representation of any value to the console, followed by a newline character and flush
### Parameters
- `val`: Any valid value in the solus language
### Example
```sol
io.println("Hello, World!");
```

## `io.time()`
Returns the time in seconds since the UNIX epoch
### Returns
- `f64`: Time in seconds since the UNIX epoch, represented as an f64

## `io.fread(path: str)`
Attempts to read a file from the specified path
### Parameters
- `path`: The relative path to the file
### Returns
- `str`: The string contents of the file on success
- `err`: The reason for read failure
### Example
```sol
let f = io.fread("test.cfg");
eval(unwrap(f));
```

## `io.fwrite(path: str, content: str)`
Writes the provided string to a file at the specified path
### Parameters
- `path`: The relative path to the file
### Returns
- `err`: The reason for write failure, if encountered
### Example
```sol
unwrap(io.fwrite("test.cfg", obj.stringify(default, false)));
default
```