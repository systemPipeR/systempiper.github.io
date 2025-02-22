---
title: "Generate Reports" 
date: "Last update: 06 June, 2022" 
type: docs
weight: 7
---

After the analysis, we often would like to generate some reports. In SPR, we 
provide two types of reports: technical report and analysis report. Both of 
them would give you an interactive HTML file. 

## Technical report

_`systemPipeR`_ compiles all the workflow execution logs in one central location, 
making it easier to check any standard output (`stdout`) or standard error 
(`stderr`) for any command-line tools used on the workflow or the R code `stdout`.
Also, the workflow plot is appended at the beginning of the report, making it 
easier to click on the respective step.


```r
sal <- renderLogs(sal)
```

An example log file can be viewed over [here](../logs_example.html). 

## Analysis report
To communicate with researchers outside one's field, text explanation is usually 
expected. When we design a workflow and [import from a template](../step_import), 
adding text description to help people understand the workflow is highly recommended. 
The template can also be used to display results. Remember only **SPR chunks** `(spr=TRUE)`  
would be imported into the workflow. Therefore, other chunks are 
**ignored until rendering the analysis report** with `renderReport`. These 
non-SPR chunks will be **evaluated** (if they do not have `eval=FALSE`) in report 
rendering and all SPR chunks will all be **muted**. So these non-SPR chunks can be 
good places to add some images, tables, plots, or other light calculations.



```r
sal <- renderReport(sal)
```

- Here the `renderReport` uses the copy of workflow template, which is stored in `.SPRProject`, 
  as skeleton to generate the report. All text is copied over and all steps in current 
  workflow are **translated** into reproducible code to the skeleton. 
- If any step is added interactively, meaning they did not exist in the template when
  you used `importWF`, `renderReport` has an internal algorithm to find the right 
  place to inject the translated code based on the order where they appear inside 
  `SYSargsList`. However, there will be no text description of these new steps.
- The algorithm is smart but not 100%, so if any new step is been added interactively, 
  we recommend you to add text description and code accordingly in the template 
  and use `importWF(..., update = TRUE)` as discussed in [import section](../step_import) to update. 
- If all steps are added interactively, meaning you did not use `importWF` at all,
  `sal2rmd` will be called. We will discuss this function in the next section.

To have a glimpse of what the `renderReport` file look like, check out our 
pre-configed workflow templates rendered pages [here](/spr_wf/#workflow-templates).


