\cleardoublepage

# (APPENDIX) Appendix {.unnumbered}

# Code availability

All code that we used in each phase of the project can be located on
Github. Below we listed the repositories used as well as a brief
description of their content.


Table: (\#tab:github-repositories-used)Github repositories used for this project.

|Repository                                                      |Description                                                                                                                                                                                                                                                                                                                                 |
|:---------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|<https://github.com/ccg-esb-lab/uJ>                             |It contains a series of programs in $\mu \mathrm{J}$, which consist of an $ImageJ$ macro library for quantifying unicellular bacterial dynamics in microfluidic devices. Besides, it includes all the Python code used for the image analysis processing and our developed custom Napari cell-viewer (see Chapter \@ref(image-processing)). |
|<https://github.com/jvelezmagic/undergraduate_research_project> |It contains all the files necessary to reproduce this document in its entirety. In addition, it includes the code used in R to analyze the tabular data of the experiments (see Chapter \@ref(experiment-analysis)).                                                                                                                        |
|<https://github.com/jvelezmagic/CellFilamentation>              |In includes all the Julia code used to create the mathematical filamentation model exposed in Chapter \@ref(model-analysis).                                                                                                                                                                                                                |

# Software tools

## Python

Below is the main list of packages used for Chapter
\@ref(image-processing)

-   Python [@10.5555/1593511].

-   dask [@rocklin2015dask].

-   ipython [@perez2007ipython].

-   matplotlib [@hunter2007matplotlib].

-   napari [@sofroniew2021a].

-   networkx [@hagberg2008exploring].

-   numpy [@2020NumPy-Array].

-   pandas [@mckinney2010data].

-   pickle [@van1995python].

-   scikit-image [@vanderwalt2014].

-   shapely [@shapely2007].

## R

Below is the main list of packages used for Chapter
\@ref(experiment-analysis) as well for the reproducibility of this
undergraduate research project.







- base [@R-base].
 - bookdown [@R-bookdown].
 - embed [@R-embed].
 - fs [@R-fs].
 - GGally [@R-GGally].
 - ggdist [@R-ggdist].
 - ggpubr [@R-ggpubr].
 - here [@R-here].
 - janitor [@R-janitor].
 - knitr [@R-knitr].
 - patchwork [@R-patchwork].
 - plotly [@R-plotly].
 - renv [@R-renv].
 - rmarkdown [@R-rmarkdown].
 - sessioninfo [@R-sessioninfo].
 - stringr [@R-stringr].
 - tidymodels [@R-tidymodels].
 - tidytext [@R-tidytext].
 - tidyverse [@R-tidyverse].

## Julia

Below is the main list of packages used for Chapter
\@ref(model-analysis).

-   Julia [@Julia-2017].
-   DrWatson.jl [@datseris2020].
-   DifferentialEquations.jl [@rackauckas2017differentialequations;
    @rackauckas2017adaptive; @rackauckas_stability-optimized_2018].
-   DataFrames.jl [@white2021].

# Software usage

## Undergraduate research project

This code base is using the `R Language` and `renv` to make a
reproducible scientific project named `undergraduate_research_project`.

1.  Clone the repository with:
    `git clone https://github.com/jvelezmagic/undergraduate_research_project`.
2.  Download latest version of [R](https://cran.r-project.org/).
3.  Open R project.
4.  Install the `renv` package with `install.packages('renv')`.
5.  Restore working environment with: `renv::restore()`.
6.  Render the book with: `bookdown::render_book()`.
7.  Edit documents and render again.

## Cell-viewer

This code base is using the `Python Language`.

1.  Clone the repository with:
    `git clone https://github.com/ccg-esb-lab/uJ`.
2.  Go to `single-channel` directory.
3.  Inside of `MGGT-AMP-Pulse` (*i.e.*, chromosome strain) or
    `pBGT-AMP-Pulse` (*i.e.*, plasmid strain) enter to
    `6_Lineages_corrector_napari.ipynb`.
4.  Change the parameters and use it.

## Filamentation model

This code base is using the `Julia Language` and `DrWatson` to make a
reproducible scientific project named `CellFilamentation`.

1.  Clone the repository with:
    `git clone https://github.com/jvelezmagic/CellFilamentation`.
2.  Download latest version of
    [Julia](https://julialang.org/downloads/).
3.  Open Julia project.
4.  Open Julia console and do the following to restore working
    environment:

``` {.julia}
using Pkg
Pkg.activate(".") # Path to the project.
Pkg.instantiate()
```

5.  Play with the model.

# Colophon

This undergraduate research project was written in
[RStudio](https://www.rstudio.com/products/rstudio/)
using [**bookdown**](https://bookdown.org).
The [website](https://jvelezmagic.github.io/undergraduate_research_project/) is
hosted via Github Pages, and the complete source is
available via Github.

This version of the project was built with R version 4.1.2 (2021-11-01) and the
following packages:


Table: (\#tab:colophon)Packages used to built the project documents.

|Package     |Version |Source         |
|:-----------|:-------|:--------------|
|bookdown    |0.24    |CRAN (R 4.1.0) |
|embed       |0.1.5   |CRAN (R 4.1.0) |
|fs          |1.5.1   |CRAN (R 4.1.0) |
|GGally      |2.1.2   |CRAN (R 4.1.0) |
|ggdist      |3.0.1   |CRAN (R 4.1.0) |
|ggpubr      |0.4.0   |CRAN (R 4.1.0) |
|here        |1.0.1   |CRAN (R 4.1.0) |
|janitor     |2.1.0   |CRAN (R 4.1.0) |
|knitr       |1.36    |CRAN (R 4.1.0) |
|patchwork   |1.1.1   |CRAN (R 4.1.0) |
|plotly      |4.10.0  |CRAN (R 4.1.0) |
|renv        |0.14.0  |CRAN (R 4.1.0) |
|rmarkdown   |2.11    |CRAN (R 4.1.0) |
|sessioninfo |1.2.1   |CRAN (R 4.1.0) |
|stringr     |1.4.0   |CRAN (R 4.1.0) |
|tidymodels  |0.1.4   |CRAN (R 4.1.0) |
|tidytext    |0.3.2   |CRAN (R 4.1.0) |
|tidyverse   |1.3.1   |CRAN (R 4.1.0) |
