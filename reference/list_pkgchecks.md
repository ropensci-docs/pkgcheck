# List all checks currently implemented

List all checks currently implemented

## Usage

``` r
list_pkgchecks(quiet = FALSE)
```

## Arguments

- quiet:

  If `TRUE`, print all checks to screen. Function invisibly returns list
  of checks regardless.

## Value

Character vector of names of all checks (invisibly)

## See also

Other extra:
[`checks_to_markdown()`](https://docs.ropensci.org/pkgcheck/reference/checks_to_markdown.md),
[`fn_names_on_cran()`](https://docs.ropensci.org/pkgcheck/reference/fn_names_on_cran.md),
[`logfile_names()`](https://docs.ropensci.org/pkgcheck/reference/logfile_names.md),
[`render_md2html()`](https://docs.ropensci.org/pkgcheck/reference/render_md2html.md)

## Examples

``` r
list_pkgchecks ()
#> ℹ The following checks are currently implemented in pkgcheck:
#> 1. pkgchk_branch_is_master
#> 2. pkgchk_ci_badges
#> 3. pkgchk_fns_have_exs
#> 4. pkgchk_fns_have_return_vals
#> 5. pkgchk_has_bugs
#> 6. pkgchk_has_citation
#> 7. pkgchk_has_contrib_md
#> 8. pkgchk_has_orcid
#> 9. pkgchk_has_ror
#> 10. pkgchk_has_scrap
#> 11. pkgchk_has_url
#> 12. pkgchk_has_vignette
#> 13. pkgchk_left_assign
#> 14. pkgchk_license
#> 15. pkgchk_lintr
#> 16. pkgchk_no_r_subdir
#> 17. pkgchk_num_imports
#> 18. pkgchk_obsolete_pkg_deps
#> 19. pkgchk_on_cran
#> 20. pkgchk_pkgname_available
#> 21. pkgchk_renv_activated
#> 22. pkgchk_repo_has_website
#> 23. pkgchk_repo_not_fork
#> 24. pkgchk_srr_okay
#> 25. pkgchk_unique_fn_names
#> 26. pkgchk_uses_dontrun
#> 27. pkgchk_uses_roxygen2
```
