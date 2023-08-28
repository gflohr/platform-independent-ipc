# io-multiplexing

Example for platform-independent IO-multiplexing

## Additional Information

This repository illustrates the information of the blog post at
http://www.guido-flohr.net/multiplexing-child-process-i-o-on-windows/.

Source code is provided for Perl and C.

## Building

The source code provided here is not meant to be installed but you should
build and run it locally.

### Perl

The repository does not have any other dependencies than Perl itself.  Open a
terminal and run:

```sh
$ perl parent.pl
Running forever, hit CTRL-C to stop.
[child 69554][info]: child pid 69554 writing to stdout before sleeping 2261943 μs.
[child 69555][info]: child pid 69555 writing to stdout before sleeping 858209 μs.
[child 69556][info]: child pid 69556 writing to stdout before sleeping 2370161 μs.
[child 69555][info]: child pid 69555 writing to stderr before sleeping 2860666 μs.
...
```

This will launch the script `parent.pl` which in turn starts the script
`child.pl` three times.  Standard output and standard error of all child
processes is piped back into the parent process which logs it to its own
standard output, whenever a full line of output is read.

Compare that to the output of running a child process standalone:

```sh
$ perl child.pl
child pid 71879 writing to stdout before sleeping 460897 μs.
child pid 71879 writing to stderr before sleeping 1832933 μs.
child pid 71879 writing to stdout before sleeping 874834 μs.
child pid 71879 writing to stderr before sleeping 2937516 μs.
...
```

The child processes write these lines to standard output and standard error
respectively, before sleeping a random period of time between 0 and 3 seconds.

### C

The same example is provided in C.  If you have `make`, you can just do:

```sh
$ make
```

This creates the two executables `parent` and `child` (or `parent.exe` and
`child.exe` on MS-DOS).

You can run these executables just like the Perl scripts described above.  The
output is identical (except for the process IDs).

If your system lacks `make` but has a C compiler, you can also compile the
two executables manually:

```sh
$ cc parent.c
$ cc child.c
```

Replace `cc` with the path to your C compiler if `cc` cannot be found.