# get_default_github_branch

get_default_github_branch

## Usage

``` r
get_default_github_branch(org, repo)
```

## Arguments

- org:

  Github organization

- repo:

  Github repository

## Value

Name of default branch on GitHub

## Note

This function is not intended to be called directly, and is only
exported to enable it to be used within the plumber API.

## See also

Other github:
[`get_gh_token()`](https://docs.ropensci.org/pkgcheck/reference/get_gh_token.md),
[`get_latest_commit()`](https://docs.ropensci.org/pkgcheck/reference/get_latest_commit.md),
[`use_github_action_pkgcheck()`](https://docs.ropensci.org/pkgcheck/reference/use_github_action_pkgcheck.md)

## Examples

``` r
if (FALSE) { # \dontrun{
org <- "ropensci-review-tools"
repo <- "pkgcheck"
branch <- get_default_github_branch (org, repo)
} # }
```
