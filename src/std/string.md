# `string` Module
This module provides functions for manipulating `str` types. Note that strings in solus can be concatenated using the same `+` operator as any other value, which is why there is no `string.cat(a, b)`!

## `string.sub(str: str, start: i64, end: i64)`
Returns a substring using the specified start and end. End must not be before start, and both indices are clamped
### Parameters
- `str`: The string to slice
- `start`: The start index (starting at 0)
- `end`: The end index
### Returns
- `str`: The substring, which may be empty

## `string.len(str: str)`
Returns the length of a string
### Parameters
- `str`: The string to get the length of
### Returns
- `i64`: The length of the string, in characters