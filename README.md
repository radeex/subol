Subol
=====

Features
--------

 * Flexible syntax (prefix and infix syntax; indentation-based blocks)

 * AST Macros.

 * Transparently call Subol from Python and vice versa

 * Interactive interpreter for rapid development and experimenting

 * Extremely flexible parsing system

Syntax
------

Optional indent-block syntax

    class Foo ():
        def (greet self):
            (print "hello from" self "!")

I recommend using your editor's Python syntax support instead of a lisp mode, since it will handle the indentation better.

Python/Subol
------------

Subol comes with an import hook that you can install in your sitecustomize.py so that all existing python code can import your Subol code transparently. This means you can have Python packages and module made entirely out of .sub files with rules identical to those of Python: Your packages must have `__init__.{sub,py,so,etc}` files, and can contain more packages or .sub files.

This import hook will add a negligible impact to successful imports of python files on your system, and a bigger impact to imports failing with an ImportError. Three accumulated runs of the command `mktap', an extremely import-heavy script used by Twisted, goes from ~1.0 to ~1.4 seconds on system (The impact on a single run is ~0.3 to ~0.45 seconds) . This is a speed hit of ~40%. However, this is not a general number to be applied to the performance of applications; Almost all imports happen at the start of a program, so this import hook will certainly not decrease the runtime performance of your programs by any noticeable amount.

Reader macros
-------------

You can say `!c fully.qualified.function` to register a reader macro for `c`. That is:

`!`, followed by the character that you want to register the macro for, followed by a space, followed by a fully-qualified function name.

The function should accept a character, a stream, and a result list.

This allows you to have a customized syntax that only your file has to know about. Hooray.

Unit Tests
----------

To prove that the software is Bug Free, run the tests (They require the Twisted testing framework, twisted.trial).

    trial subol.test
