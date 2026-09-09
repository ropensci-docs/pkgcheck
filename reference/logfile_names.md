# Set up stdout & stderr cache files for `r_bg` process

Set up stdout & stderr cache files for `r_bg` process

## Usage

``` r
logfile_names(path)
```

## Arguments

- path:

  Path to local repository

## Value

Vector of two strings holding respective local paths to `stdout` and
`stderr` files for `r_bg` process controlling the main
[pkgcheck](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.md)
function when executed in background mode.

## Note

These files are needed for the callr `r_bg` process which controls the
main
[pkgcheck](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.md).
The `stdout` and `stderr` pipes from the process are stored in the cache
directory so they can be inspected via their own distinct endpoint
calls.

## See also

Other extra:
[`checks_to_markdown()`](https://docs.ropensci.org/pkgcheck/reference/checks_to_markdown.md),
[`fn_names_on_cran()`](https://docs.ropensci.org/pkgcheck/reference/fn_names_on_cran.md),
[`list_pkgchecks()`](https://docs.ropensci.org/pkgcheck/reference/list_pkgchecks.md),
[`render_md2html()`](https://docs.ropensci.org/pkgcheck/reference/render_md2html.md)

## Examples

``` r
if (FALSE) { # \dontrun{
logfiles <- logfiles_namnes ("/path/to/my/package")
print (logfiles)
} # }
```
