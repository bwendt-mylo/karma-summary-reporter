# karma-summary-reporter

Show a table detailing the test results for all connected browsers at the end
of a test run. This gives a better overview which browsers are broken than the
output of other reporters.

The plugin is intended to be used in addition to some other reporter that
shows you the error details. This plugin only shows a overview of passed and
failed testcases, no more detailed information:


```
$ karma test-stringfunctions.conf.js
[... error output and detail for example from karma-dot-reporter]
```

## Use cases

### Testing in several browsers

When you test in several browsers, the sequential test output of all the
browsers can be unwieldy to quickly grasp the problems in the tests. The
summary table provided by this reporter shows the failing tests in a
compact format that is easy to grasp at a glance:

```
$ karma start examples/bugs/karma.conf.js
[...]
SUMMARY
 0: Chromium 51.0.2704 (Ubuntu 0.0.0): Executed 3 of 3 (1 FAILED) (0.083 secs / 0.003 secs)
 1: Firefox 48.0.0 (Ubuntu 0.0.0): Executed 3 of 3 (1 FAILED) (0.068 secs / 0.009 secs)
 2: IE 11.0.0 (Windows 7 0.0.0): Executed 3 of 3 (3 FAILED) ERROR (0.014 secs / 0.001 secs)
                                                   all   0  1  2 
  addPrefix()
    should combine both strings                     ✗    ✗  ✗  ✗ 
  stripPrefix()
    should remove the prefix if present             ✗    ✓  ✓  ✗ 
    should do nothing if the prefix isn't present   ✗    ✓  ✓  ✗ 
```

Here we can clearly see that `addPrefix()` has some general problem while
the error in `stripPrefix()` seems to be specific to IE.


### Feature tests

The summary table is also useful if you want to (ab-)use karma to run 
feature tests, like checking which standard string functions are available:

```
$ karma start examples/features/karma.conf.js
[...]
SUMMARY
 0: Firefox 48.0.0 (Ubuntu 0.0.0): Executed 7 of 7 SUCCESS (0.065 secs / 0 secs)
 1: Chromium 51.0.2704 (Ubuntu 0.0.0): Executed 7 of 7 SUCCESS (0.081 secs / 0.013 secs)
 2: IE 11.0.0 (Windows 7 0.0.0): Executed 7 of 7 (6 FAILED) (0.041 secs / 0.001 secs)
                                                   all   0  1  2 
  ES2015 String
    has fromCodePoint()                             ✗    ✓  ✓  ✗ 
  ES2015 String.prototype
    has codePointAt()                               ✗    ✓  ✓  ✗ 
    has endsWith()                                  ✗    ✓  ✓  ✗ 
    has includes()                                  ✗    ✓  ✓  ✗ 
    has repeat()                                    ✗    ✓  ✓  ✗ 
    has startsWith()                                ✗    ✓  ✓  ✗ 
    has trim()                                      ✓    ✓  ✓  ✓ 
```

We can see that IE is lacking some features here.

## Config

Not yet.

