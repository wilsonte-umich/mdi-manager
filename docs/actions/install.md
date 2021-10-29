---
title: install
parent: R_Commands
has_children: false
nav_order: 1
---

<!-- FILE GENERATED BY document.R - DO NOT EDIT MANUALLY -->

# `install`

Install Michigan Data Interface (MDI) dependencies


## Description

Install all dependencies of the Michigan Data Interface (MDI).
 This will include Bioconductor's BiocManager and its child packages.


## Usage

```r
install(
  mdiDir = "~",
  installApps = TRUE,
  gitUser = NULL,
  token = NULL,
  clone = TRUE,
  cranRepo = "https://repo.miserver.it.umich.edu/cran/",
  packages = NULL,
  force = FALSE,
  ondemand = FALSE
)
```


## Arguments

Argument      |Description
------------- |----------------
`mdiDir`     |     character. Path to the directory where the MDI will be/has been installed. Defaults to your home directory.
`installApps`     |     logical vector. If TRUE (the default), `mdi::install()` will install both Stage 1 pipelines and Stage 2 apps for use on the computer or server. If you know you will only want to use Stage 1 pipelines from an installation, setting `installApps`  to FALSE will skip the much slower installation of the R packages library.
`gitUser`     |     character. Developers should use `gitUser` to provide the username of the GitHub account that holds their forks of any frameworks or suites repositories. Code editing is done in these forks, which will be cloned locally into frameworks/developer-forks and/or suites/developer-forks and used by `mdi::develop()` instead of the upstream repos, when available.
`token`     |     character. The GitHub Personal Access Token (PAT) that grants permissions for accessing forked repositories in the `gitUser` account, and/or any tool suites that have restricted access. You can also preset the token into environment variable `GITHUB_PAT` using `Sys.setenv(GITHUB_PAT = "your_token")` .
`clone`     |     logical. If TRUE (the default), the apps and pipelines code repositories will be cloned anew from GitHub if they do not already exist, or they will be pulled from the server to update a repository if they have been cloned previously. Developers might want to set this option to FALSE.
`cranRepo`     |     character. The base URL of the R repository to use, e.g., the URL of a CRAN mirror. Defaults to the University of Michigan CRAN mirror.
`packages`     |     character vector. If not NULL (the default), only install these specific R packages (for developers to quickly update selected packages). No other actions will be taken and the library's installation.rds file will not be updated.
`force`     |     logical.  When FALSE (the default), `mdi::install()`  does not attempt to update R packages that have previously been installed, regardless of version. When TRUE, all packages are installed without further prompting.
`ondemand`     |     logical. If TRUE, the installer will not install _any_ R packages, as they will be used from the managed host installation. Default is FALSE.


## Details

All default settings are consistent with an end user running the
 MDI in local mode on their desktop or laptop computer.
 
 `mdiDir` must already exist, it will not be created.
 
 If `mdiDir` ends with '/mdi' it will be used as is
 without prompting. Otherwise, a subdirectory of that name will be
 created in `mdiDir` after prompting for confirmation.
 
 If they do not already exist, `mdi::install()` will create a series of
 subdirectories in `mdiDir` without prompting, as follows:
   

*  data = project-specific input and output files  

*  environments = conda environments used by data analysis pipelines  

*  frameworks = git repositories with common code for all pipelines and apps  

*  library = version-controlled library of R packages private to the MDI  

*  resources = version-controlled ~static files such as reference data sets  

*  sessions = temporary files associated with user web sessions  

*  suites = git repositories with code that defines specific pipelines and apps 
 
 As an alternative to using `gitUser` and `token` , developers and
 users can also create script 'gitCredentials.R' in `mdiDir` , with the
 following contents:
 Sys.setenv(GIT_USER = "xxxx")
 Sys.setenv(GITHUB_PAT = "xxxx")


## Value

a list of installation data with names components 'versions', dirs',
 'repos', 'rRepos', 'packages'. This information will be incomplete if
 `packages` was not NULL (repos and rRepos will be NULL, packages will
 only contain `packages` ) or if installApps was FALSE (repos, rRepos and
 packages will all be NULL).

