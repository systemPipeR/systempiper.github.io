---
title: "Developer tools"
linkTitle: "Developer tools"
type: docs
weight: 9
---

SPS is not only a framework to run interactive workflow and visualize data, but 
also a framework with a abundant developer tools for building Shiny apps, writing R markdowns,
integrating R-HTML and general R utilities. 

These developer toolkits are distributed in supporting packages. If you like 
some of the functionality from SPS and think installing the whole framework is 
too expensive (time consuming), cherry-pick the functionality you want in following
categories:

- [**spsCpmps**](./spscomps): Shiny/Rmarkdown UI components, and Shiny server functions.
- [**drawer**](./drawer): Shiny/Rmarkdown/HTML interactive image editing tool.
- [**spsUtil**](./spsutil): General R utilities, like pretty logging functions.


## Install
All these supporting packages are available on CRAN. We recommend to use the 
modern package manager {[pak](https://github.com/r-lib/pak)} to install packages. 


```r
if(!requireNamespace("pak", quietly = TRUE))
  install.packages("pak", repos = "https://r-lib.github.io/p/pak/dev/")
```

Pick and install packages as your need 

```r
pak::pkg_install("spsCpmps")
pak::pkg_install("drawer")
pak::pkg_install("spsUtil")
```

### Linux 

If you are on Linux, you need to install some system dependencies **before** R package
installation. To figure out 
what system dependencies and command, run: 


```r
cat(paste("sudo", pak::pkg_system_requirements("spsComps")), sep = "\n")
```

```
sudo apt-get install -y make
sudo apt-get install -y libicu-dev
```

```r
cat(paste("sudo", pak::pkg_system_requirements("drawer")), sep = "\n")
```

```
sudo apt-get install -y make
sudo apt-get install -y pandoc
sudo apt-get install -y libicu-dev
```

```r
cat(paste("sudo", pak::pkg_system_requirements("spsUtil")), sep = "\n")
```

```
sudo apt-get install -y libcurl4-openssl-dev
sudo apt-get install -y libssl-dev
sudo apt-get install -y libicu-dev
```


<b class = "text-primary">We are rendering this doc in Ubuntu. If your Linux distribution is different, commands above will be different.</b>

## Functions reference manual
In documents, we only highlight some important functions. Please read 
the [reference manuals](/sps/sps_funcs) for details of every function. 





