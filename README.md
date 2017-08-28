adiff - wordwise diff
=====================

This tool is a replacement for GNU wdiff that provides the ability to generate context and unified diffs based on the wordwise diff. It's written in Perl instead of C, so it's both shorter and slower. It doesn't have as many options as wdiff, but it provides some others. 

Example
-------

Consider the standard placeholder text:

    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
    incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
    nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
    Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu
    fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
    culpa qui officia deserunt mollit anim id est laborum.

Let's remove a few words near the top and add a few words near the bottom, then look at a unified diff:

    $ diff -u 1.txt 2.txt
    @@ -1,6 +1,6 @@
     Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
    -incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
    -nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
    -Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu
    -fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
    -culpa qui officia deserunt mollit anim id est laborum.
    +incididunt ut labore. Ut enim ad minim veniam, quis nostrud exercitation ullamco
    +laboris nisi ut aliquip ex ea commodo consequat.  Duis aute irure dolor in
    +reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    +Excepteur foo bar baz quux sint occaecat cupidatat non proident, sunt in culpa
    +qui officia deserunt mollit anim id est laborum.

That isn't very helpful. Here's the adiff unified output:

    $ adiff -u 1.txt 2.txt
    @@ -1,6 +1,6 @@
     Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
    -incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco
    +incididunt ut labore. Ut enim ad minim veniam, quis nostrud exercitation ullamco
     laboris nisi ut aliquip ex ea commodo consequat.  Duis aute irure dolor in
     reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    -Excepteur sint occaecat cupidatat non proident, sunt in culpa
    +Excepteur foo bar baz quux sint occaecat cupidatat non proident, sunt in culpa
     qui officia deserunt mollit anim id est laborum.

And here's the standard adiff output which mimics wdiff output:

    $ adiff 1.txt 2.txt
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
    incididunt ut [-labore et dolore magna aliqua.-]{+labore.+} Ut enim ad minim veniam, quis nostrud exercitation ullamco
    laboris nisi ut aliquip ex ea commodo consequat.  Duis aute irure dolor in
    reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    Excepteur {+foo bar baz quux+} sint occaecat cupidatat non proident, sunt in culpa
    qui officia deserunt mollit anim id est laborum.

