# Known faults #

Some tests has Windows file system path in .master files and will fault

# Introduction #

NanoLP package contains different tests in `test/` directory. Testing "engine" is based on UnitTest framework, so all test has bound testSOMETHING.py module in it's directory.


# Docstrings tests #

Some modules of `nanolp` package contains docstring based tests (doctests). To run it, do from directory of decompressed source-package:
```
python -m unittest discover -s test/
```
Bound Python module is `testDocStrings.py` in `test/` directory with corresponding config file `lprc`.

# Files tests #

Also there are several directories in the `tests/` (test1, test2, etc.) with file-based tests - for test of parsing, crsoff-reference creation, publishing and so on.

To run them, do:
```
python -m unittest discover -s test/tests
```
**If you need demo files, see tests! Each parsable file (usually they looks like `example.*`, note also relative files, included with `<<use>>` command!) - is also for demonstration or little tutorial.**

Each directory is one or more tests actually. If it's a test of parsing, `example.*` should exist there. Usually test engine try to parse some `example`-file and then to compare all `SOME.master` files with their reflections: considering `SOME` file. Test is successful, if comparision is true.

If there is `*.sh` files, instead of parsing `example` files (running nlp.py tool as `-i EXAMPLE`) command from `sh`-file will be executed.

**So, usually `example.*` files are main "material" for testing (if no `*.sh` files)**.

If exists `*.in` files, they use as original for file with the same name, but without `.in` extension (`SOME.in -> SOME`).

Before to run any test all outputs are deleted, i.e. all files with names like of `*.master` files but without `.master` extension. Usually resulting extension is `.out`, but not always!

Output file may be in different directory with test directory. In this case `master`-file looks like `somedir__somefile.master`, so two underscores `'__'` will be replaced by File System path separator: `'__' -> '/'`, and out file in our example becames: `somedir/somefile` _(directory will be create if not exists)_.

Driver module is still testSOMETHING.py. What really will happens is determined by this Python module.

Each file-based test has own config file - `lprc`. And these `lprc` files usually are different for different tests!