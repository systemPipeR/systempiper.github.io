---
title: "Quick start"
linkTitle: "Quick start"
type: docs
weight: 3
---

# SPS example usage 

To start with SPS after installation:

## Load package

Load the `systemPipeShiny` package in your R session.


```r
library(systemPipeShiny)
## Loading required package: shiny
## Loading required package: spsUtil
## Loading required package: spsComps
## Loading required package: drawer
```

## Initialize `SPS` project

Before launching the `SPS` application, a project environment needs to be created with the
following command.


```r
spsInit()
```

For this demo, the project directory structure is written to a temporary
directory on a user's system. For a real project, it should be written to a
defined and user controlled location on a system rather than a temporary
directory.


```r
sps_tmp_dir <- tempdir()
spsInit(app_path = sps_tmp_dir, change_wd = FALSE, project_name = "SPSProject")
## [SPS-INFO] 2021-12-14 23:53:38 Start to create a new SPS project
## [SPS-INFO] 2021-12-14 23:53:38 Create project under /tmp/RtmpGAaU3K/SPSProject
## [SPS-INFO] 2021-12-14 23:53:38 Now copy files
## [SPS-INFO] 2021-12-14 23:53:38 Create SPS database
## [SPS-INFO] 2021-12-14 23:53:38 Created SPS database method container
## [SPS-INFO] 2021-12-14 23:53:38 Creating SPS db...
## [SPS-DANGER] 2021-12-14 23:53:38 Done, Db created at '/tmp/RtmpGAaU3K/SPSProject/config/sps.db'. DO NOT share this file with others or upload to open access domains.
## [SPS-INFO] 2021-12-14 23:53:38 Key md5 90499a61aeea98b338debf236bd5aef4
## [SPS-INFO] 2021-12-14 23:53:38 SPS project setup done!
sps_dir <- file.path(sps_tmp_dir, "SPSProject")
```

### SPS project structure

The file and directory structure of an SPS project is organized as follows. 

<pre>
SPS_xx/  
├── server.R               <span class="text-success">|</span> 
├── global.R               <span class="text-success">| Most important server, UI and global files, unless special needs, `global.R` is the only file you need to edit manually</span>   
├── ui.R                   <span class="text-success">|</span>  
├── deploy.R               <span class="text-info">| Deploy helper file</span>  
├── config                 <span class="text-success">| Important app config files. Do not edit them by hand if you don't know</span>  
│   ├── sps.db             <span class="text-gray">| SPS database</span> 
│   ├── sps_options.yaml   <span class="text-gray">| SPS default option list</span> 
│   └── tabs.csv           <span class="text-gray">| SPS tab registration information</span> 
├── data                   <span class="text-primary">| App example data files</span> 
│   ├── xx.csv             
├── R                      <span class="text-primary">| All SPS additional tab files, helper R function, interactive guides files</span> 
│   ├── tab_xx.R            
├── README.md              
├── results                <span class="text-gray">| Not in use for this current version, but you can store some data been generated from the app</span> 
│   └── README.md          
└── www                    <span class="text-primary">| Internet resources</span>  
    ├── css                <span class="text-info">| CSS files</span>  
    │   └── sps.css         
    ├── img                <span class="text-info">| App image resources</span>    
    │   └── xx.png         
    ├── js                 <span class="text-info">| Javascripts</span>
    │   └── xx.js           
    ├── loading_themes     <span class="text-info">| Loading screen files</span> 
    │   └── xx.html         
    └── plot_list          <span class="text-info">| Image files for custom visualization tab thumbnails</span>  
        └── plot_xx.jpg      
</pre>

## Launch `SPS` 

By default, the working directory will be set inside the project folder automatically. 
To launch the `SPS` Shiny application, one only needs to execute the following command.


```r
shiny::runApp()
```

Alternatively, when using RStudio one can click the <img src=../img/app_start.png style="display: inline;
padding-left:0; width:10px; height:15px;">`Run App` button in the top right corner.

After the SPS app has been launched, clicking the "Continue to app" button
on the welcome screen will open the main dashboard (Fig.2).



<center id="sps_ui">

![sps_ui](/sps/img/main_app.png)

</center>

**Figure 2A:** SPS welcome page

Click on one of the big icons on the welcome page to choose for the module/tool 
you want to use, or use the lefe sidebar to navigate to different tabs. 

## SPS tabs

Within the functional categories, `SPS` functions are modularized into
sub-components, here referred to as **SPS tabs** that are similar to 
menu tabs in other GUI applications that organize related and inter-connected 
functionalies into groups. On the backend, **SPS tabs** are based on [Shiny modules](https://shiny.rstudio.com/articles/modules.html), 
that are stored in separate files. This modular structure is highly extensible 
and greatly simplifies the design of new `SPS` tabs by both users and/or developers. 
Details about extending existing tabs and designing new ones are provided in 
[Manage tabs section on our website](https://systempipe.org/sps/adv_features/tabs/). 


<center id="sps_ui">

![sps_ui](../img/sps_ui_main.jpg)

</center>

**Figure 2B:** Screenshot of SPS' tabs.

1. Welcome screen.
2. Module tabs.
3. User defined custom tabs.
4. The Canvas tab.
5. All SPS tabs has this description on top. It is highly recommend to click here 
   to expand and read the full the description for the first time.


In addition, in Rstudio the *global.R* file will be automatically
opened when the `SPS` project is created. Custom changes can be made inside this file
before the app launches. Later we will discuss how to change and create new custom tabs 
and change other settings in [advanced sections](../adv_features).
