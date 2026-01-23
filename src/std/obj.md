# `obj` Module
This module provides functions that allow you to interact with objects without using the built in operators and construction methods. This is useful for non-identifier friendly keys.

## `obj.new()`
Constructs a new object with no members
### Returns
- `obj`: An empty object

## `obj.set(obj: obj, key: str, val: any)`
Sets the object's member at the specified key. Not all keys set this way can be accessed with the postfix `obj.member` operator
### Parameters
- `obj`: The object to call set on
- `key`: The member name to store the value at
- `val`: The value to store at the specified member name
### Example
```sol
let o = {};
obj.set(o, "wow", 1);
io.println(o.wow); // 1
obj.set(o, "Can't do this with . lol", 2);
```

## `obj.set(obj: obj, key: str, val: any)`
Gets the object's member at the specified key. Useful for non identifier friendly member keys
### Parameters
- `obj`: The object to call get on
- `key`: The member name to attempt to get
### Returns
- `any`: If the member exists
- `err`: If the member does not exist
### Example
```sol
let x = obj.get(o, "Can with this :)");
```