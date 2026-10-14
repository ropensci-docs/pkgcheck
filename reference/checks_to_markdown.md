# Convert checks to markdown-formatted report

Convert checks to markdown-formatted report

## Usage

``` r
checks_to_markdown(checks, render = FALSE)
```

## Arguments

- checks:

  Result of main
  [pkgcheck](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.md)
  function

- render:

  If `TRUE`, render output as `html` document and open in browser.

## Value

Markdown-formatted version of check report

## See also

Other extra:
[`fn_names_on_cran()`](https://docs.ropensci.org/pkgcheck/reference/fn_names_on_cran.md),
[`list_pkgchecks()`](https://docs.ropensci.org/pkgcheck/reference/list_pkgchecks.md),
[`logfile_names()`](https://docs.ropensci.org/pkgcheck/reference/logfile_names.md),
[`render_md2html()`](https://docs.ropensci.org/pkgcheck/reference/render_md2html.md)

## Examples

``` r
f <- system.file ("extdata", "pkgstats_9.9.tar.gz", package = "pkgstats")
path <- pkgstats::extract_tarball (f)

if (FALSE) { # \dontrun{
checks <- pkgcheck (path, goodpractice = FALSE)
md <- checks_to_markdown (checks) # markdown-formatted character vector
md <- checks_to_markdown (checks, render = TRUE) # HTML version
} # }
fs::dir_delete (path)
```
