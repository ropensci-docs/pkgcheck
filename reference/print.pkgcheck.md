# Generic print method for 'pkgcheck' objects.

Generic print method for 'pkgcheck' objects.

## Usage

``` r
# S3 method for class 'pkgcheck'
print(x, deps = FALSE, ...)
```

## Arguments

- x:

  A 'pkgcheck' object to be printed.

- deps:

  If 'TRUE', include details of dependency packages and function usage.

- ...:

  Further arguments pass to or from other methods (not used here).

## Value

Nothing. Method called purely for side-effect of printing to screen.

## See also

Other pkgcheck_fns:
[`pkgcheck()`](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.md),
[`pkgcheck_bg()`](https://docs.ropensci.org/pkgcheck/reference/pkgcheck_bg.md)

## Examples

``` r
f <- system.file ("extdata", "pkgstats_9.9.tar.gz", package = "pkgstats")
path <- pkgstats::extract_tarball (f)

if (FALSE) { # \dontrun{
checks <- pkgcheck (path)
summary (checks) # print summary only
print (checks) # print full checks, starting with summary
} # }
fs::dir_delete (path)
```
