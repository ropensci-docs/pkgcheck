# Check whether a function name exists in any CRAN packages

Check whether a function name exists in any CRAN packages

## Usage

``` r
fn_names_on_cran(fn_name, force_update = FALSE)
```

## Arguments

- fn_name:

  Character vector of one or more function names to check.

- force_update:

  If 'TRUE', locally-cached data of all function names from all CRAN
  packages will be updated to latest version.

## Value

A `data.frame` of three columns, "package", "version", and "fn_name",
identifying any other packages matching specified function name(s). If
no matches are found, the `data.frame` will have no rows.

## See also

Other extra:
[`checks_to_markdown()`](https://docs.ropensci.org/pkgcheck/reference/checks_to_markdown.md),
[`list_pkgchecks()`](https://docs.ropensci.org/pkgcheck/reference/list_pkgchecks.md),
[`logfile_names()`](https://docs.ropensci.org/pkgcheck/reference/logfile_names.md),
[`render_md2html()`](https://docs.ropensci.org/pkgcheck/reference/render_md2html.md)

## Examples

``` r
fn_names_on_cran (c ("min", "max"))
#>       package version fn_name
#> 1    matlab2r   1.5.0     max
#> 2    matlab2r   1.5.0     min
#> 3 rapportools     1.2     max
#> 4 rapportools     1.2     min
#> 5      tidyna   0.4.0     max
#> 6      tidyna   0.4.0     min
#> 7      mosaic  1.10.2     max
#> 8      mosaic  1.10.2     min
```
