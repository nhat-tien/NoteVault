The > operator redirects the output usually to a file but it can be to a device. You can also use >> to append.

If you don't specify a number then the standard output stream is assumed, but you can also redirect errors:

`> file` redirects stdout to file
`1> file` redirects stdout to file

`2> file` redirects stderr to file

`&> file` redirects stdout and stderr to file
`> file 2>&1` redirects stdout and stderr to file

Note that `> file 2>&1` is an older syntax which still works,`&> file` is neater, but would not have worked on older systems.
