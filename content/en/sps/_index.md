---
title: "systemPipeShiny Documentation"
linkTitle: "systemPipeShiny"
type: docs
---

<link href="/css/home_page.css" rel="stylesheet">
<div id="svg-logo"></div>

<script src="/js/home_page.js"></script>
<script>
  loadLogo("/images/sps_logos.svg")
</script>
<style>
#svg-logo {
  background: 
    radial-gradient(circle, transparent 0%,  rgba(255,255,255,1) 30%),
    linear-gradient(to right, var(--color), var(--color)), var(--image2);
  background-repeat: no-repeat;
  background-size: auto 1200px;
  background-position: center center;
  background-blend-mode: 
    var(--blend-top, normal),
    var(--blend-bottom, saturation),
    normal;
  --image2: url("/background.jpg");
  --color-v: rgba(76,169,237,1);
  --color: rgba(76,169,237,1);
}

#svg-logo svg {
  margin: 0 auto;
  display: block;
  padding: 50px;
}
</style>



**<span style="color:#5DA7D6;">s</span>ystem<span
style="color:#5DA7D6;">P</span>ipe<span style="color:#5DA7D6;">S</span>hiny**
(SPS) extends the widely used [systemPipeR](/spr/) 
(SPR) workflow
environment with a versatile graphical user interface provided by a [Shiny
App](https://shiny.rstudio.com). This allows non-R users, such as
experimentalists, to run many systemPipeR's workflow designs, control, and
visualization functionalities interactively without requiring knowledge of R.
Most importantly, `SPS` has been designed as a general purpose framework for
interacting with other R packages in an intuitive manner. Like most Shiny Apps,
SPS can be used on both local computers as well as centralized server-based
deployments that can be accessed remotely as a public web service for using
SPR's functionalities with community and/or private data. The framework can
integrate many core packages from the R/Bioconductor ecosystem. Examples of
SPS' current functionalities include: 

- A default interactive workflow module to 
create experimental designs, visualize and customize workflow topologies with previews, and 
programming free workflow execution within the application. 
- An interactive module with extensive plot options to visualize downstream analysis of a RNA-Seq workflow.
- A quick ggplot module to make all variety of scientific plots from any user defined 
tabular data. 
- An extendable set of visualization functionalities makes it easy to design 
custom Shiny Apps under SPS framework without any knowledge of Shiny. 
- A 'Canvas Workbench' to manage complex visual results. It allows users to 
organize and to compare plots in an efficient manner combined
with a session screenshot feature to edit scientific and publishable figures. 
- Three other supporting packages to help all users from beginners and advanced developers 
to extend under current SPS framework or on their own visualization apps. 

## Demo
View our online demo app:

<a 
href="https://tgirke.shinyapps.io/systemPipeShiny/" 
style="background-color: #eee;border-radius: 10px;border: #c2daf7f5 solid 4px; font-weight: 800; font-size: 1.5rem; margin-left: 40%">
Try a demo!
</a>

## Other packages in systemPipeShiny

| Package | Description | Documents | Function reference | Demo |
| --- | --- | --- | :---: | --- |
|<img src="https://github.com/systemPipeR/systemPipeR.github.io/blob/main/static/images/sps_small.png?raw=true" align="right" height="30" width="30"/>[systemPipeShiny](https://github.com/systemPipeR/systemPipeShiny) | SPS main package |[website](https://systempipe.org/sps/)|[link](https://systempipe.org/sps/funcs/sps/reference/)  | [demo](https://tgirke.shinyapps.io/systemPipeShiny/)|
|<img src="https://github.com/systemPipeR/systemPipeR.github.io/blob/main/static/images/spscomps.png?raw=true" align="right" height="30" width="30" />[spsComps](https://github.com/lz100/spsComps) | SPS UI and server components |[website](https://systempipe.org/sps/dev/spscomps/)|[link](https://systempipe.org/sps/funcs/spscomps/reference/)  | [demo](https://lezhang.shinyapps.io/spsComps)|
|<img src="https://github.com/systemPipeR/systemPipeR.github.io/blob/main/static/images/drawer.png?raw=true" align="right" height="30" width="30" />[drawer](https://github.com/lz100/drawer) | SPS interactive image editing tool |[website](https://systempipe.org/sps/dev/drawer/)|[link](https://systempipe.org/sps/funcs/drawer/reference/)  | [demo](https://lezhang.shinyapps.io/drawer)|
|<img src="https://github.com/systemPipeR/systemPipeR.github.io/blob/main/static/images/spsutil.png?raw=true" align="right" height="30" width="30" />[spsUtil](https://github.com/lz100/spsUtil) | SPS utility functions |[website](https://systempipe.org/sps/dev/spsutil/)|[link](https://systempipe.org/sps/funcs/spsutil/reference/)  | NA|
