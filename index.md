---
title: "iSEE workshop | Bioconductor conference 2019"
categories: R
date: '2019-02-05T00:00:00Z'
slides:
  highlight_style: github
  theme: white
summary: An introduction to the iSEE package and functionality.
tags:
- iSEE
- Bioconductor
authors:
- Kevin Rue-Albrecht
- Charlotte Soneson
---

<!-- Prevent capitalization of titles -->
<style>
    .reveal h1, .reveal h2, .reveal h3, .reveal h4, .reveal h5 {
                  text-transform: none;
		  }
    .reveal fs80 {
                  font-size: 80%;
		  }
    .reveal fs60 {
                  font-size: 60%;
		  }
</style>

# [iSEE](http://bioconductor.org/packages/iSEE/) package and functionality

Bioconductor conference 2019

[Kevin Rue-Albrecht](https://kevinrue.github.io) & [Charlotte Soneson](https://csoneson.github.io)

Twitter: [@KevinRUE67](https://twitter.com/KevinRUE67) & [@csoneson](https://twitter.com/csoneson)

<!--
Welcome to the iSEE workshop.
In this presentation, we will introduce the concepts and functionality of the iSEE package.
-->

---

# The team

<table>
<tr>
<td width="25%"><a href="https://kevinrue.github.io"><img src="/img/iSEE/kevin-rue.png"></a></td>
<td width="25%"><a href="https://csoneson.github.io"><img src="/img/iSEE/charlotte-soneson.png"></a></td>
<td width="25%"><a href="https://federicomarini.github.io"><img src="/img/iSEE/federico-marini.png"></a></td>
<td width="25%"><a href="https://orcid.org/0000-0002-3564-4813"><img src="/img/iSEE/aaron-lun.png"></a></td>
</tr>
</table>

<!--
This was a team effort!
-->

---

<a href="https://bioconductor.org"><img src="/img/iSEE/biocstickers.jpg" height=600></a>

<!--
iSEE tightly integrates with other packages of the Bioconductor project.
-->

---

# <fs60>Original wishlist (1 / 2)</fs60>

- <fs80>An interactive user interface for exploring data in *[SummarizedExperiment](https://bioconductor.org/packages/release/SummarizedExperiment)* objects</fs80>
- <fs80>Particular focus given to single-cell data in the *[SingleCellExperiment](https://bioconductor.org/packages/release/SingleCellExperiment)* derived class</fs80>
- <fs80>Sample-oriented visualizations</fs80>
- <fs80>Feature-oriented visualizations</fs80>
- <fs80>Heat maps (cells _and_ features)</fs80>
- <fs80>Selectable points</fs80>

<!--
When we sat down at EuroBioc2017, we drafted a wishlist of features.
See commit #3 at https://github.com/csoneson/iSEE/tree/021e3e20cfdb194e511f8097ed544329bd46bcd6
-->

---

# <fs60>Original wishlist (2 / 2)</fs60>

- <fs80>Colouring of samples by metadata or assayed values</fs80>
- <fs80>Stratify axes and facets by metadata (e.g., violin plots)</fs80>
- <fs80>Hover and click</fs80>
- <fs80>Zoom</fs80>
- <fs80>Transmission of points selections between plots</fs80>
- <fs80>Code tracking for reproducibility and batch generation of figures</fs80>

<!--
When we sat down at EuroBioc2017, we drafted a wishlist of features.
See commit #3 at https://github.com/csoneson/iSEE/tree/021e3e20cfdb194e511f8097ed544329bd46bcd6
-->

---

<img src="/img/OSCA/bioc-figures_v2-02.png" height=500>

<!--
iSEE focuses on the SingleCellExperiment class.
This class stores all the data and metadata associated with assays, cells, and features.
-->

---

<img src="/img/OSCA/bioc-figures_v2-03.png" height=600>

<!-- 
The SingleCellExperiment class is designed to accomodate all the information produced along a typical single-cell analysis workflow.
Those data include raw data:
- raw assay data
- experimental metadata
Processed data:
- quality control metrics
- normalized data
- dimensionality reduction results
Downstream analyses:
- cluster labels
- differential expression results
- downstream cell and feature annotations
-->

---

<img src="/img/iSEE/batman-robin.png" height=500>

<!--
Don't try this at home.
The wealth of information produced by single-cell analysis workflows has motivated the development of many interactive applications to help researchers explore their data sets.
Each of those applications has its own strengths and limitations.
It is very tempting to develop new applications to with their own strengths and limitations.
Before you decide to do so, we encourage you to test iSEE.
You may find that it already does everything you would like!
-->

---

<img src="/img/OSCA/OSCA-figure-4.png" height=600>

<!--
Here we demonstrate how iSEE dissects SCE objects to produce figures.
-->

---

<img src="https://raw.githubusercontent.com/kevinrue/iSEEWorkshop2019/master/inst/vignettes/img/iSEEinterface.png" height=600>

<!--
iSEE provides a powerful yet flexible user interface that includes 8 predefined panel types.
That said, it also gives the freedom to define any number custom panel types, both plots and tables.
-->

---

<a href="https://kevinrue.shinyapps.io/magick-profile/"><img src="/img/workshop.png"></a>

<!--
With that introduction to the user interface, let us head into the workshop!
-->

---

`iSEE(sce, voice=TRUE)`

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe src="//www.youtube.com/embed/0crFZLwAJOE?autoplay=0" style="position: absolute; top: 0; left: 0; width: 100%; height: 90%; border:0;" allowfullscreen title="YouTube Video"></iframe>
</div>

<!--
iSEE can be extended using third-party JavaScript libraries.
Here we demonstrate how speech recognition was integrated to support a number of predefined vocal commands.
-->

---

<a href="https://blog.rstudio.com/2019/04/05/first-shiny-contest-winners/"><img src="/img/iSEE/shiny-contest.png" height=600></a>

<!--
iSEE won the RStudio Shiny Contest in April 2019 with mention for "Most technically impressive".
See https://blog.rstudio.com/2019/04/05/first-shiny-contest-winners/ for more details.
In particular:
- There were 136 submissions from 122 unique app developers!
-->

---

Creating an `ExperimentColorMap`

```
qc_color_fun <- function(n){
    qc_colors <- c("forestgreen", "firebrick1")
    names(qc_colors) <- c("Y", "N")
    qc_colors
}
```

```
ExperimentColorMap(
    assays = list(
        counts = heat.colors,
        logcounts = logcounts_color_fun,
        cufflinks_fpkm = fpkm_color_fun
    ),
    colData = list(
        passes_qc_checks_s = qc_color_fun
    ),
    all_continuous = list(
        assays = viridis::plasma
    ),
    global_continuous = viridis::viridis
)
```

---

Using an `ExperimentColorMap` object

```
colDataColorMap(ecm, "passes_qc_checks_s", discrete=TRUE)
```

---

How [iSEE](http://bioconductor.org/packages/iSEE/) uses the `ExperimentColorMap` object

<img src="/img/iSEE/Use-ExperimentColorMap.png">

---

# <fs60>The iSEE-verse</fs60>

* <fs60>http://bioconductor.org/packages/iSEE/</fs60>
* <fs60>https://github.com/LTLA/iSEE2018</fs60>
* <fs60>https://github.com/csoneson/iSEE</fs60>
* <fs60>https://github.com/kevinrue/iSEE_custom</fs60>
* <fs60>https://github.com/federicomarini/iSEE_instances</fs60>
* <fs60>https://github.com/kevinrue/iSEEWorkshop2019</fs60>

<!--
The growing funtionality of the iSEE package is demonstrated in various places:
- The Bioconductor website is the primary source of information for the latest release and development package versions.
- The package GitHub repository is the place to monitor the latest developments, open issues, and contribute pull requests (consider the Bioconductor support website for general questions)
- kevinrue/iSEE_custom demonstrates the development of custom panels through a gallery of examples
- federicomarini/iSEE_instances demonstrates the integration of iSEE with entire analyses of publicly available datasets through a gallery of examples
- Finally, the iSEE workshop was written for the Bioconductor conference 2019 to showcase the functionality of the iSEE package for both newcomers and experienced R users.
-->

<!-- F1000 Twitter teaser -->
<!-- {{< video library="1" src="iSEE/twitter-F1000.mp4" controls="yes" >}} -->
