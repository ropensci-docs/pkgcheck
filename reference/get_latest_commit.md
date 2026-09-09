# get_latest_commit

get_latest_commit

## Usage

``` r
get_latest_commit(org, repo, branch = NULL)
```

## Arguments

- org:

  Github organization

- repo:

  Github repository

- branch:

  Branch from which to get latest commit

## Value

Details of latest commit including OID hash

## Note

This returns the latest commit from the default branch as specified on
GitHub, which will not necessarily be the same as information returned
from
[`gert::git_info`](https://docs.ropensci.org/gert/reference/git_repo.html)
if the `HEAD` of a local repository does not point to the same default
branch.

## See also

Other github:
[`get_default_github_branch()`](https://docs.ropensci.org/pkgcheck/reference/get_default_github_branch.md),
[`get_gh_token()`](https://docs.ropensci.org/pkgcheck/reference/get_gh_token.md),
[`use_github_action_pkgcheck()`](https://docs.ropensci.org/pkgcheck/reference/use_github_action_pkgcheck.md)

## Examples

``` r
if (FALSE) { # \dontrun{
org <- "ropensci-review-tools"
repo <- "pkgcheck"
commit <- get_latest_commit (org, repo)
} # }
```
