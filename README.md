## About ##

|            |                           |  
| ---------- | ------------------------- |  
| Title:     | libCoreUtilities        |  
| Author:    | Fletcher T. Penney       |  
| Date:      | 2020-04-11 |  
| Copyright: | Copyright © 2020 Fletcher T. Penney.    |  
| Version:   | 1.0.0      |  


## What is this? ##

Many of my projects, open-source and commercial, deal with text in one way or
another.  One of the first files created was `GString.c`, which was initially
written by Daniel Jalkut as a way to remove the dependency that
`peg_multimarkdown` had on `GLib`.  It was an enormous library to link to in
order to have a dynamic string functionality.  (It was part of the initial
`peg_markdown` by John MacFarlane.)

Over the years I have tweaked `GString.c` and migrated it to `d_string.c`, and
it has been used in many of my projects.

`char.c` came about while developing MultiMarkdown version 6.  I needed some
fast routines to check character types.  It has also come in handy in several
other projects.

`stack.c` was also developed for MultiMarkdown v 6.  I needed a dynamic array
structure for several areas of code, so I created a reusable one.  It has also
found it's way in many of my projects.

These files may not be better than any other similar files out there.  They
may even be worse.  But, most importantly, they are *mine*.  I wrote them
(with help from internet searches of course), so I understand how they work
and can easily modify them for new functionality as needed.  You may or may
not find them useful.  But if so, feel free.

You can either copy the files to your project, or include this entire project
as a static (or dynamic) library and access them that way.  I will be
migrating my projects to include this as a git submodule, and link to the
files that way, so that I can centralize any fixes/improvements I make. 
(Keeping the files in sync across multiple projects was becoming quite a pain
in the neck...)

All I ask is that you give proper attribution if you use them.

If you have improvements, send pull requests (vs the develop branch) and I
will look at them.


Thanks!



## How to build ##

### macOS ###

You can automatically build Xcode projects:

*	`make xcode` -- regular build
*	`make xcode-test` -- build `run_tests` to perform CuTest unit tests

The Xcode projects can then be opened in Xcode, or you can build from
the command line via `xcodebuild`.


### Other ###

*	`make` -- regular build
*	`make-test` -- build `run_tests` to perform CuTest unit tests

These steps configure a build directory, but you still have to perform
the actual compilation.  Once you perform either step above, `cd build`
or `cd build-test` and then `make` (and `./run_tests` or `ctest` or
`make test` for the unit testing variant).


### Rebuilding `char.c` ###

The lookup table near the top of `char.c` is generated via the `char_lookup`
program:

	gcc char_lookup.c
	./a.out

This (or the equivalent on your system), rebuilds the lookup table that can
then replace the one in the `char.c` file, should you need to modify things,
or add new functionality.

To keep things small, this only provides lookup for ASCII characters, not
UTF-8 or the like.  That would require a much more complex library.  This is
designed as a lightweight tool for quick lookups for common characters.  It is
useful when parsing MultiMarkdown, as well as in some other text based
projects I have developed.

There is an option to add some characteristics for extended ASCII characters, 
but this turned out not to work well with UTF-8, so I don't use it any more. 
You need to compile with `USE_EXTENDED_ASCII` defined.  You'll need to test
these features if you use this option.

Your mileage may vary.


## License ##

	MIT License
	
	Copyright (c) 2020 Fletcher T. Penney
	
	Permission is hereby granted, free of charge, to any person obtaining a copy
	of this software and associated documentation files (the "Software"), to deal
	in the Software without restriction, including without limitation the rights
	to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
	copies of the Software, and to permit persons to whom the Software is
	furnished to do so, subject to the following conditions:
	
	The above copyright notice and this permission notice shall be included in all
	copies or substantial portions of the Software.
	
	THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
	IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
	FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
	AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
	LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
	OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
	SOFTWARE.
