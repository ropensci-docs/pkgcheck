# Get GitHub token

Get GitHub token

## Usage

``` r
get_gh_token(token_name = "")
```

## Arguments

- token_name:

  Optional name of token to use

## Value

The value of the GitHub access token extracted from environment
variables.

## See also

Other github:
[`get_default_github_branch()`](https://docs.ropensci.org/pkgcheck/reference/get_default_github_branch.md),
[`get_latest_commit()`](https://docs.ropensci.org/pkgcheck/reference/get_latest_commit.md),
[`use_github_action_pkgcheck()`](https://docs.ropensci.org/pkgcheck/reference/use_github_action_pkgcheck.md)

## Examples

``` r
if (FALSE) { # \dontrun{
token <- get_gh_token ()
} # }
```
