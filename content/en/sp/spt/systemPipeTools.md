---
title: "Data Visualizations" 
author: "Author: Daniela Cassol (danielac@ucr.edu) and Thomas Girke (thomas.girke@ucr.edu)"
date: "Last update: 05 May, 2021" 
output:
  BiocStyle::html_document:
    toc_float: true
    code_folding: show
  BiocStyle::pdf_document: default
package: systemPipeTools
vignette: |
  %\VignetteEncoding{UTF-8}
  %\VignetteIndexEntry{systemPipeTools: Data Visualizations}
  %\VignetteEngine{knitr::rmarkdown}
fontsize: 14pt
bibliography: bibtex.bib
type: docs
weight: 1
---

<script src="/rmarkdown-libs/htmlwidgets/htmlwidgets.js"></script>
<script src="/rmarkdown-libs/jquery/jquery.min.js"></script>
<link href="/rmarkdown-libs/datatables-css/datatables-crosstalk.css" rel="stylesheet" />
<script src="/rmarkdown-libs/datatables-binding/datatables.js"></script>
<link href="/rmarkdown-libs/dt-core/css/jquery.dataTables.min.css" rel="stylesheet" />
<link href="/rmarkdown-libs/dt-core/css/jquery.dataTables.extra.css" rel="stylesheet" />
<script src="/rmarkdown-libs/dt-core/js/jquery.dataTables.min.js"></script>
<link href="/rmarkdown-libs/dt-ext-fixedcolumns/css/fixedColumns.dataTables.min.css" rel="stylesheet" />
<script src="/rmarkdown-libs/dt-ext-fixedcolumns/js/dataTables.fixedColumns.min.js"></script>
<link href="/rmarkdown-libs/dt-ext-scroller/css/scroller.dataTables.min.css" rel="stylesheet" />
<script src="/rmarkdown-libs/dt-ext-scroller/js/dataTables.scroller.min.js"></script>
<link href="/rmarkdown-libs/crosstalk/css/crosstalk.css" rel="stylesheet" />
<script src="/rmarkdown-libs/crosstalk/js/crosstalk.min.js"></script>
<script src="/rmarkdown-libs/htmlwidgets/htmlwidgets.js"></script>
<script src="/rmarkdown-libs/plotly-binding/plotly.js"></script>
<script src="/rmarkdown-libs/typedarray/typedarray.min.js"></script>
<script src="/rmarkdown-libs/jquery/jquery.min.js"></script>
<link href="/rmarkdown-libs/crosstalk/css/crosstalk.css" rel="stylesheet" />
<script src="/rmarkdown-libs/crosstalk/js/crosstalk.min.js"></script>
<link href="/rmarkdown-libs/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="/rmarkdown-libs/plotly-main/plotly-latest.min.js"></script>
<style type="text/css">
pre code {
white-space: pre !important;
overflow-x: scroll !important;
word-break: keep-all !important;
word-wrap: initial !important;
}
</style>
<script type="text/javascript">
document.addEventListener("DOMContentLoaded", function() {
  document.querySelector("h1").className = "title";
});
</script>
<script type="text/javascript">
document.addEventListener("DOMContentLoaded", function() {
  var links = document.links;  
  for (var i = 0, linksLength = links.length; i < linksLength; i++)
    if (links[i].hostname != window.location.hostname)
      links[i].target = '_blank';
});
</script>

# Data Visualization with `systemPipeR`

