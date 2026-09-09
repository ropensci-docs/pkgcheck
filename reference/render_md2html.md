# render markdown-formatted input into 'html'

render markdown-formatted input into 'html'

## Usage

``` r
render_md2html(md, open = TRUE)
```

## Arguments

- md:

  Result of
  [checks_to_markdown](https://docs.ropensci.org/pkgcheck/reference/checks_to_markdown.md)
  function.

- open:

  If `TRUE`, open `hmtl`-rendered version in web browser.

## Value

(invisible) Location of `.html`-formatted version of input.

## See also

Other extra:
[`checks_to_markdown()`](https://docs.ropensci.org/pkgcheck/reference/checks_to_markdown.md),
[`fn_names_on_cran()`](https://docs.ropensci.org/pkgcheck/reference/fn_names_on_cran.md),
[`list_pkgchecks()`](https://docs.ropensci.org/pkgcheck/reference/list_pkgchecks.md),
[`logfile_names()`](https://docs.ropensci.org/pkgcheck/reference/logfile_names.md)

## Examples

``` r
if (FALSE) { # \dontrun{
checks <- pkgcheck ("/path/to/my/package")
# Generate standard markdown-formatted character vector:
md <- checks_to_markdown (checks)

# Directly generate HTML output:
h <- checks_to_markdown (checks, render = TRUE) # HTML version

# Or convert markdown-formatted version to HTML:
h <- render_md2html (md)
} # }
```
