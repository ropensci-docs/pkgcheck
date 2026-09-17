# pkgcheck

Check whether a package is ready for submission to
[rOpenSci](https://ropensci.org)’s peer review system. The primary
function,
[`pkgcheck()`](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.html),
collates the output of
[`goodpractice`](https://github.com/ropensci-review-tools/goodpractice),
including `R CMD check` results, a number of statistics via the
[`pkgstats` package](https://github.com/ropensci-review-tools/pkgstats),
and checks for package structure expected for rOpenSci submissions. The
output of this function immediately indicates whether or not a package
is “Ready to Submit”.

## Installation

The easiest way to install this package is via the [associated
`r-universe`](https://ropensci-review-tools.r-universe.dev/#builds). As
shown there, simply enable the universe with

``` r

options (repos = c (
    ropenscireviewtools = "https://ropensci-review-tools.r-universe.dev",
    CRAN = "https://cloud.r-project.org"
))
```

And then install the usual way with,

``` r

install.packages ("pkgcheck")
```

Alternatively, the package can be installed by first installing either
the [remotes](https://remotes.r-lib.org) or
[pak](https://pak.r-lib.org/) packages and running one of the following
lines:

``` r

remotes::install_github ("ropensci-review-tools/pkgcheck")
pak::pkg_install ("ropensci-review-tools/pkgcheck")
```

The package may also be installed from locations other than GitHub, with
any of the following options:

``` r

remotes::install_git ("https://codeberg.org/ropensci-review-tools/pkgcheck")
remotes::install_git ("https://codefloe.com/ropensci-review-tools/pkgcheck")
```

The package can then be loaded for use with:

``` r

library (pkgcheck)
```

## Setup

The [`pkgstats`
package](https://github.com/ropensci-review-tools/pkgstats) also
requires the system libraries [`ctags`](https://ctags.io) and [GNU
`global`](https://www.gnu.org/software/global/) to be installed.
Procedures to install these libraries on various operating systems are
described in a [`pkgstats`
vignette](https://docs.ropensci.org/pkgstats/articles/installation.html).
This package also uses the [GitHub GraphQL
API](https://docs.github.com/v4) which requires a local GitHub token to
be stored with an unambiguous name including `GITHUB`, such as
`GITHUB_TOKEN` (recommended), or `GITHUB_PAT` (for Personal
Authorization Token). This can be obtained from GitHub (via your user
settings), and stored using

``` r

Sys.setenv ("GITHUB_TOKEN" = "<my_token>")
```

This can also be set permanently by putting this line in your
`~/.Renviron` file (or creating this if it does not yet exist). Once
`pkgstats` has been successfully installed, the `pkgcheck` package can
then be loaded via a `library` call:

``` r

library (pkgcheck)
```

## Usage

The package primarily has one function, `pkgcheck`, which accepts the
single argument, `path`, specifying the local location of a git
repository to be analysed. The following code generates a reproducible
report by first downloading a local clone of a repository called
[`srr-demo`](https://github.com/mpadge/srr-demo), which contains the
skeleton of an [`srr` (Software Review Roclets)
package](https://github.com/ropensci-review-tools/srr), generated with
the [`srr_stats_pkg_skeleton()`
function](https://docs.ropensci.org/srr/reference/srr_stats_pkg_skeleton.html):

``` r

mydir <- file.path (tempdir (), "srr-demo")
gert::git_clone ("https://github.com/mpadge/srr-demo", path = mydir)
devtools::document (mydir, quiet = TRUE) # Generate documentation entries in "/man" directory
x <- pkgcheck (mydir)
```

That object has default `print` and `summary` methods. The latter can be
used to simply check whether a package is ready for submission:

``` r

summary (x)
## 
## ── demo 0.0.0.9000 ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
## 
## ✔ Package name is available
## ✖ does not have a 'contributing' file.
## ✖ The following function has no documented return value: [test_fn]
## ✔ uses 'roxygen2'.
## ✔ 'DESCRIPTION' has a URL field.
## ✖ 'DESCRIPTION' does not have a BugReports field.
## ✖ Package has no HTML vignettes
## ✖ These functions do not have examples: [test_fn].
## ✖ Repository has no website
## ✖ Package has no continuous integration checks.
## ✖ Package coverage failed
## ✖ Statistical standards should be documented in most package files, yet are mostly only documented in one file.
## ✔ R CMD check found no errors.
## ✔ R CMD check found no warnings.
## ℹ Some goodpractice linters failed.
## 
## ℹ Current status:
## ✖ Frustration is a natural part of programming :)
## 
## ℹ 'pkgcheck' version: 0.1.3.12
## 
```

A package may only be submitted when the summary contains all ticks and
no cross symbols. (These symbols are colour-coded with green ticks and
red crosses when generated in a terminal; GitHub markdown only renders
them in black-and-white.) The object returned from the `pkgcheck`
function is a complex nested list with around a dozen primary
components. Full information can be obtained by simply calling the
default `print` method by typing the object name (`x`).

To avoid potential namespace conflicts with existing CRAN packages,
`pkgcheck` includes the helper function
[`fn_names_on_cran`](https://docs.ropensci.org/pkgcheck/reference/fn_names_on_cran.html).
You can use this interactively during development to check if your
proposed function names are already in use. This is a useful step to
perform before committing new functions and running a full `pkgcheck`:

``` r

fn_names_on_cran (c ("min", "max"))
```

``` R
##       package version fn_name
## 1    matlab2r   1.5.0     max
## 2    matlab2r   1.5.0     min
## 3 rapportools     1.2     max
## 4 rapportools     1.2     min
## 5      mosaic   1.9.2     max
## 6      mosaic   1.9.2     min
```

## The `pkgcheck` GitHub action

The `pkgcheck` package also has an associated GitHub action in [the
`pkgcheck-action`
repository](https://github.com/ropensci-review-tools/pkgcheck-action).
You can use this action to run `pkgcheck` every time you push commits to
GitHub, just like the `rcmdcheck()` checks which can be installed and
run via [the `usethis::use_github_action_check_standard()`
function](https://usethis.r-lib.org/reference/github_actions.html).
`pkgcheck` includes an analogous function,
[`use_github_action_pkgcheck()`](https://docs.ropensci.org/pkgcheck/reference/use_github_action_pkgcheck.html),
which will download the workflow file defining the action into your
local `.github/workflows` folder. See [the `pkgcheck-action`
repository](https://github.com/ropensci-review-tools/pkgcheck-action)
for more details.

You can also add a `pkgcheck` badge, just like that `rcmdcheck` badge,
that will always reflect the current state of your repository’s
`pkgcheck` results. To add a badge, copy the following line to your
README file, filling in details of the GitHub organization and
repository name (`<org>` and `<repo>`, respectively):

``` markdown
[![pkgcheck](https://github.com/<org>/<repo>/workflows/pkgcheck/badge.svg)](https://github.com/<org>/<repo>/actions?query=workflow%3Apkgcheck)
```

## What is checked?

All current checks are listed in [a separate
vignette](https://docs.ropensci.org/pkgcheck/articles/list-checks.html).

### Summary of Check Results

Calling [`summary()`](https://rdrr.io/r/base/summary.html) on the object
returned by the [`pkgcheck()`
function](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.html)
will generate a checklist like that shown above. This checklist will
also be automatically generated when a package is first submitted to
rOpenSci, and is used by the editors to assess whether to process a
submission. Authors must ensure prior to submission that there are no
red crosses in the resultant list. (In the unlikely circumstances that a
package is unable to pass particular checks, explanations should be
given upon submission about why those checks fail, and why review may
proceed in spite of such failures.)

### Detailed Check Results

Full details of check results can be seen by `print`-ing the object
returned by the [`pkgcheck()`
function](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.html)
(or just by typing the name of this object in the console.)

The package includes an additional function,
[`checks_to_markdown()`](https://docs.ropensci.org/pkgcheck/reference/checks_to_markdown.html),
with a parameter, `render`, which can be set to `TRUE` to automatically
render a HTML-formatted representation of the check results, and open it
in a browser. The formatting differs only slightly from the terminal
output, mostly through the components of
[`goodpractice`](http://docs.ropensci.org/goodpractice/) being divided
into distinct headings, with explicit statements in cases where
components pass all checks (the default screen output inherits directly
from that package, and only reports components which *do not* pass all
checks).

This
[`checks_to_markdown()`](https://docs.ropensci.org/pkgcheck/reference/checks_to_markdown.html)
function returns the report in markdown format, suitable for pasting
directly into a GitHub issue, or other markdown-compatible place. (The
[`clipr` package](https://github.com/mdlincoln/clipr) can be used to
copy this directly to your local clipboard with `write_clip(md)`, where
`md` is the output of
[`checks_to_markdown()`](https://docs.ropensci.org/pkgcheck/reference/checks_to_markdown.md).)

## Caching and running `pkgcheck` in the background

Running the [`pkgcheck`
function](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.html)
can be time-consuming, primarily because the
[`goodpractice`](https://docs.ropensci.org/goodpractice/) component runs
both a full `R CMD check`, and calculates code coverage of all tests. To
avoid re-generating these results each time, `pkgcheck` saves previous
reports to a local cache directory defined in
`Sys.getenv("PKGCHECK_CACHE_DIR")`.

You may manually erase the contents of this `pkgcheck` subdirectory at
any time at no risk beyond additional time required to re-generate
contents. By default checks presume packages use `git` for version
control, with checks updated only when code is updated via `git commit`.
Checks for packages that do not use `git` are updated when any files are
modified.

The first time
[`pkgcheck()`](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.html)
is applied to a package, the checks will be stored in the cache
directory. Calling that function a second time will then load the cached
results, and so enable checks to be returned much faster. For code which
is frequently updated, such as for packages working on the final stages
prior to submission, it may still be necessary to repeatedly call
[`pkgcheck()`](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.html)
after each modification, a step which may still be inconveniently
time-consuming. To facilitate frequent re-checking, the package also has
a [`pkgcheck_bg()`
function](https://docs.ropensci.org/pkgcheck/reference/pkgcheck_bg.html)
which is effectively identical to the main [`pkgcheck()`
function](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.html),
except it runs in the background, enabling you to continue coding while
checks are running.

The [`pkgcheck_bg()`
function](https://docs.ropensci.org/pkgcheck/reference/pkgcheck_bg.html)
returns a handle to the [`callr::r_bg()`
process](https://callr.r-lib.org/reference/r_bg.html) in which the
checks are running. Typing the name of the returned object will
immediately indicate whether the checks are still running, or whether
they have finished. That handle is itself an [`R6`
object](https://r6.r-lib.org/) with a number of methods, notably
including
[`get_result()`](https://callr.r-lib.org/reference/get_result.html)
which can be used to access the checks once the process has finished.
Alternatively, as soon as the background process, the normal
(foreground) [`pkgcheck()`
function](https://docs.ropensci.org/pkgcheck/reference/pkgcheck.html)
may be called to quickly re-load the cached results.

## See Also

[The `checklist` package](https://github.com/inbo/checklist) for
“checking R packages and R code”.

## Code of Conduct

Please note that this package is released with a [Contributor Code of
Conduct](https://ropensci.org/code-of-conduct/). By contributing to this
project, you agree to abide by its terms.

## Contributors

All contributions to this project are gratefully acknowledged using the
[`allcontributors` package](https://github.com/ropensci/allcontributors)
following the [allcontributors](https://allcontributors.org)
specification. Contributions of any kind are welcome!

### Code

[TABLE]

### Issue Authors

[TABLE]

### Issue Contributors

[TABLE]