*systemPipeTools* package extends the widely used *[systemPipeR](https://systempipe.org/)* (SPR) (H Backman and Girke 2016)
workflow environment with enhanced toolkit for data visualization,
including utilities to automate the analysis of differentially expressed genes (DEGs).
*systemPipeTools* provides functions for data transformation and data exploration via
scatterplots, hierarchical clustering heatMaps, principal component analysis,
multidimensional scaling, generalized principal components, t-Distributed
Stochastic Neighbor embedding (t-SNE), and MA and volcano plots.
All these utilities can be integrated with the modular design of the *systemPipeR*
environment that allows users to easily substitute any of these features and/or
custom with alternatives.

## Metadata and Reads Counting Information

The first step is importing the `targets` file and raw reads counting table.
- The `targets` file defines all FASTQ files and sample comparisons of the analysis workflow.
- The raw reads counting table represents all the reads that map to gene (row) for each sample (columns).

``` r
## Targets file
targetspath <- system.file("extdata", "targets.txt", package = "systemPipeR")
targets <- read.delim(targetspath, comment = "#")
cmp <- systemPipeR::readComp(file = targetspath, format = "matrix", delim = "-")
## Count table file
countMatrixPath <- system.file("extdata", "countDFeByg.xls", package = "systemPipeR")
countMatrix <- read.delim(countMatrixPath, row.names = 1)
showDT(countMatrix)
```

<div id="htmlwidget-1" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"filter":"none","extensions":["FixedColumns","Scroller"],"data":[["AT1G01010","AT1G01020","AT1G01030","AT1G01040","AT1G01050","AT1G01060","AT1G01070","AT1G01073","AT1G01080","AT1G01090","AT1G01100","AT1G01110","AT1G01115","AT2G01008","AT2G01021","AT2G01023","AT3G01010","AT3G01015","AT3G01020","AT3G01030","AT3G01040","AT3G01050","AT3G01060","AT3G01070","AT3G01080","AT3G01085","AT3G01090","AT3G01100","AT3G01120","AT3G01130","AT3G01140","AT3G01150","AT3G01160","AT3G01170","AT4G00005","AT4G00020","AT4G00026","AT4G00030","AT4G00040","AT4G00050","AT4G00060","AT4G00070","AT4G00080","AT4G00090","AT4G00100","AT4G00110","AT4G00120","AT4G00124","AT4G00130","AT4G00140","AT5G01010","AT5G01015","AT5G01020","AT5G01030","AT5G01040","AT5G01050","AT5G01060","AT5G01070","AT5G01075","AT5G01080","AT5G01090","AT5G01100","AT5G01110","AT5G01120","AT5G01130","AT5G01140","AT5G01150","AT5G01160","ATCG00020","ATCG00040","ATCG00050","ATCG00070","ATCG00080","ATCG00120","ATCG00130","ATCG00140","ATCG00150","ATCG00160","ATCG00170","ATCG00180","ATCG00190","ATCG00210","ATCG00220","ATCG00270","ATCG00280","ATCG00300","ATCG00330","ATCG00340","ATCG00350","ATCG00360","ATCG00380","ATCG00420","ATCG00430","ATCG00440","ATCG00470","ATCG00480","ATCG00490","ATCG00500","ATCG00510","ATMG00010","ATMG00030","ATMG00040","ATMG00050","ATMG00060","ATMG00070","ATMG00080","ATMG00090","ATMG00110","ATMG00120","ATMG00130","ATMG00140","ATMG00150","ATMG00160","ATMG00170","ATMG00180","ATMG00200"],[57,23,41,180,60,26,0,0,98,331,230,6,0,28,6267,0,0,0,0,0,93,31,235,0,30,0,70,38,709,54,0,37,33,33,0,4,19,69,61,12,48,0,0,21,186,22,0,0,6,8,143,16,87,31,49,4,0,0,1,0,17,162,2,0,0,0,0,28,1917,9,0,5,15,52,34,36,17,7,7,5,37,6,3,105,283,4,52,147,192,1,2,7,21,12,54,180,856,8,10,2,60,11,0,0,8,7,5,6,3,1,0,0,5,3,18,0],[244,93,98,684,127,264,0,0,379,1027,432,10,0,68,3061,14,0,0,0,0,454,121,801,8,29,0,274,132,2358,140,14,126,238,131,0,25,89,106,176,138,359,0,0,59,384,78,0,0,9,6,442,26,227,170,125,7,0,4,28,0,103,1002,26,2,0,0,0,124,1696,28,3,23,50,210,127,46,53,8,39,49,145,5,83,300,723,34,103,412,480,6,21,97,312,44,339,1191,1029,13,1,0,40,56,0,3,18,18,72,27,0,4,7,1,31,15,59,3],[201,69,73,522,102,59,2,0,179,779,516,11,0,61,7559,6,0,0,0,0,364,108,553,6,151,0,315,87,2031,149,4,186,123,161,0,6,60,255,189,20,162,0,0,89,402,75,0,0,32,30,542,11,184,91,179,5,0,0,9,0,41,754,6,0,0,0,0,119,970,10,1,14,13,113,37,60,22,3,14,22,49,1,5,165,293,5,56,222,191,6,8,18,45,12,92,369,793,4,5,0,79,38,0,4,5,20,30,7,0,0,0,0,25,5,44,1],[169,126,58,664,166,56,1,0,456,1343,458,5,0,33,2203,10,0,1,0,0,578,167,674,2,14,0,373,126,2222,131,39,170,329,212,0,66,75,121,147,117,381,0,0,88,432,147,0,0,4,11,646,17,207,219,103,3,0,0,23,0,121,1185,27,2,0,0,0,127,661,19,1,59,53,190,167,42,88,14,94,68,208,16,75,212,641,45,135,530,520,10,24,147,347,34,423,1501,871,10,1,7,35,50,0,3,47,31,120,34,14,1,5,0,72,17,62,4],[365,107,94,585,125,8,6,0,287,647,468,4,0,48,3125,0,0,0,0,0,375,104,226,5,56,0,334,100,1674,242,2,138,133,110,0,16,41,127,158,23,275,0,0,56,403,81,0,0,28,30,606,4,165,97,150,7,0,0,2,0,62,819,11,2,0,0,0,103,2258,12,0,23,34,160,74,44,26,12,22,32,95,10,25,126,403,10,50,313,366,4,10,26,36,24,102,403,977,2,15,2,43,45,0,2,19,16,25,13,0,1,2,3,26,14,24,1],[229,88,156,680,303,26,6,0,538,1831,849,17,0,53,1168,3,0,1,0,0,735,146,366,6,97,0,349,203,2310,254,0,380,126,296,0,49,43,193,282,19,406,0,0,138,966,131,0,0,16,21,1031,8,463,106,427,10,2,0,5,1,89,2267,41,4,0,0,0,238,1232,6,0,24,56,277,66,33,54,11,55,61,186,3,29,250,375,23,58,509,455,1,10,63,112,15,347,984,1161,10,2,3,35,39,0,7,21,19,41,15,1,3,2,1,46,13,58,3],[41,18,9,162,116,5,2,0,102,350,522,3,0,39,12653,0,0,0,0,0,46,43,8,0,15,0,92,28,780,84,14,45,51,51,0,5,56,73,102,63,70,0,0,42,360,42,0,0,3,7,230,15,153,22,2,0,0,0,11,0,23,24,6,0,0,0,0,60,1677,4,0,5,4,37,8,41,2,0,1,11,18,2,4,63,186,2,19,121,116,0,0,7,8,2,19,73,592,0,2,1,89,19,0,2,4,8,11,5,0,1,0,0,8,6,27,2],[38,25,13,163,180,2,4,0,211,524,634,3,0,38,12386,1,0,0,0,0,76,55,59,0,25,0,139,50,1217,116,14,95,80,54,0,11,66,124,114,45,119,3,0,66,440,40,0,0,2,13,334,58,221,27,2,0,0,0,11,0,36,99,8,0,0,0,0,76,1184,6,0,1,7,42,20,18,16,1,6,15,22,2,2,59,190,4,13,152,168,0,3,11,9,1,30,163,681,2,1,0,35,37,0,4,9,4,9,3,0,1,2,0,16,8,26,2],[152,20,8,249,139,0,5,0,79,323,926,5,0,97,9799,0,0,0,0,0,80,52,13,0,72,0,148,74,1176,160,21,67,92,73,0,11,93,157,185,151,122,0,0,78,656,48,0,0,3,20,461,2,260,57,11,0,0,0,8,0,39,188,4,0,0,0,0,83,1201,0,0,1,11,41,7,23,5,0,6,2,15,2,0,56,132,2,23,75,122,0,2,4,10,4,22,93,475,4,0,0,117,31,0,5,1,5,12,7,2,1,3,0,19,9,33,0],[46,5,6,66,37,0,2,0,42,140,183,2,0,23,10386,1,0,0,0,0,23,21,1,0,7,0,48,19,270,27,7,14,20,22,0,1,12,21,48,8,43,0,0,22,113,12,0,0,1,3,109,10,50,29,2,3,0,0,1,0,13,42,0,0,0,0,0,33,1261,4,0,2,3,42,15,26,4,0,4,5,4,6,1,65,138,9,17,106,126,2,4,6,4,0,12,54,749,6,1,0,30,4,0,0,0,2,3,1,0,0,0,0,2,0,7,0],[294,88,36,697,236,0,5,0,150,600,1333,1,0,82,9414,3,0,2,0,0,162,112,14,0,57,0,236,126,1737,341,15,126,178,132,0,23,146,209,317,158,210,0,0,191,1005,46,0,0,12,22,731,0,423,100,7,0,0,0,12,0,68,277,5,0,0,0,0,128,1192,1,0,2,9,52,9,28,8,3,1,7,22,2,3,83,172,4,25,112,112,1,0,11,14,6,29,110,446,2,4,3,101,56,0,5,10,9,20,14,0,1,1,0,36,9,44,2],[405,151,147,1060,679,4,13,0,551,1693,2401,16,0,112,3265,4,0,0,0,0,260,292,41,2,33,0,468,280,2768,376,50,299,278,112,0,36,175,337,471,169,463,2,0,334,1831,107,0,0,12,13,1229,53,903,127,12,3,0,0,32,0,168,146,33,0,0,0,0,266,398,6,0,4,11,75,26,18,18,3,17,11,67,2,3,71,176,7,28,163,186,2,7,18,23,4,52,345,493,0,4,0,43,88,0,8,25,18,39,14,4,11,4,0,54,20,53,2],[117,43,32,338,362,89,9,0,250,800,762,7,0,142,6908,6,0,0,0,0,143,53,103,0,27,0,257,128,1998,110,52,130,65,95,0,19,38,245,362,472,298,0,0,74,703,51,0,0,5,23,449,6,732,62,2,0,0,0,12,0,46,42,2,2,0,0,0,157,1406,8,0,11,6,51,13,9,5,0,5,13,28,2,2,100,126,2,2,128,194,1,3,12,30,2,63,270,445,2,0,0,64,6,0,1,9,18,6,7,0,0,5,1,21,7,25,1],[139,74,29,604,746,203,43,0,612,1662,1805,38,0,230,3676,2,0,0,0,0,131,211,178,4,34,0,390,194,1861,323,81,191,125,93,0,28,132,397,598,499,414,1,0,166,1319,117,0,0,11,29,861,65,1008,100,2,0,0,2,29,0,128,80,35,0,0,0,0,274,473,0,0,3,16,91,32,23,13,0,5,19,51,2,7,65,167,1,26,121,132,1,0,8,23,1,65,346,377,0,0,0,75,49,0,2,20,16,23,25,1,5,7,0,29,10,26,0],[132,33,12,360,194,118,8,0,78,281,761,4,0,85,11154,2,0,0,0,0,79,87,39,2,88,0,176,121,781,184,19,74,59,80,0,11,52,164,203,239,176,0,0,91,600,37,0,0,6,13,599,2,265,70,0,0,0,0,5,0,41,85,0,0,0,0,0,91,1136,0,0,6,11,34,12,38,10,0,2,9,9,2,2,48,135,3,15,88,108,1,0,2,6,3,25,82,429,2,0,0,114,23,0,5,6,4,10,2,0,4,0,0,16,6,17,0],[64,18,9,80,50,24,0,0,26,122,102,0,0,18,3301,0,0,0,0,0,34,25,6,0,13,0,32,24,219,51,13,20,26,19,0,1,13,22,37,12,48,0,0,20,106,10,0,0,1,2,121,1,95,21,2,0,0,0,3,0,14,33,0,0,0,0,0,38,1860,8,0,3,4,40,26,13,0,0,1,4,1,5,0,61,259,1,28,147,176,2,3,21,11,0,17,84,662,2,2,1,23,15,0,2,9,3,1,3,1,1,0,0,5,0,8,0],[230,43,70,203,214,62,9,0,78,391,627,0,0,100,9421,5,0,0,0,0,105,43,52,0,56,0,127,79,734,97,18,70,28,61,0,4,33,92,112,178,140,0,0,93,565,17,0,0,1,5,331,4,283,29,0,0,0,0,9,0,33,155,4,0,0,0,0,118,1336,0,0,8,4,27,5,8,8,6,2,10,7,1,4,52,112,1,10,81,106,1,0,8,19,3,37,140,440,2,2,0,66,10,0,7,7,5,13,7,0,3,6,1,16,0,28,2],[120,31,85,171,181,32,1,0,55,273,476,4,0,46,8486,2,0,0,0,0,55,24,24,0,33,0,76,45,291,98,12,42,39,29,0,4,26,57,69,59,62,0,0,51,362,17,0,0,1,5,207,3,195,28,1,0,0,0,4,0,17,67,3,0,0,0,0,86,1236,3,0,1,5,39,14,31,12,0,2,2,18,5,1,48,172,0,14,118,118,0,7,0,8,1,19,116,529,4,0,0,46,18,0,3,3,4,5,6,0,0,2,2,12,2,10,0]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>M1A<\/th>\n      <th>M1B<\/th>\n      <th>A1A<\/th>\n      <th>A1B<\/th>\n      <th>V1A<\/th>\n      <th>V1B<\/th>\n      <th>M6A<\/th>\n      <th>M6B<\/th>\n      <th>A6A<\/th>\n      <th>A6B<\/th>\n      <th>V6A<\/th>\n      <th>V6B<\/th>\n      <th>M12A<\/th>\n      <th>M12B<\/th>\n      <th>A12A<\/th>\n      <th>A12B<\/th>\n      <th>V12A<\/th>\n      <th>V12B<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"scrollX":true,"fixedColumns":true,"deferRender":true,"scrollY":200,"scroller":true,"columnDefs":[{"className":"dt-right","targets":[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>

## Data Transformation

For gene differential expression, raw counts are required, however for data
visualization or clustering, it can be useful to work with transformed count data.
`exploreDDS` function is convenience wrapper to transform raw read counts using the
[`DESeq2`](@Love2014-sh) package transformations methods. The input file
has to contain all the genes, not just differentially expressed ones. Supported
methods include variance stabilizing transformation (`vst`) (Anders and Huber (2010)), and
regularized-logarithm transformation or `rlog` (Love, Huber, and Anders (2014)).

``` r
exploredds <- exploreDDS(countMatrix, targets, cmp = cmp[[1]], preFilter = NULL, 
    transformationMethod = "rlog")
exploredds
```

    ## class: DESeqTransform 
    ## dim: 116 18 
    ## metadata(1): version
    ## assays(1): ''
    ## rownames(116): AT1G01010 AT1G01020 ... ATMG00180 ATMG00200
    ## rowData names(51): baseMean baseVar ... dispFit rlogIntercept
    ## colnames(18): M1A M1B ... V12A V12B
    ## colData names(2): condition sizeFactor

Users are strongly encouraged to consult the [`DESeq2`](@Love2014-sh) vignette for
more detailed information on this topic and how to properly run `DESeq2` on data
sets with more complex experimental designs.

## Scatterplot

To decide which transformation to choose, we can visualize the transformation effect
comparing two samples or a grid of all samples, as follows:

``` r
exploreDDSplot(countMatrix, targets, cmp = cmp[[1]], preFilter = NULL, samples = c("M12A", 
    "M12A", "A12A", "A12A"), scattermatrix = TRUE)
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

<img src="/en/sp/spt/systemPipeTools_files/figure-html/exploreDDSplot-1.png" width="672" />

The scatterplots are created using the log2 transform normalized reads count,
variance stabilizing transformation (VST) (Anders and Huber (2010)), and
regularized-logarithm transformation or `rlog` (Love, Huber, and Anders (2014)).

## Hierarchical Clustering Dendrogram

The following computes the sample-wise correlation coefficients using the `stats::cor()`
function from the transformed expression values. After transformation to a
distance matrix, hierarchical clustering is performed with the `stats::hclust`
function and the result is plotted as a dendrogram, as follows:

``` r
hclustplot(exploredds, method = "spearman")
```

<img src="/en/sp/spt/systemPipeTools_files/figure-html/hclustplot-1.png" width="672" />

The function provides the utility to save the plot automatically.

## Hierarchical Clustering HeatMap

This function performs hierarchical clustering on the transformed expression
matrix generated within the `DESeq2` package. It uses, by default, a `Pearson`
correlation-based distance measure and complete linkage for cluster join.
If `samples` selected in the `clust` argument, it will be applied the `stats::dist()`
function to the transformed count matrix to get sample-to-sample distances. Also,
it is possible to generate the `pheatmap` or `plotly` plot format.

``` r
## Samples plot
heatMaplot(exploredds, clust = "samples", plotly = TRUE)
```

<div id="htmlwidget-2" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"visdat":{"34341250a552":["function () ","plotlyVisDat"]},"cur_data":"34341250a552","attrs":{"34341250a552":{"x":["M1A","M1B","A1A","A1B","V1A","V1B","M6A","M6B","A6A","A6B","V6A","V6B","M12A","M12B","A12A","A12B","V12A","V12B"],"y":["M1A","M1B","A1A","A1B","V1A","V1B","M6A","M6B","A6A","A6B","V6A","V6B","M12A","M12B","A12A","A12B","V12A","V12B"],"z":[[0,7.04650716301563,5.70678310405774,8.20976445672658,5.82667776225818,7.3279781790244,8.39986657356742,8.16733063204217,9.58637200173571,7.68841587215867,10.1640441508758,10.7676019921496,10.0039632569807,11.32498784981,9.8146750121175,7.74473230078491,9.45716343166999,7.95378561107353],[7.04650716301563,0,6.66154862259465,4.25865887783483,6.67960023884926,6.26668680998727,9.91630309634838,9.25451827523275,10.9564120825428,9.93575571094716,11.099388064366,10.6754670535994,9.90683653800534,10.9561298226477,10.7399675586854,9.18116169782986,9.77109863659917,9.40323019102986],[5.70678310405774,6.66154862259465,0,7.98994675562316,4.94593038167375,5.72836463615867,8.11235158724083,7.65256178153187,8.15065142907597,8.76007256265634,8.30988507282082,8.91309701678265,8.66629724080143,9.82426010379448,8.30870129249907,8.54268071001664,8.35323474316893,7.70897398227057],[8.20976445672658,4.25865887783483,7.98994675562316,0,6.99532785790822,6.43469620310431,10.4096764476556,9.51652950962973,11.1939050957909,10.4627147426448,11.1689702900908,10.546647320753,10.5708484745604,11.5547562063225,11.6160197603858,9.88406363111819,10.7020155017471,10.4675703563444],[5.82667776225818,6.67960023884926,4.94593038167375,6.99532785790822,0,4.8575131388009,8.46288752842871,8.0319315058583,8.726172089783,8.73161790330149,8.27286514155669,8.88152783442813,9.62675093908279,10.8109068917939,9.50867890759956,8.56129430593498,9.21166728284744,8.48571139105286],[7.3279781790244,6.26668680998727,5.72836463615867,6.43469620310431,4.8575131388009,0,10.051631844146,8.92833694901717,9.88801350128227,10.1968579735558,9.80606329541741,9.47694677716336,10.2032985748696,10.9502439173503,10.7118343889731,10.2485736407499,9.95124988126944,9.6455696901528],[8.39986657356742,9.91630309634838,8.11235158724083,10.4096764476556,8.46288752842871,10.051631844146,0,4.32289188181976,5.45401419571659,6.66929785847857,5.82333805363524,6.89960979808065,6.60846441830892,7.49378480640748,6.09490379797155,6.92856692552639,6.73658240504653,6.04084631483171],[8.16733063204217,9.25451827523275,7.65256178153187,9.51652950962973,8.0319315058583,8.92833694901717,4.32289188181976,0,5.86548263173596,6.92170483627566,6.43771467140554,5.936553276735,6.66918890392232,7.10201521498403,6.87338305585792,7.70858313971616,6.93977726065822,6.12205683109543],[9.58637200173571,10.9564120825428,8.15065142907597,11.1939050957909,8.726172089783,9.88801350128227,5.45401419571659,5.86548263173596,0,8.10337075683393,4.02970654063498,6.37598537189006,6.96355226928132,7.79890861008178,5.50539366529938,8.64913887544163,6.82883422186719,6.22801929982399],[7.68841587215867,9.93575571094716,8.76007256265634,10.4627147426448,8.73161790330149,10.1968579735558,6.66929785847857,6.92170483627566,8.10337075683393,0,9.22853479532283,10.1030591897721,9.35527845594351,11.0912154866989,8.92785474831708,6.32121021712703,9.14034499886722,7.20502415178336],[10.1640441508758,11.099388064366,8.30988507282082,11.1689702900908,8.27286514155669,9.80606329541741,5.82333805363524,6.43771467140554,4.02970654063498,9.22853479532283,0,5.40796455622463,7.23562402229216,8.05893271349359,5.83000947413891,8.94623155465764,6.52802367477244,6.94139936721835],[10.7676019921496,10.6754670535994,8.91309701678265,10.546647320753,8.88152783442813,9.47694677716336,6.89960979808065,5.936553276735,6.37598537189006,10.1030591897721,5.40796455622463,0,7.14309602773391,6.1610771391521,7.4911181113735,10.0381028337193,7.56298264238769,7.68916986877059],[10.0039632569807,9.90683653800534,8.66629724080143,10.5708484745604,9.62675093908279,10.2032985748696,6.60846441830892,6.66918890392232,6.96355226928132,9.35527845594351,7.23562402229216,7.14309602773391,0,5.69259437645614,5.58694500597765,8.50447659713418,5.53119139458227,6.33933832045536],[11.32498784981,10.9561298226477,9.82426010379448,11.5547562063225,10.8109068917939,10.9502439173503,7.49378480640748,7.10201521498403,7.79890861008178,11.0912154866989,8.05893271349359,6.1610771391521,5.69259437645614,0,6.42494730487994,10.5078546330517,7.19994521380774,7.82561653509729],[9.8146750121175,10.7399675586854,8.30870129249907,11.6160197603858,9.50867890759956,10.7118343889731,6.09490379797155,6.87338305585792,5.50539366529938,8.92785474831708,5.83000947413891,7.4911181113735,5.58694500597765,6.42494730487994,0,8.18110233128943,5.25899641633563,5.72577800197228],[7.74473230078491,9.18116169782986,8.54268071001664,9.88406363111819,8.56129430593498,10.2485736407499,6.92856692552639,7.70858313971616,8.64913887544163,6.32121021712703,8.94623155465764,10.0381028337193,8.50447659713418,10.5078546330517,8.18110233128943,0,7.99272460895717,6.58008064549415],[9.45716343166999,9.77109863659917,8.35323474316893,10.7020155017471,9.21166728284744,9.95124988126944,6.73658240504653,6.93977726065822,6.82883422186719,9.14034499886722,6.52802367477244,7.56298264238769,5.53119139458227,7.19994521380774,5.25899641633563,7.99272460895717,0,5.56397338345294],[7.95378561107353,9.40323019102986,7.70897398227057,10.4675703563444,8.48571139105286,9.6455696901528,6.04084631483171,6.12205683109543,6.22801929982399,7.20502415178336,6.94139936721835,7.68916986877059,6.33933832045536,7.82561653509729,5.72577800197228,6.58008064549415,5.56397338345294,0]],"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"heatmap"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"xaxis":{"domain":[0,1],"automargin":true,"title":[]},"yaxis":{"domain":[0,1],"automargin":true,"title":[]},"scene":{"zaxis":{"title":[]}},"hovermode":"closest","showlegend":false,"legend":{"yanchor":"top","y":0.5}},"source":"A","config":{"showSendToCloud":false},"data":[{"colorbar":{"title":"","ticklen":2,"len":0.5,"lenmode":"fraction","y":1,"yanchor":"top"},"colorscale":[["0","rgba(68,1,84,1)"],["0.0416666666666667","rgba(70,19,97,1)"],["0.0833333333333333","rgba(72,32,111,1)"],["0.125","rgba(71,45,122,1)"],["0.166666666666667","rgba(68,58,128,1)"],["0.208333333333333","rgba(64,70,135,1)"],["0.25","rgba(60,82,138,1)"],["0.291666666666667","rgba(56,93,140,1)"],["0.333333333333333","rgba(49,104,142,1)"],["0.375","rgba(46,114,142,1)"],["0.416666666666667","rgba(42,123,142,1)"],["0.458333333333333","rgba(38,133,141,1)"],["0.5","rgba(37,144,140,1)"],["0.541666666666667","rgba(33,154,138,1)"],["0.583333333333333","rgba(39,164,133,1)"],["0.625","rgba(47,174,127,1)"],["0.666666666666667","rgba(53,183,121,1)"],["0.708333333333333","rgba(79,191,110,1)"],["0.75","rgba(98,199,98,1)"],["0.791666666666667","rgba(119,207,85,1)"],["0.833333333333333","rgba(147,214,70,1)"],["0.875","rgba(172,220,52,1)"],["0.916666666666667","rgba(199,225,42,1)"],["0.958333333333333","rgba(226,228,40,1)"],["1","rgba(253,231,37,1)"]],"showscale":true,"x":["M1A","M1B","A1A","A1B","V1A","V1B","M6A","M6B","A6A","A6B","V6A","V6B","M12A","M12B","A12A","A12B","V12A","V12B"],"y":["M1A","M1B","A1A","A1B","V1A","V1B","M6A","M6B","A6A","A6B","V6A","V6B","M12A","M12B","A12A","A12B","V12A","V12B"],"z":[[0,7.04650716301563,5.70678310405774,8.20976445672658,5.82667776225818,7.3279781790244,8.39986657356742,8.16733063204217,9.58637200173571,7.68841587215867,10.1640441508758,10.7676019921496,10.0039632569807,11.32498784981,9.8146750121175,7.74473230078491,9.45716343166999,7.95378561107353],[7.04650716301563,0,6.66154862259465,4.25865887783483,6.67960023884926,6.26668680998727,9.91630309634838,9.25451827523275,10.9564120825428,9.93575571094716,11.099388064366,10.6754670535994,9.90683653800534,10.9561298226477,10.7399675586854,9.18116169782986,9.77109863659917,9.40323019102986],[5.70678310405774,6.66154862259465,0,7.98994675562316,4.94593038167375,5.72836463615867,8.11235158724083,7.65256178153187,8.15065142907597,8.76007256265634,8.30988507282082,8.91309701678265,8.66629724080143,9.82426010379448,8.30870129249907,8.54268071001664,8.35323474316893,7.70897398227057],[8.20976445672658,4.25865887783483,7.98994675562316,0,6.99532785790822,6.43469620310431,10.4096764476556,9.51652950962973,11.1939050957909,10.4627147426448,11.1689702900908,10.546647320753,10.5708484745604,11.5547562063225,11.6160197603858,9.88406363111819,10.7020155017471,10.4675703563444],[5.82667776225818,6.67960023884926,4.94593038167375,6.99532785790822,0,4.8575131388009,8.46288752842871,8.0319315058583,8.726172089783,8.73161790330149,8.27286514155669,8.88152783442813,9.62675093908279,10.8109068917939,9.50867890759956,8.56129430593498,9.21166728284744,8.48571139105286],[7.3279781790244,6.26668680998727,5.72836463615867,6.43469620310431,4.8575131388009,0,10.051631844146,8.92833694901717,9.88801350128227,10.1968579735558,9.80606329541741,9.47694677716336,10.2032985748696,10.9502439173503,10.7118343889731,10.2485736407499,9.95124988126944,9.6455696901528],[8.39986657356742,9.91630309634838,8.11235158724083,10.4096764476556,8.46288752842871,10.051631844146,0,4.32289188181976,5.45401419571659,6.66929785847857,5.82333805363524,6.89960979808065,6.60846441830892,7.49378480640748,6.09490379797155,6.92856692552639,6.73658240504653,6.04084631483171],[8.16733063204217,9.25451827523275,7.65256178153187,9.51652950962973,8.0319315058583,8.92833694901717,4.32289188181976,0,5.86548263173596,6.92170483627566,6.43771467140554,5.936553276735,6.66918890392232,7.10201521498403,6.87338305585792,7.70858313971616,6.93977726065822,6.12205683109543],[9.58637200173571,10.9564120825428,8.15065142907597,11.1939050957909,8.726172089783,9.88801350128227,5.45401419571659,5.86548263173596,0,8.10337075683393,4.02970654063498,6.37598537189006,6.96355226928132,7.79890861008178,5.50539366529938,8.64913887544163,6.82883422186719,6.22801929982399],[7.68841587215867,9.93575571094716,8.76007256265634,10.4627147426448,8.73161790330149,10.1968579735558,6.66929785847857,6.92170483627566,8.10337075683393,0,9.22853479532283,10.1030591897721,9.35527845594351,11.0912154866989,8.92785474831708,6.32121021712703,9.14034499886722,7.20502415178336],[10.1640441508758,11.099388064366,8.30988507282082,11.1689702900908,8.27286514155669,9.80606329541741,5.82333805363524,6.43771467140554,4.02970654063498,9.22853479532283,0,5.40796455622463,7.23562402229216,8.05893271349359,5.83000947413891,8.94623155465764,6.52802367477244,6.94139936721835],[10.7676019921496,10.6754670535994,8.91309701678265,10.546647320753,8.88152783442813,9.47694677716336,6.89960979808065,5.936553276735,6.37598537189006,10.1030591897721,5.40796455622463,0,7.14309602773391,6.1610771391521,7.4911181113735,10.0381028337193,7.56298264238769,7.68916986877059],[10.0039632569807,9.90683653800534,8.66629724080143,10.5708484745604,9.62675093908279,10.2032985748696,6.60846441830892,6.66918890392232,6.96355226928132,9.35527845594351,7.23562402229216,7.14309602773391,0,5.69259437645614,5.58694500597765,8.50447659713418,5.53119139458227,6.33933832045536],[11.32498784981,10.9561298226477,9.82426010379448,11.5547562063225,10.8109068917939,10.9502439173503,7.49378480640748,7.10201521498403,7.79890861008178,11.0912154866989,8.05893271349359,6.1610771391521,5.69259437645614,0,6.42494730487994,10.5078546330517,7.19994521380774,7.82561653509729],[9.8146750121175,10.7399675586854,8.30870129249907,11.6160197603858,9.50867890759956,10.7118343889731,6.09490379797155,6.87338305585792,5.50539366529938,8.92785474831708,5.83000947413891,7.4911181113735,5.58694500597765,6.42494730487994,0,8.18110233128943,5.25899641633563,5.72577800197228],[7.74473230078491,9.18116169782986,8.54268071001664,9.88406363111819,8.56129430593498,10.2485736407499,6.92856692552639,7.70858313971616,8.64913887544163,6.32121021712703,8.94623155465764,10.0381028337193,8.50447659713418,10.5078546330517,8.18110233128943,0,7.99272460895717,6.58008064549415],[9.45716343166999,9.77109863659917,8.35323474316893,10.7020155017471,9.21166728284744,9.95124988126944,6.73658240504653,6.93977726065822,6.82883422186719,9.14034499886722,6.52802367477244,7.56298264238769,5.53119139458227,7.19994521380774,5.25899641633563,7.99272460895717,0,5.56397338345294],[7.95378561107353,9.40323019102986,7.70897398227057,10.4675703563444,8.48571139105286,9.6455696901528,6.04084631483171,6.12205683109543,6.22801929982399,7.20502415178336,6.94139936721835,7.68916986877059,6.33933832045536,7.82561653509729,5.72577800197228,6.58008064549415,5.56397338345294,0]],"type":"heatmap","xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

If `ind` selected in the `clust` argument, it is necessary to provide the list of
differentially expressed genes for the `exploredds` subset.

``` r
## Individuals genes identified in DEG analysis DEG analysis with `systemPipeR`
degseqDF <- systemPipeR::run_DESeq2(countDF = countMatrix, targets = targets, cmp = cmp[[1]], 
    independent = FALSE)
DEG_list <- systemPipeR::filterDEGs(degDF = degseqDF, filter = c(Fold = 2, FDR = 10))
```

<img src="/en/sp/spt/systemPipeTools_files/figure-html/heatMaplot_DEG-1.png" width="672" />

``` r
### Plot
heatMaplot(exploredds, clust = "ind", DEGlist = unique(as.character(unlist(DEG_list[[1]]))))
```

<img src="/en/sp/spt/systemPipeTools_files/figure-html/heatMaplot_DEG-2.png" width="672" />

The function provides the utility to save the plot automatically.

## Principal Component Analysis

This function plots a Principal Component Analysis (PCA) from transformed expression
matrix. This plot shows samples variation based on the expression values and
identifies batch effects.

``` r
PCAplot(exploredds, plotly = FALSE)
```

<img src="/en/sp/spt/systemPipeTools_files/figure-html/PCAplot-1.png" width="672" />

The function provides the utility to save the plot automatically.

## Multidimensional scaling with `MDSplot`

This function computes and plots multidimensional scaling analysis for dimension
reduction of count expression matrix. Internally, it is applied the `stats::dist()`
function to the transformed count matrix to get sample-to-sample distances.

``` r
MDSplot(exploredds, plotly = FALSE)
```

<img src="/en/sp/spt/systemPipeTools_files/figure-html/MDSplot-1.png" width="672" />

The function provides the utility to save the plot automatically.

## Dimension Reduction with `GLMplot`

This function computes and plots generalized principal components analysis for
dimension reduction of count expression matrix.

``` r
exploredds_r <- exploreDDS(countMatrix, targets, cmp = cmp[[1]], preFilter = NULL, 
    transformationMethod = "raw")
GLMplot(exploredds_r, plotly = FALSE)
```

<img src="/en/sp/spt/systemPipeTools_files/figure-html/GLMplot-1.png" width="672" />

The function provides the utility to save the plot automatically.

## MA plot

This function plots log2 fold changes (y-axis) versus the mean of normalized
counts (on the x-axis). Statistically significant features are colored.

``` r
MAplot(degseqDF, comparison = "M12-A12", filter = c(Fold = 1, FDR = 20), genes = "ATCG00280")
```

<img src="/en/sp/spt/systemPipeTools_files/figure-html/MAplot-1.png" width="672" />

The function provides the utility to save the plot automatically.

## t-Distributed Stochastic Neighbor embedding with `tSNEplot`

This function computes and plots t-Distributed Stochastic Neighbor embedding (t-SNE)
analysis for unsupervised nonlinear dimensionality reduction of count expression
matrix. Internally, it is applied the `Rtsne::Rtsne()` (Krijthe 2015) function, using the exact
t-SNE computing with `theta=0.0`.

``` r
tSNEplot(countMatrix, targets, perplexity = 5)
```

<img src="/en/sp/spt/systemPipeTools_files/figure-html/tSNEplot-1.png" width="672" />

## Volcano plot

A simple function that shows statistical significance (`p-value`) versus magnitude
of change (`log2 fold change`).

``` r
volcanoplot(degseqDF, comparison = "M12-A12", filter = c(Fold = 1, FDR = 20), genes = "ATCG00280")
```

<img src="/en/sp/spt/systemPipeTools_files/figure-html/volcanoplot-1.png" width="672" />

# Version information

``` r
sessionInfo()
```

    ## R Under development (unstable) (2021-02-04 r79940)
    ## Platform: x86_64-pc-linux-gnu (64-bit)
    ## Running under: Ubuntu 20.04.2 LTS
    ## 
    ## Matrix products: default
    ## BLAS:   /usr/lib/x86_64-linux-gnu/blas/libblas.so.3.9.0
    ## LAPACK: /home/dcassol/src/R-devel/lib/libRlapack.so
    ## 
    ## locale:
    ##  [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
    ##  [3] LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8    
    ##  [5] LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
    ##  [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                 
    ##  [9] LC_ADDRESS=C               LC_TELEPHONE=C            
    ## [11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       
    ## 
    ## attached base packages:
    ## [1] stats4    parallel  stats     graphics  grDevices utils     datasets 
    ## [8] methods   base     
    ## 
    ## other attached packages:
    ##  [1] systemPipeR_1.25.11         ShortRead_1.49.2           
    ##  [3] GenomicAlignments_1.27.2    SummarizedExperiment_1.21.3
    ##  [5] Biobase_2.51.0              MatrixGenerics_1.3.1       
    ##  [7] matrixStats_0.58.0          BiocParallel_1.25.5        
    ##  [9] Rsamtools_2.7.2             Biostrings_2.59.2          
    ## [11] XVector_0.31.1              GenomicRanges_1.43.4       
    ## [13] GenomeInfoDb_1.27.11        IRanges_2.25.9             
    ## [15] S4Vectors_0.29.15           BiocGenerics_0.37.2        
    ## [17] systemPipeTools_0.9.1       BiocStyle_2.19.2           
    ## 
    ## loaded via a namespace (and not attached):
    ##   [1] backports_1.2.1          BiocFileCache_1.99.6     plyr_1.8.6              
    ##   [4] lazyeval_0.2.2           splines_4.1.0            crosstalk_1.1.1         
    ##   [7] ggplot2_3.3.3            digest_0.6.27            htmltools_0.5.1.1       
    ##  [10] fansi_0.4.2              magrittr_2.0.1           checkmate_2.0.0         
    ##  [13] memoise_2.0.0            BSgenome_1.59.2          base64url_1.4           
    ##  [16] limma_3.47.12            annotate_1.69.2          prettyunits_1.1.1       
    ##  [19] jpeg_0.1-8.1             colorspace_2.0-0         blob_1.2.1              
    ##  [22] rappdirs_0.3.3           ggrepel_0.9.1            xfun_0.22               
    ##  [25] dplyr_1.0.5              crayon_1.4.1             RCurl_1.98-1.3          
    ##  [28] jsonlite_1.7.2           genefilter_1.73.1        VariantAnnotation_1.37.1
    ##  [31] brew_1.0-6               survival_3.2-10          ape_5.4-1               
    ##  [34] glue_1.4.2               gtable_0.3.0             zlibbioc_1.37.0         
    ##  [37] DelayedArray_0.17.10     V8_3.4.0                 scales_1.1.1            
    ##  [40] pheatmap_1.0.12          DBI_1.1.1                GGally_2.1.1            
    ##  [43] edgeR_3.33.3             Rcpp_1.0.6               viridisLite_0.4.0       
    ##  [46] xtable_1.8-4             progress_1.2.2           tidytree_0.3.3          
    ##  [49] bit_4.0.4                rsvg_2.1.1               DT_0.18                 
    ##  [52] htmlwidgets_1.5.3        httr_1.4.2               RColorBrewer_1.1-2      
    ##  [55] ellipsis_0.3.1           farver_2.1.0             pkgconfig_2.0.3         
    ##  [58] reshape_0.8.8            XML_3.99-0.6             dbplyr_2.1.1            
    ##  [61] sass_0.3.1               locfit_1.5-9.4           utf8_1.2.1              
    ##  [64] labeling_0.4.2           later_1.1.0.1            tidyselect_1.1.0        
    ##  [67] rlang_0.4.10             AnnotationDbi_1.53.1     munsell_0.5.0           
    ##  [70] tools_4.1.0              cachem_1.0.4             generics_0.1.0          
    ##  [73] RSQLite_2.2.7            evaluate_0.14            stringr_1.4.0           
    ##  [76] fastmap_1.1.0            yaml_2.2.1               ggtree_2.5.2            
    ##  [79] knitr_1.32               bit64_4.0.5              purrr_0.3.4             
    ##  [82] KEGGREST_1.31.1          nlme_3.1-152             mime_0.10               
    ##  [85] formatR_1.9              aplot_0.0.6              biomaRt_2.47.7          
    ##  [88] compiler_4.1.0           filelock_1.0.2           plotly_4.9.3            
    ##  [91] curl_4.3                 png_0.1-7                treeio_1.15.7           
    ##  [94] tibble_3.1.1             geneplotter_1.69.0       bslib_0.2.4             
    ##  [97] stringi_1.5.3            highr_0.9                blogdown_1.3            
    ## [100] GenomicFeatures_1.43.8   lattice_0.20-41          Matrix_1.3-2            
    ## [103] glmpca_0.2.0             vctrs_0.3.7              pillar_1.6.0            
    ## [106] lifecycle_1.0.0          BiocManager_1.30.12      jquerylib_0.1.3         
    ## [109] data.table_1.14.0        bitops_1.0-6             httpuv_1.5.5            
    ## [112] rtracklayer_1.51.5       patchwork_1.1.1          BiocIO_1.1.2            
    ## [115] R6_2.5.0                 latticeExtra_0.6-29      hwriter_1.3.2           
    ## [118] promises_1.2.0.1         bookdown_0.22            codetools_0.2-18        
    ## [121] MASS_7.3-53.1            assertthat_0.2.1         rjson_0.2.20            
    ## [124] DESeq2_1.31.18           withr_2.4.2              batchtools_0.9.15       
    ## [127] GenomeInfoDbData_1.2.4   hms_1.0.0                grid_4.1.0              
    ## [130] tidyr_1.1.3              DOT_0.1                  rmarkdown_2.7.12        
    ## [133] rvcheck_0.1.8            Rtsne_0.15               shiny_1.6.0             
    ## [136] restfulr_0.0.13

# Funding

This project is funded by NSF award [ABI-1661152](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1661152).

# References

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-Anders2010-tp" class="csl-entry">

Anders, Simon, and Wolfgang Huber. 2010. “Differential Expression Analysis for Sequence Count Data.” *Genome Biol.* 11 (10): R106.

</div>

<div id="ref-H_Backman2016-bt" class="csl-entry">

H Backman, Tyler W, and Thomas Girke. 2016. “<span class="nocase">systemPipeR: NGS workflow and report generation environment</span>.” *BMC Bioinformatics* 17 (1): 388. <https://doi.org/10.1186/s12859-016-1241-0>.

</div>

<div id="ref-Rtsne" class="csl-entry">

Krijthe, Jesse H. 2015. *Rtsne: T-Distributed Stochastic Neighbor Embedding Using Barnes-Hut Implementation*. <https://github.com/jkrijthe/Rtsne>.

</div>

<div id="ref-Love2014-sh" class="csl-entry">

Love, Michael, Wolfgang Huber, and Simon Anders. 2014. “Moderated Estimation of Fold Change and Dispersion for <span class="nocase">RNA-seq</span> Data with DESeq2.” *Genome Biol.* 15 (12): 550. <https://doi.org/10.1186/s13059-014-0550-8>.

</div>

</div>
