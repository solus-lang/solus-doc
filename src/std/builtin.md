# Builtin Functions
These are the functions that are defined in the global namespace, they have no module prefix and are the core functions of the language, its flow, and error handling.

## `import(path: str)`
Loads a solus file and then executes it. If the file is not found at first and the `.sol` file extension is not provided, it will attempt to find `path + '.sol'`.
### Parameters
- `path`: The path to the solus file. The .sol extension will be attempted automatically if excluded.
### Returns
- `any`: If execution succeeds
- `err`: If the path cannot be found or the execution fails
### Example
```sol
let module = unwrap(import("module"));
if type(module) == "err":
    io.println("Failed to load module.sol");
else:
    io.println(module.version);
```
## `require(path: str)`
Loads a solus file and then executes it, behaving identically to import besides the fact that it panics instead of returning an error.
### Parameters
- `path`: The path to the solus file. The .sol extension will be attempted automatically if excluded.
### Returns
- `any`: If execution succeeds
- `panic`: If the path cannot be found or the execution fails
### Example
```sol
let module = require("notfound"); // This will stop execution!
let mod2 = catch([](){ require("notfound") }); // Same as import("notfound")
```
## `eval(src: str)`
Compiles source code from a string into a `fun`, note that this is NOT sandboxed and is NOT safe to accept use input with. Treat eval very carefully.
### Parameters
- `src`: Solus source code stored in a string
### Returns
- `any`: On successful evaluation
- `err`: On compile error or runtime panic
### Example
```sol
let cat = "{ meows = 2 paws = 4 }";
let instance = eval(cat);
io.println(instance.meows); // 2
```
## `panic(err: str)`
Creates a runtime `panic`, solus' equivalent to an exception pretty much. This will exit the program if it is not DIRECTLY caught.
### Parameters
- `err`: The reason for the runtime panic
### Returns
- `panic`: A fatal error type that exits the program if not caught
### Example
```sol
if fatal_err_condition:
    panic("ohhhh shit!");
```
## `catch(try: fun)`
Catches any `panic`s thrown within the provided try block's scope of execution. Think of this as a try/catch that returns a result instead of passing it.
### Parameters
- `try`:  A function that may panic or return an err
### Returns
- `any`: Whatever the provided try `fun` returns
- `err`: The caught panic if one is thrown, converted to an err
### Example
```sol
let mod = catch([](){ require("notfound") }); // Same as import("notfound")
```
## `attempt(try: fun, handler: fun(err))`
Similar to `catch` except it uses a proper handler `fun`, mimicking try/catch behavior in other languages. If `
### Parameters
- `try`: A function that may panic or return an err
- `handler`: A handler function that optionally accepts the caught panic/returned error as an `err`
### Returns
- `any`: Whatever the provided try `fun` returns if it succeeds, or whatever the provided handler `fun` returns
### Example
```sol
let mod = attempt(
    []() { return import("doesnt-exist.sol"); },
    [](err) { io.println(err); return {}; }
);
```
## `unwrap(val: any)`
Unwraps a variable that is ambiguously value or error, returning either the value or panicking on `err`
### Parameters
- `val`: Either a value or an `err`
### Returns
- `any`: `val` is a valid value
- `panic`: `val` is of type `err`
### Example
```sol
let mod = unwrap(import("")); // Panics on failure like require("")
```
## `unwrap_or(valid: any, invalid: any)`
Returns `valid` if it is a valid value, or returns `invalid` if `valid` is `err`
### Parameters
- `valid`: A value to check the validity of
- `invalid`: The fallback case if `valid` is not
### Returns
- `any`: Either `valid` or `invalid`
### Example
```sol
let cfg = unwrap_or(do {
    let f = io.fread("test.cfg");
    if type(f) == "err": f
    else: eval(f)
}, do {
    unwrap(io.fwrite("test.cfg", obj.stringify(default, false)));
    default
});
```
## `assert(con: bool)`
Throws a `panic` if the provided condition is false
### Parameters
- `con`: Boolean condition
### Example
```sol
assert(1 == 1);
assert(1 == 2); // Panic
```
## `type(val: any)`
Returns the type of a value represented as a string
### Parameters
- `val`: Any value possible in the solus language
### Returns
- `str`: The typename of the value provided
### Example
```sol
let module = unwrap(import("module"));
if type(module) == "err":
    io.println("Failed to load module.sol");
else:
    io.println(module.version);
```

## `()`

## `str(val: any)`
Converts a value of any type into a string representation. Note that this function does not stringify objects, but rather gives a string representation of the pointer.
### Parameters
- `val`: A value of any type.
### Returns
- `str`: A string representation of the value at its most basic.
### Example
```sol
let x = 4; // i64
let y = {}; // obj
io.println("x: " + str(x) + ", y: " + str(y)); // "x: 4, y: 0x71d00c0d8"
```
## `err(str: str)`
Constructs an `err` type from a `str`. You can return this to represent failure conditions.
### Parameters
- `str`: The reason of error or failure condition
### Returns
- `err`: An error or failure condition internally represented by a string
### Example
```sol
let fun = [](bool) {
    if bool: "success"
    else: err("failure!")
};
```
## `i64(f64: f64)`
Converts an f64 value into the i64 equivalent value. This will result in loss of floating point (decimal) precision.
### Parameters
- `f64`: An f64 value to be converted into i64
### Returns
- `i64`: The i64 equivalent to the f64 value provided
## `f64(i64: i64)`
Converts an i64 value into the f64 equivalent value. Not all values i64 represents can be represented by f64 accurately.
### Parameters
- `i64`: An f64 value to be converted into i64
### Returns
- `f64`: The f64 equivalent to the i64 value provided
