compiler-warnings
=================

.. image:: https://travis-ci.org/yi-editor/compiler-warnings.svg?branch=master
    :target: https://travis-ci.org/yi-editor/compiler-warnings

.. image:: https://img.shields.io/hackage/v/yi.svg?maxAge=2592000
    :target: https://hackage.haskell.org/package/yi

.. image:: https://img.shields.io/hackage-deps/v/compiler-warnings.svg?maxAge=2592000

.. image:: http://stackage.org/package/compiler-warnings/badge/lts-7
    :target: http://stackage.org/lts-7/package/compiler-warnings

.. image:: http://stackage.org/package/compiler-warnings/badge/nightly
    :target: http://stackage.org/nightly/package/compiler-warnings

A library for parsing typical human-oriented compiler output like::

  Preprocessing test suite 'tasty' for compiler-warnings-0.1.0...
  [1 of 1] Compiling Main             ( test/Main.hs, .stack-work/dist/x86_64-osx/Cabal-1.24.0.0/build/tasty/tasty-tmp/Main.o )
               
  /Users/ethercrow/src/compiler-warnings/test/Main.hs:(172,1)-(173,120): warning: [-Worphans]
      Orphan instance: instance Arbitrary Warning
      To avoid this
          move the instance declaration to the module of the class or of the type, or
          wrap the type with a newtype and declare the instance on the new type.
  Linking .stack-work/dist/x86_64-osx/Cabal-1.24.0.0/build/tasty/tasty ...
  compiler-warnings-0.1.0: copy/register
  Installing library in
  /Users/ethercrow/src/compiler-warnings/.stack-work/install/x86_64-osx/nightly-2016-10-10/8.0.1/lib/x86_64-osx-ghc-8.0.1/compiler-warnings-0.1.0-HDNNDzMUbqD5QdFxwEItyG
  Registering compiler-warnings-0.1.0...
  compiler-warnings-0.1.0: Test running disabled by --no-run-tests flag.
  Completed 2 action(s).

into something a little bit more structured::

  Text.Warning> parseWarnings thatOutputAbove
  [Warning {cmFilePath = "/Users/ethercrow/src/compiler-warnings/test/Main.hs", cmStartLine = 172, cmStartColumn = 1, cmEndLine = 173, cmEndColumn = 120, cmMessage = " warning: [-Worphans]\n    Orphan instance: instance Arbitrary Warning\n    To avoid this\n        move the instance declaration to the module of the class or of the type, or\n        wrap the type with a newtype and declare the instance on the new type."}]