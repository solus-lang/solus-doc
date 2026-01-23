# The STD
The std, or standard library, are the functions and globals that are built in to the solus language, but aren't always necessarily available in all solus environments. The standard library is optionally loaded by the C api, and is always loaded in the CLI tool. All values in the global namespace CAN be overridden for now, but it is likely that readonly objects will be added in the future.

## `sol.version`: `str`
The version string of the solus VM you're running currently
## `sol.git`: `str`
The github repository link for solus :)