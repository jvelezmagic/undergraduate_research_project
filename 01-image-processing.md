# Image processing {#image-processing}

## Introduction

With the progress of technology, optical and fluorescence microscopy has
become a fundamental tool for the characterization and understanding of
the bacterial world. Microscopy has allowed humanity to extend its
senses to observe the unknown world with exciting new perspectives that
they might never otherwise have envisioned. Furthermore, microscopy
offers a clear advantage over other techniques used to characterize
bacteria since it can acquire data from living cells in spatial
resolution [@schermelleh2019].

Including the discovery of fluorescent proteins (*e.g.*, GFP and DsRed)
and improvements in fluorescent reporters, it is possible to
specifically label specific cellular components and track cellular
functions [@Specht2017]. On the other hand, mechanical and intellectual
development of microfluidic research techniques provides an excellent
opportunity to overcome bio-medical and chemical techniques
[@convery2019]. Collectively, it is possible to study communities of
bacteria at the level of individual cells [@balaban2004a; @elowitz2002].

Although all this technological development has provided a significant
advance for the scientific community, after acquiring fluorescence
images, the extraction of quantitative properties from these images is
crucial, but unfortunately, a difficult step for analyzing experiments.
Not so long ago, image analysis in biology relied on manual
quantification. However, manual analysis suffers from two main problems:
1) accuracy and 2) scalability (that is, analyzing miles or more
images). Fortunately, improvements in image accuracy and computational
image analysis capabilities are revolutionizing the quantification of
biological processes through [@Caicedo2017; @Smith2018]. Therefore, the
manual correction required to analyze the experiments is minimal.

Here, we used a series of programs in $\mu \mathrm{J}$
(<https://github.com/ccg-esb-lab/uJ>), which consists of an
$\mathrm{ImageJ}$ macro library (mainly) for quantifying unicellular
bacterial dynamics in microfluidic devices [@schneider2012]. The
specific steps used are described below and are summarized in Figure
@ref(fig:).

## Preprocessing

We exported the figures obtained by the NIS-Elements software
(RRID:SCR_014329) from the microfluidics experiments in TIFF (Tagged
Image File Format) format. Each figure was named as follows:
*experimentxyc1t001* where *experiment* indicates the name assigned to
the experiment, *xy* the trap number, *c* the fluorescence channel, and
*t* the passage of time.

Subsequently, we compile the images, rename them and save them as images
in different folders. We maintained the classification by fluorescence
channels and phase contrast, and within the channel folder, it is the
sub-classification by trap number.

## Segmentation

To determine which parts of the photographs correspond to cells, we
carry out an image segmentation analysis. Segmentation consists of
classification at the pixel level, which allows us to define the pixels
that give identity to the limit of a cell, its interior, and the image's
background (everything that is not a cell). A new image is generated
from the above, known as the segmentation mask, containing only the
pixels that identify cells.

To build the segmentation mask, we used *Deepcell* [@vanvalen2016].
*Deepcell* is a network trained with a robust set of images that people
previously classified as cells. However, the generation of the
segmentation masks is not absolved of errors (see also Section
\@ref(manual-corrections)). Sometimes we must correct them manually due
to 1) mistakenly identifying two or more cells as one, 2) identifying
two or more cells when it is only one cell, and 3) failing to identify a
cell.

## Tracking

From the image segmentation, we obtain ROI files (region of interest),
which contain coordinates of the position of individual cells in each
photograph [@10.5555/1386553]. Tracking is the tracking of a region of
interest in a consecutive series of images. In this case, the tracking
generates the identification of the lineages, that is, the ancestry of
each cell.

We read the ROI files in Python through the *shapely* package, which
efficiently reconstructs polygons, thus calculating the length of the
cells [@10.5555/1593511; @shapely2007]. Also, in Python using ROI files,
we track cells with the k-nearest neighbors algorithm that uses various
properties such as fluorescence intensity, length, and shape of each
cell, to identify cell lineages [@altman1992].

## Manual corrections {#manual-corrections}

For cell-tracking manual correction, we used *Napari,* an open-source
python-based tool designed to explore, annotate, and analyze large
multidimensional images [@sofroniew2021a]. Our custom cell-viewer allows
us to easy lineage data visualization, custom-plotting, and
lineage-correction. Code for our cell-viewer is available on
<https://github.com/ccg-esb-lab/uJ/tree/master/single-channel>.

We produced high-throughput data of thousands of cells with a
single-cell resolution to the end of the lineages manual reconstruction.
We obtained data about time-series of fluorescent intensity,
morphological properties of individual cells (*e.g.*, elongation,
duplication rate), and time-resolved population-level statistics
(*e.g.*, probability of survival to the antibiotic shock).

## Data extraction

We construct a file in columnar format through image processing that
contains the information necessary to analyze each experiment (*i.e.*,
chromosomal and plasmids) in its different traps (*i.e.*, XY
identifier). See Table \@ref(tab:data-columns-specifications) for a full
description of the output data. Subsequently, the table was analyzed in
R for statistical computation and plotting (see Chapter
\@ref(experiment-analysis)) [@R-base].
  

+------------------------------------+------------------------------------------------------------------+
| Column                             | Description                                                      |
+====================================+==================================================================+
| experimentID                       | Unique identifier of the experiment.                             |
+------------------------------------+------------------------------------------------------------------+
| trapID                             | Unique identifier of the trap used.                              |
+------------------------------------+------------------------------------------------------------------+
| lineageID                          | Unique integer of the stem cell and its ancestry.                |
+------------------------------------+------------------------------------------------------------------+
| cellID                             | Unique identification number for each cell existing since the    |
|                                    | beginning of the experiment or generated later.                  |
+------------------------------------+------------------------------------------------------------------+
| motherID                           | Represents the identification number of the stem cell that gave  |
|                                    | rise to the progeny.                                             |
+------------------------------------+------------------------------------------------------------------+
| trackID                            | Indicates the x-y coordinates where the cell being tracked       |
|                                    | starts.                                                          |
+------------------------------------+------------------------------------------------------------------+
| roiID                              | Indicates the x-y position in which the cell is located,         |
|                                    | followed after each photograph.                                  |
+------------------------------------+------------------------------------------------------------------+
| frame                              | Number of the photograph in the sequence of photographs taken,   |
|                                    | indicating the elapsed time (10 minutes per frame).              |
+------------------------------------+------------------------------------------------------------------+
| length                             | Cell length.                                                     |
+------------------------------------+------------------------------------------------------------------+
| division                           | Indicates cell division events, represented by the value 1 when  |
|                                    | they occur and 0 otherwise.                                      |
+------------------------------------+------------------------------------------------------------------+
| GFP                                | Represents the relative fluorescence intensity in each cell by   |
|                                    | green fluorescent protein (*i.e.*, GFP).                         |
+------------------------------------+------------------------------------------------------------------+
| DsRed                              | Represents the relative fluorescence intensity for cells         |
|                                    | generated by rhodamine's internalization (*i.e.*, DsRed); an     |
|                                    | indicator of cell death events.                                  |
+------------------------------------+------------------------------------------------------------------+
| tracking_score                     | Determine how good or bad the tracking of a cell was.            |
+------------------------------------+------------------------------------------------------------------+
| state                              | Indicates the state of the cell determined from its length and   |
|                                    | fluorescence thresholds. -1 for death, 0 for normal, and 1 for   |
|                                    | filamentation (see Section                                       |
|                                    | \@ref(experiment-general-preprocessing) for detailed             |
|                                    | information).                                                    |
+------------------------------------+------------------------------------------------------------------+

: (\#tab:data-columns-specifications) Resulting table from image processing.
