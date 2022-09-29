Exploring what happens when one uses Apkg::Symbol in code in a second package, Bpkg.

+ Is the symbol resolved at installation time?
+ is it byte compiled
+ is it dynamically resolved in each call via ::

We create two simple packages Apkg and Bpkg. (R doesn't like packages with single-letter names.)

```r
library(Bpkg)
trace("::")
b1(10, 20)
```

+ We do need to list it in the Imports field in the DESCRIPTION file.
+ We don't need  to import the Apkg package in the NAMESPACE. 
+ Not listing the symbols that are imported makes it harder to know what packages and what symbols
  from what packages are used.
  + We use static code analysis to find these.
```r
library(Bpkg)
i = CodeAnalysis::getGlobals(b1)
grep("::", i$functions)  # will also find ::: calls.
```


