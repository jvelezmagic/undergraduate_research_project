# Experiment analysis {#experiment-analysis}


















































































































































## Introduction

The previous chapter (see Chapter \@ref(image-processing)) detailed the
steps necessary to extract data from a set of microfluidic images
through image analysis techniques and fluorescence microscopy. Each step
was instrumental in creating a dataset that was easy to explore and ask
questions. With the help of computational biology, systems biology, and
data analysis techniques, we could process these files to help us in the
search to find the role of filamentation in cell survival.

Both the ideas and concepts of computational biology and systems biology
contributed to the development of this analysis. In principle,
computational biology originated after the origin of computer science
with the British mathematician and logistician Alan Turing (regularly
known as the father of computing) [@turing1950]. Over time, systems
biology emerged as an area that synergistically combines models and
experimental data to understand biological processes [@bruggeman]. Thus,
giving a step towards creating models that, in general, are
phenomenological but that sometimes serve to discover new ideas about
the process under study. Ideas and aspects of the study of biological
sciences that otherwise could be unthinkable without the computer's
power.

Here, we divide the experimental analysis into two main parts: 1) at the
cell level or measurements at specific points in time and 2) at the
population level and time series. The first level allowed us to identify
the individual contribution of each variable understudy to determine
cell survival. The second level allowed us to understand how the
population behaves according to the passage of time in the face of
exposure to a harmful agent (in this case, beta-lactam antibiotics).
Together, both visions of the same study phenomenon allowed us to
extract the main ideas for postulating a mathematical model that seeks
to show how filamentation is a factor for cell survival in stressful
environments (see Chapter \@ref(model-analysis)).

## General preprocessing of data {#experiment-general-preprocessing}

The raw data processing consisted mainly of creating two levels of
observation for the cells of both chromosomal strains and multicopy
plasmids. The first level is at a cell granularity, that is, point
properties. The second level consists of the cells over time, thus
observing properties at the population level. We did this because it
would allow us to understand what factors are affecting filamentation
and why.

We normalized the fluorescence values of DsRed and GFP for both
experiments based on the values observed before exposure to antibiotics.
It allowed us to have a basis to work with and compare expressions
between cells. In the case of DsRed environment drug concentration, we
also applied a logarithmic transformation to observe subtle changes in
fluorescence intensity that would allow us to detect cell dead.

Ultimately, we decided to classify cells into four fundamental groups
based on whether the cell filamented and survived (see Figure
\@ref(fig:experiment-03-cell-distribution-across-experiments)). We
define a *filamented cell* as a cell with more than two standard
deviations from the mean concerning the lengths observed before
introducing antibiotics into the system. On the other hand, although
there are multiple ways to define death from single-cell observations
[@trevors2012; @kroemer2008], we considered a *cell dead or missing*
when we stopped having information about it, either because of
fluorescence in the red channel was above a given threshold (resulting
from an increase in cell membrane permeability and the introduction of
fluorescent dye into the cell) or because it left the field of
observation. Therefore, a *surviving cell* is defined as a cell observed
before and after exposure to the antibiotic and does not surpass the
DsRed threshold.

(ref:experiment-03-cell-distribution-across-experiments-scap) Cell classification and its distribution across experiments.

(ref:experiment-03-cell-distribution-across-experiments-cap) **Cell classification and its distribution across experiments.** We define a *filamented cell* as a cell whose length exceeded two standard deviations from the mean at any time during the experiment. A *surviving cell* is a cell that was observed before and after exposure to the antibiotic. Accordingly, we removed from the analysis those cells that died before or were born after the exposure of the experiment. Therefore, we delimited the effect caused by the exposure to the antibiotic.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-cell-distribution-across-experiments-1.svg" alt="(ref:experiment-03-cell-distribution-across-experiments-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-cell-distribution-across-experiments)(ref:experiment-03-cell-distribution-across-experiments-cap)</p>
</div>

## Results

### Cell length and the amount of GFP are crucial in determining cell survival {#length-gfp-crucial}

We evaluated the DsRed, GFP, and length values for each cell at
different time points: initial, filamentation, and end. This
preprocessing allowed us to observe and quantify each cell at critical
times in the experiment and eliminate noise or signals outside the scope
of this investigation.

We define the *initial time* as the first time we observed the cell in
the experiment. *Filamentation time* equals when a cell reaches the
filamentation threshold (see Figure
\@ref(fig:experiment-03-length-temporal-distribution)) for the first
time. We defined the *end time* as the time of the last observation of
the cell. We decided to bound the end time for surviving cells to one
frame (10 min) after the end of antibiotic exposure so that the observed
signal would reflect the final stress responses.

When we compared the distributions of DsRed, GFP, and length for both
experiments, we observed its changes in its role for cell survival. In
Figure \@ref(fig:experiment-03-dsred-temporal-distribution), we show
that indistinctly and, as expected, surviving cells managed to eliminate
the antibiotic by the end time. In contrast, dead cells presented higher
levels of antibiotics (measured by proxy through the mean DsRed
intensity of the cell).

(ref:experiment-03-dsred-temporal-distribution-scap) DsRed temporal distribution.

(ref:experiment-03-dsred-temporal-distribution-cap) **DsRed temporal distribution.** To evaluate the incident effect of the antibiotic marked by DsRed on cells by class, we show its values at three key moments: start, filamentation (SOS), and end. The upper asterisks represent the significance value when comparing a group X to the filamented and surviving cell reference. Asterisks in a line indicate whether or not there is a significant difference in the survival of non-filamented cells. The black dots represent the mean of each group, and the lines that join them are a comparative guide. The extent of the black bars represents the distribution of the data. Although, at the initial time, we observe multiple significant differences, this is likely due to the intrinsic noise of the system since, as expected, the values are close to zero. We observed a difference between the surviving and non-filamented cells for the chromosomal strain for the SOS time, but the same did not occur for the plasmid strain. The final amount of DsRed makes a clear difference between survival and death.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-dsred-temporal-distribution-1.svg" alt="(ref:experiment-03-dsred-temporal-distribution-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-dsred-temporal-distribution)(ref:experiment-03-dsred-temporal-distribution-cap)</p>
</div>

On the other hand, GFP observations in Figure
\@ref(fig:experiment-03-gfp-temporal-distribution) showed us two
essential things for cell classification: 1) The chromosomal strain did
not exhibit noticeable changes in GFP levels, and 2) filamented cells
were those that had low fluorescent intensities (low plasmid
copy-number) at the beginning of the experiment. For the final
observation times, GFP measurements indicated that among the cells that
did not filament, the ones that survived exhibited a reduced GFP
expression concerning cells killed by the antibiotic. Meanwhile, for the
filamented cells, whether surviving or dead, their GFP measurements
indicated no difference at the beginning or the end of the experiment,
suggesting the presence of other determinants of cell survival.

(ref:experiment-03-gfp-temporal-distribution-scap) GFP temporal distribution.

(ref:experiment-03-gfp-temporal-distribution-cap) **GFP temporal distribution.** To evaluate the incident effect of the GFP on cells by class, we used the same notation as in Figure \@ref(fig:experiment-03-dsred-temporal-distribution). The chromosomal strain exhibits variability in GFP at different time points, mainly due to experimental noise resulting from low fluorescent intensity values. As expected, in the plasmid strain, filamented cells had a lower initial GFP. At the time of filamentation, there appear to be differences in fluorescence between surviving and dead cells. However, in the end time, we observed that the surviving non-filamented cells have lower GFP values than the non-filamented dead cells and alive filamented cells.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-gfp-temporal-distribution-1.svg" alt="(ref:experiment-03-gfp-temporal-distribution-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-gfp-temporal-distribution)(ref:experiment-03-gfp-temporal-distribution-cap)</p>
</div>

Cell length was one of the factors that GFP expression levels could not
explain for cell survival. In Figure
\@ref(fig:experiment-03-length-temporal-distribution), we show that the
conclusions regarding filamentation were applicable for both chromosomal
or plasmid strains. For the initial times, filamented and survived cells
were shorter in length than those that died but longer than not
filamented cells of both classes, while non-filamented cells did not
differ from each other. We observed no length differences between cells
at filamentation time. Thus, survival could depend on other factors,
such as growth rate. At the final time, the results were well-defined.
Surviving cells had a greater length relative to their non-surviving
pair (*i.e.*, dead filamented and non-filamented cells). However, for
filamented cells, surviving cells represent a distribution of higher
final length values in general but not as extensive as their dead
counterpart. Which we could explain as a length limit to which cells can
grow without dying. Nevertheless, we had no information to evaluate such
a hypothesis.

(ref:experiment-03-length-temporal-distribution-scap) Length temporal distribution.

(ref:experiment-03-length-temporal-distribution-cap) **Length temporal distribution.** To evaluate the incident effect of length on cells by class, we use the same notation as in Figure \@ref(fig:experiment-03-dsred-temporal-distribution). The observations for both strains, chromosomal or plasmid, are the same. In the beginning, the surviving filamented cells already have a difference in length concerning the rest of the classes. At the time of filamentation, there is no difference to help determine whether the cell will survive or not. Finally, in the final time, it seems that the surviving filamented cells have a greater length than the rest of the groups. However, this length is moderate compared to the excess length shown by non-surviving filamented cells. On the other hand, we highlighted the growth of the surviving non-filamented cells. Therefore, although they did not reach a length for us to classify as filamented, the cells did resort to filamentation.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-length-temporal-distribution-1.svg" alt="(ref:experiment-03-length-temporal-distribution-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-length-temporal-distribution)(ref:experiment-03-length-temporal-distribution-cap)</p>
</div>

Once we observed the effects of GFP expression levels and lengths in
determining whether a cell lives or dies, we projected the cells onto
the plane and painted them with their class status (See Figure
\@ref(fig:experiment-03-cell-distribution-across-experiments)) to
determine whether these two variables contained the necessary
information to cluster the data correctly. In Figure
\@ref(fig:experiment-03-just-initial-values), we show the initial GFP
and length values projection. While, with some work, we could
contextually place the results in Figures
\@ref(fig:experiment-03-gfp-temporal-distribution) and
\@ref(fig:experiment-03-length-temporal-distribution), the initial
values did not appear to determine the classes. Therefore, we explored
the final versus initial values differences in Figure
\@ref(fig:experiment-03-metric-differences). With this new
representation of the cells in the plane, we contextualized the
statistical results presented in Figures
\@ref(fig:experiment-03-gfp-temporal-distribution) and
\@ref(fig:experiment-03-length-temporal-distribution). Besides, it
showed us that differences in length (*i.e.*, filamentation) and
reductions in GFP expression are essential in determining cell survival.
Though, the clustering of cells by state is not completely separated,
which means that other variables are affection the experimental results
in cell survival.

(ref:experiment-03-just-initial-values-scap) Experiment initial values.

(ref:experiment-03-just-initial-values-cap) **Experiment initial values.** By positioning a cell in space based on its initial length and GFP values, we can see that class separation occurs, but not as a strong signal. Therefore, we concluded that although the initial state influences the result, this is not everything. For this, we have the example of the length changes throughout the experiment caused by filamentation. In this graph, the GFP scale is at log10 to help us observe those minor differences between the experiments.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-just-initial-values-1.svg" alt="(ref:experiment-03-just-initial-values-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-just-initial-values)(ref:experiment-03-just-initial-values-cap)</p>
</div>

(ref:experiment-03-metric-differences-scap) Experiment initial values differences.

(ref:experiment-03-metric-differences-cap) **Experiment initial values differences.** By comparing the metric differences of the last observation and the first observation of a cell, we can separate mainly the surviving filamented cells from those that did not do it in both experiments (green dots). Meanwhile, cells with plasmids form a small accumulation of surviving cells that did not produce filament (purple dots). However, this has made a breakthrough in understanding what is affecting cell survival. There are still variables that we can include to understand this phenomenon better.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-metric-differences-1.svg" alt="(ref:experiment-03-metric-differences-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-metric-differences)(ref:experiment-03-metric-differences-cap)</p>
</div>

### Number of divisions and cell age do not appear to play a clear role in determining cell survival

In Section \@ref(length-gfp-crucial), we explored how GFP variability
and cell length influence cell survival. However, Figures
\@ref(fig:experiment-03-just-initial-values) and
\@ref(fig:experiment-03-metric-differences) showed us the possibility of
other factors relevant to the phenomenon under study. As some papers in
the literature suggest, some of these other factors may be cell division
and chronological age (*i.e.*, how much time has passed since the last
cell division at the time of exposure to a toxic agent)
[@moger-reischer2019; @roostalu2008; @heinrich2015]. Therefore, we chose
to observe these two metrics in experiments at a purely qualitative
level, i.e., without the inclusion of, e.g., metrics of membrane or cell
cycle properties [@Joseleau-Petit1999].

Although we expected to see a small contribution, either by the number
of divisions or cell age, in Figures
\@ref(fig:experiment-03-number-divisions) and
\@ref(fig:experiment-03-time-since-last-division), we could not observe
a precise effect of these variables on cell survival. Patterns that,
although they could have an explanation or biological significance, we
decided to omit as relevant in the characterization of our cells, since
the signal was not clear. However, we derived from this analysis a
slightly simpler variable that tells us whether a cell underwent a cell
division event or not. So it gives us a more generalized picture of the
contribution of division to cell survival (see Figure
\@ref(fig:experiment-03-plasmid-pca-variable-contribution)).

(ref:experiment-03-number-divisions-scap) Cell's number of divisions.

(ref:experiment-03-number-divisions-cap) **Cell's number of divisions.** Chromosomal cells exhibited more divisions for surviving classes and non-surviving filamented cells (*i.e.*, purple, green, and red dots) relative to unchanged behavior in plasmid cells. Therefore, its contribution to filamentation remains uncertain.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-number-divisions-1.svg" alt="(ref:experiment-03-number-divisions-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-number-divisions)(ref:experiment-03-number-divisions-cap)</p>
</div>

(ref:experiment-03-time-since-last-division-scap) Time elapsed since the last division at the beginning of the experiment.

(ref:experiment-03-time-since-last-division-cap) **Time elapsed since the last division at the beginning of the experiment.** The mean time of the last division before starting the experiment indicates that it did not influence the final result for chromosomal cells. There is a slight difference between the filamented-not survived cells and the rest for cells with plasmids. However, the signal does not appear to be strong on the survival role. Therefore, we conclude that we have no evidence to support that the time of the last division at the beginning of the experiment influences the final classification results.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-time-since-last-division-1.svg" alt="(ref:experiment-03-time-since-last-division-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-time-since-last-division)(ref:experiment-03-time-since-last-division-cap)</p>
</div>

### Time to reach filamentation matters in determining cell survival

In Figures \@ref(fig:experiment-03-dsred-temporal-distribution),
\@ref(fig:experiment-03-gfp-temporal-distribution), and
\@ref(fig:experiment-03-length-temporal-distribution), we showed how, at
the time of filamentation, DsRed and GFP levels appeared indifferent to
the cells. Therefore, we hypothesized that a possible variable that
could determine cell survival could be its time to activate its
anti-stress response system that causes filamentation. Furthermore, we
also guided our hypothesis by previous reports showing us how the gene
expression level can induce filamentation with tight temporal
coordination [x].

While, for our analyses, we did not measure the concentration of
antibiotic that triggers filamentation per se, we indirectly quantified
its effect by using the time it took for a cell to reach a length at
which it is already considered a filamentating cell. Furthermore, to
recognize that the observed effect was a product of the experiment, we
decided to keep only filamented cells just once antibiotic exposure
began.

Figure \@ref(fig:experiment-03-time-to-filamentation-filtered) shows how
filamentation times are narrower for chromosomal cells than for
plasmid-bearing cells. Then, we hypothesize that the effect could come
from the heterogeneity in the plasmid copy number in the population.
Also, interestingly, we observed that, for both experiments, cells that
survived had longer filamentation times than the cells that died. These
differences in response times suggest the following: 1) if the cell
grows too fast, it will reach a limit and start to accumulate
antibiotics constantly, and 2) if the cell grows too fast, it is likely
that the cost of maintaining an ample length for prolonged periods of
exposure will become counterproductive.

(ref:experiment-03-time-to-filamentation-filtered-scap) Time to filamentation filtered.

(ref:experiment-03-time-to-filamentation-filtered-cap) **Time to filamentation filtered.** To quantify the effect of filamented to survive, we filtered those cells that filamented during the experiment. In this way, we normalize the start times for the calculation of the filamentation time. For both strains, the filamentation time had a more significant delay in the surviving cells.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-time-to-filamentation-filtered-1.svg" alt="(ref:experiment-03-time-to-filamentation-filtered-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-time-to-filamentation-filtered)(ref:experiment-03-time-to-filamentation-filtered-cap)</p>
</div>

In Figure \@ref(fig:experiment-03-initial-values-with-time), we decided
to project the results of Figure
\@ref(fig:experiment-03-time-to-filamentation-filtered) in a space
similar to the one described in Figure
\@ref(fig:experiment-03-just-initial-values). Thus, we separated our
data into cells that survived and cells that did not, and painted them
when it took them to reach their filamented state. We realized that,
indeed, by adding this temporal component to the initial variables of
length and GFP, we could separate surviving cells from dead cells to a
greater degree. However, it may still not be enough, and there are still
many other variables that play a crucial role in understanding the
ecology of stress and how some cells will be survivors or not.

(ref:experiment-03-initial-values-with-time-scap) Experiment initial values with time to filamentation.

(ref:experiment-03-initial-values-with-time-cap) **Experiment initial values with time to filamentation.** As in Figure \@ref(fig:experiment-03-just-initial-values), including the time it will take for cells to filament allows us to understand the phenomenon of survival better. Cells that filamented and survived generally have a much higher delay than their non-filamented peers for both strains (see Figure \@ref(fig:experiment-03-time-to-filamentation-filtered)).

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-initial-values-with-time-1.svg" alt="(ref:experiment-03-initial-values-with-time-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-initial-values-with-time)(ref:experiment-03-initial-values-with-time-cap)</p>
</div>

### Increasing the complexity of the system and analyzing it in an unsupervised way allows a correct classification of cell states

In the experiments, we observed the importance of GFP filamentation and
variability for cell survival. Similarly, we realized that other
variables must be affecting the final results. Filamentation and GFP
variability alone did not fully recapitulate the expected behavior of
the data. That is, the target variables did not capture the
heterogeneity of the system.

The inability to reproduce cell classification led us to question two
things: 1) the possibility that our sorting was wrong beforehand and 2)
we did not have enough variables to capture the study phenomenon. We
decided to take the unsupervised learning way to answer these subjects
because it allows us to project our data without a *priori* knowledge
[x].

We opted for the path of dimensionality reduction techniques where each
variable or feature is equivalent to one dimension. The essence of
dimensionality reduction is that it is not feasible to analyze each
dimension with many dimensions. Furthermore, dimensionality reduction
helps us counteract several problems such as reducing the complexity of
a model, reducing the possibility of overfitting a model, removing all
correlated variables, and, of course, visualizing our data in a two- or
three-dimensional space for better appreciation [x]. Improved
visualization and identification of essential variables are the main
reasons to guide and complement our research with this technique.

#### Principal Component Analysis (PCA) emphasizes the importance of cell length and its GFP in cell survival

The first dimensionality reduction technique we decided to use was
Principal Component Analysis (PCA) [@pearson1901; @hotelling1936].
Scientist mainly uses PCA to create predictive models or in Exploratory
Data Analysis (EDA). In our case, we only use it as an EDA.

For chromosomal and plasmid strain, in Figures
\@ref(fig:experiment-03-chromosome-pca-new-coordinates) and
\@ref(fig:experiment-03-plasmid-pca-new-coordinates), we show the
projection of the first two principal components (PCs), respectively.
Figure \@ref(fig:experiment-03-chromosome-pca-new-coordinates) separates
the manually annotated classes, surviving cells separated from
non-surviving cells. However, for Figure
\@ref(fig:experiment-03-plasmid-pca-new-coordinates), the class
separation was a bit rougher but allowed us to separate the surviving
filament cells from the dead ones.

(ref:experiment-03-chromosome-pca-new-coordinates-scap) Principal Component Analysis of chromosomal strain.

(ref:experiment-03-chromosome-pca-new-coordinates-cap) **Principal Component Analysis of chromosomal strain.** When integrating the information of different variables in a dimensionality reduction analysis, we observed a clear separation between the surviving cells and those that did not. The contributions that determined this phenomenon come mainly from the last amount of DsRed, GFP, and cell length (see Figure \@ref(fig:experiment-03-chromosome-pca-variable-contribution)). Although it seems obvious, it effectively confirms that the temporal classification that we carry out makes sense. Longer length represents a greater uptake of antibiotics but in a much larger volume, so the net effect is an internal reduction of antibiotics (see Figure \@ref(fig:model-01-cell-dimensions-relationship)).

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-chromosome-pca-new-coordinates-1.svg" alt="(ref:experiment-03-chromosome-pca-new-coordinates-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-chromosome-pca-new-coordinates)(ref:experiment-03-chromosome-pca-new-coordinates-cap)</p>
</div>

(ref:experiment-03-plasmid-pca-new-coordinates-scap) Principal Component Analysis of plasmid strain.

(ref:experiment-03-plasmid-pca-new-coordinates-cap) **Principal Component Analysis of plasmid strain.** By integrating the information from different variables in a dimensionality reduction analysis, we observed a clear separation between the filamented and non-filamented cells. Said class separation is given by component 2 (Y-axis), which is determined primarily by the initial and final lengths of the cells (see Figure \@ref(fig:experiment-03-plasmid-pca-variable-contribution)). Furthermore, the classification also allows us to separate those filamented cells that died from those that survived. Therefore, despite the increase in the system's complexity, length plays a role in determining survival.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-plasmid-pca-new-coordinates-1.svg" alt="(ref:experiment-03-plasmid-pca-new-coordinates-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-plasmid-pca-new-coordinates)(ref:experiment-03-plasmid-pca-new-coordinates-cap)</p>
</div>

For their part, in Figures
\@ref(fig:experiment-03-chromosome-pca-variable-contribution) and
\@ref(fig:experiment-03-plasmid-pca-variable-contribution), we show the
total contribution of each variable per PC for the chromosomal and
plasmid strain, respectively. Finding that, indeed, filamentation plays
a crucial role in determining cell survival. For example, for PC2, we
appreciated how the variable end DsRed directed the dots to the
positive side, while the variable end and start length directed the dots
to the opposing side. Therefore, we can support that filamentation has a
role in moving cells away from having higher amounts of DsRed.

(ref:experiment-03-chromosome-pca-variable-contribution-scap) Variables contribution of Principal Component Analysis of chromosomal strain.

(ref:experiment-03-chromosome-pca-variable-contribution-cap) **Variables contribution of Principal Component Analysis of chromosomal strain.** In the figure \@ref(fig:experiment-03-chromosome-pca-new-coordinates), we see that the classes we created manually reflected what we observed when performing a reduction of dimensions analysis. Here we show the individual contribution of each variable for the first two components. The variables that most affected components 1 and 2 (X-axis and Y-axis, respectively) are the final measurements of DsRed, GFP, length, and the initial amount of GFP. Given that they are chromosomal strains, we should note that this variability could be produced by intrinsic experimental noise that we could not remove. With that in mind, having the DsRed and the final length highlights the inherent role of cells by having increased its size.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-chromosome-pca-variable-contribution-1.svg" alt="(ref:experiment-03-chromosome-pca-variable-contribution-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-chromosome-pca-variable-contribution)(ref:experiment-03-chromosome-pca-variable-contribution-cap)</p>
</div>

(ref:experiment-03-plasmid-pca-variable-contribution-scap) Variables contribution of Principal Component Analysis of plasmid strain.

(ref:experiment-03-plasmid-pca-variable-contribution-cap) **Variables contribution of Principal Component Analysis of plasmid strain.** In Figure \@ref(fig:experiment-03-plasmid-pca-new-coordinates), we saw that we could separate the filamented cells from the non-filamented ones. The reduction analysis also shows a slight difference between surviving and dead cells within the small group of filamented cells. Here we offer the individual contribution of each variable for the first two components. For the first component (x-axis in Figure \@ref(fig:experiment-03-chromosome-pca-new-coordinates)), the initial and final GFP measurements received mainly the variability. We expected this component's importance since, being a chromosomal strain, we hope that its inherent variation will be inherited into the system. On the other hand, the second component (Y-axis in Figure \@ref(fig:experiment-03-chromosome-pca-new-coordinates)) was determined by the length of the cell. Factors that, in the chromosomal strain (see Figure \@ref(fig:experiment-03-chromosome-pca-variable-contribution)), determined with the help of DsRed the separation between surviving and dead cells.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-plasmid-pca-variable-contribution-1.svg" alt="(ref:experiment-03-plasmid-pca-variable-contribution-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-plasmid-pca-variable-contribution)(ref:experiment-03-plasmid-pca-variable-contribution-cap)</p>
</div>

#### Uniform Manifold Approximation and Projection (UMAP) correctly represents the local structure of cell states

Staying with only a one-dimensionality reduction technique was not an
option, so we used the UMAP technique [@mcinnes2018umap]. We mainly
decided to use UMAP for clustering purposes and see if the annotated
clusters corresponded to the manually annotated ones. UMAP has certain
advantages for these purposes, e.g., it preserves the global structure
across the whole space, so the distances between clusters matter.

In Figures \@ref(fig:experiment-03-chromosome-umap-new-coordinates) and
\@ref(fig:experiment-03-plasmid-umap-new-coordinates), we show how,
using the same variables used in the "PCA" section, UMAP was able to
cluster the four proposed classes correctly. Interestingly, in Figure
\@ref(fig:experiment-03-chromosome-umap-new-coordinates), UMAP formed
three general groups and four for Figure
\@ref(fig:experiment-03-plasmid-umap-new-coordinates). However, in
general, UMAP clustered the surviving cells from those that did not
survived. On investigating why this separation occurred, we found that
the large groups coalesced into one another if we eliminated the
division variable. So, in a way, the division also has a role in
determining survival, but it is not essential or at least not
over-represented in our data.

(ref:experiment-03-chromosome-umap-new-coordinates-scap) UMAP coordinates of chromosome strain.

(ref:experiment-03-chromosome-umap-new-coordinates-cap) **UMAP coordinates of chromosome strain.** We represented the cells in a low dimensional space. This new projection made it possible to group the cells that survived and those that did not. Therefore, as in PCA Figure \@ref(fig:experiment-03-chromosome-pca-new-coordinates), this technique supports the manual classification that we carry out.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-chromosome-umap-new-coordinates-1.svg" alt="(ref:experiment-03-chromosome-umap-new-coordinates-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-chromosome-umap-new-coordinates)(ref:experiment-03-chromosome-umap-new-coordinates-cap)</p>
</div>

(ref:experiment-03-plasmid-umap-new-coordinates-scap) UMAP coordinates of plasmid strain.

(ref:experiment-03-plasmid-umap-new-coordinates-cap) **UMAP coordinates of plasmid strain.** As in its \@ref(fig:experiment-03-chromosome-umap-new-coordinates) pair, the representation in a low-dimensional space helped classify the cells, grouping mainly into four groups, two of survivors and two of non-survivors. The variable *division* marks the separation of classes. The *division* variable indicates whether a cell is divided during its lifetime or not. Together, the UMAP represents the manually assigned classes.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-03-plasmid-umap-new-coordinates-1.svg" alt="(ref:experiment-03-plasmid-umap-new-coordinates-cap)" width="100%" />
<p class="caption">(\#fig:experiment-03-plasmid-umap-new-coordinates)(ref:experiment-03-plasmid-umap-new-coordinates-cap)</p>
</div>

### Population dynamics reveal how filamentation contributes cell survival

From the full tracking dataset, we evaluated how the different cell
states behaved over time---for example, understanding how the cells
absorbed antibiotics or how they elongated in time. In contrast to the
dataset generated in the \@ref(length-gfp-crucial) section, we did not
truncate the results 10 minutes after the antibiotic exposure. In this
way, we were able to observe cell behavior before and after the presence
of the toxic agent.

In Figure \@ref(fig:experiment-04-status-with-dead), we observed a small
fraction of cells that were already filamentous without exposure to the
toxic agent in both cell strains. However, after the onset of antibiotic
exposure at minute 60, we observed increases in the proportion of
filamented cells. It is interesting to note how filamented cells grew
after antibiotic exposure for the chromosomal strain. We speculate that
this post-antibiotic growth exists because, once the SOS system that
triggers filamentation is activated, the system continues to grow until
it reaches a limit regardless of whether the damaging agent is still
present or not [@justiceMorphologicalPlasticityBacterial2008;
@mückl2018]. Moreover, we observed how the cells start to divide again
after some time because the proportion of non-filament cells starts to
grow while the filament cells start to divide. We observed the same
effects for the plasmid strain. However, by experimental design, the
number of filament cells expected was much lower.

(ref:experiment-04-status-with-dead-scap) Population status over time.

(ref:experiment-04-status-with-dead-cap) **Population status over time.** We calculate how many cells of each type existed for each time point: non-filamented and filamented living cells (blue and green areas, respectively) and dead cells (red area; we considered *dead* cells as those cells that existed at one time and then stopped tracking). The black vertical lines represent the start and end of antibiotic exposure for each experiment. The effect of filamentation and its spread after exposure to the antibiotic is evident for the chromosomal strain. The experiment was finalized with the resolution of the cells when they returned to their non-filamented state. For its part, for the plasmid strain, it is observed how the filamented cells begin to appear slowly. Their proportion is as expected, given that the population had a wide distribution of GFP that allowed them to combat exposure to the antibiotic.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-04-status-with-dead-1.svg" alt="(ref:experiment-04-status-with-dead-cap)" width="100%" />
<p class="caption">(\#fig:experiment-04-status-with-dead)(ref:experiment-04-status-with-dead-cap)</p>
</div>

In Figure \@ref(fig:experiment-04-metrics-over-time), we showed how once
antibiotics exposure began, those cells that died had a much faster
increase in DsRed than those that did manage to live, regardless of
whether they filamented or not. On the other hand, surviving cells
managed to maintain their DsRed levels relatively stable. We noted that
length was critical for the surviving cells for the chromosomal strain
by turning to the GFP and length variables for a temporal explanation.
Even cells categorized as non-filamented reached the filamentation
threshold minutes after antibiotic exposure. However, the distinction of
live or dead filamented cells was not as evident as expected. As for
cells with plasmids, the effect on GFP for surviving cells was
maintained for filamented cells and decreased for non-filamented cells.
For the filament cells that died, we showed that they had, on average, a
much longer initial length than the surviving cells, so we also consider
it as a necessary factor in understanding which variables affect cell
survival.

(ref:experiment-04-metrics-over-time-scap) Population measurements over time.

(ref:experiment-04-metrics-over-time-cap) **Population measurements over time.** The colored lines symbolize the average value of each metric at each instant of time, while its surrounded gray shaded area represents the 95% confidence interval. The vertical lines represent the start and end of antibiotic exposure. The horizontal line in the length metric symbolizes the threshold to consider a cell filament. We observed a faster increase of DsRed for the non-surviving populations in both experiments. Regarding the GFP metric, the behavior is relatively stable for the chromosomal strain. In contrast, for the plasmid strain, a decline in GFP is observed for the population that did not survive. For the length metric, it is interesting to note how the chromosome cells that did not filament continued to grow past the filamentation threshold once the exposure to the antibiotic in the chromosomal strain had ended. On the other hand, the filamented and dead cells seem to have a greater length from the beginning for the plasmid strain.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-04-metrics-over-time-1.svg" alt="(ref:experiment-04-metrics-over-time-cap)" width="100%" />
<p class="caption">(\#fig:experiment-04-metrics-over-time)(ref:experiment-04-metrics-over-time-cap)</p>
</div>

### Heterogeneity in plasmid copy-number allows various forms of survival in addition to filamentation

We are confident that filamentation has a fundamental role in
determining cell survival, with what we have shown so far. However, for
plasmid cells, we have a component that is of our complete interest;
heterogeneity. Each cell can possess a different plasmid copy-number;
thus, each could show a different behavior under stress
[@sanmillan2016]. For instance, heterogeneity can produce resistant
cells that do not suffer damage, susceptible cells, and cells that form
filaments to mitigate environmental stress.

To study the effect of variability in plasmid copy number in the
survival probability of the population, we decided to group cells by the
proportion of initial GFP with respect to the population maximum. We
defined 100% of the population as the number of total cells at the onset
of antibiotic exposure. Figure
\@ref(fig:experiment-04-proportion-living-cells-gfp-by-row) shows how
the cells with the highest amount of GFP remained unchanged once
antibiotic exposure began, while the rest of the cells started to
decrease their percentage of surviving cells. However, the decrease was
not linear. On the contrary, we observed a bi-modal distribution on the
reduction of live cells. An average GFP point provided higher survival
than a point below or above the average (except for cells very close to
the population maximum).

(ref:experiment-04-proportion-living-cells-gfp-by-row-scap) Population survivals binned by initial GFP over time.

(ref:experiment-04-proportion-living-cells-gfp-by-row-cap) **Population survivals binned by initial GFP over time.** We categorized the cells' GFP into ranges of proportions 0.05 concerning the maximum amount of GFP in the population. 100% cells per bin of GFP was taken as the number of cells one frame before the start of exposure to the antibiotic (minute 50). Therefore, dark to light colors represent a generation of new cells, and light to dark colors the death of cells. The black vertical bars represent the start and end of the antibiotic exposure. Bars size and color on the right represent the percentage of the living cells 10 minutes after the end of the experiment. As shown in Figure \@ref(fig:experiment-04-gfp-survival-probability), we showed that the surviving cells appear to follow something similar to a bimodal distribution. More cells survive with a moderate amount of GFP or with an amount close to the maximum of the population.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-04-proportion-living-cells-gfp-by-row-1.svg" alt="(ref:experiment-04-proportion-living-cells-gfp-by-row-cap)" width="100%" />
<p class="caption">(\#fig:experiment-04-proportion-living-cells-gfp-by-row)(ref:experiment-04-proportion-living-cells-gfp-by-row-cap)</p>
</div>

Therefore, what we observed was a bimodal distribution for GFP-dependent
cell survival. In order to show this effect more clearly, in Figure
\@ref(fig:experiment-04-gfp-survival-probability), we plotted the
survival probability for each GFP bin without normalizing for the
population maximum. This new plot allowed us to observe how the bimodal
survival distribution occurs for cells that did not grow as filaments,
whereas cells that filament increase their survival probability
gradually as they have more initial GFP (see also Figure
\@ref(fig:experiment-03-gfp-temporal-distribution)).

(ref:experiment-04-gfp-survival-probability-scap) Plasmid initial GFP survival probability.

(ref:experiment-04-gfp-survival-probability-cap) **Plasmid initial GFP survival probability.** We calculated the survival probability after comparing the population distributions of GFP with those of the cells that managed to survive. To assess survival by GFP, we only used plasmid cells. For non-filamented cells (blue dots), a bell forms with an upturned tail. On the other hand, for the filamented cells (red dots), a continuous increase in survival is shown just when it seems that the probability of the non-filamented cells has decreased. In global, much GFP has higher resistance, but an average GFP value without filamentation also increases the probability of survival.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-04-gfp-survival-probability-1.svg" alt="(ref:experiment-04-gfp-survival-probability-cap)" width="100%" />
<p class="caption">(\#fig:experiment-04-gfp-survival-probability)(ref:experiment-04-gfp-survival-probability-cap)</p>
</div>

As in Figure \@ref(fig:experiment-04-gfp-survival-probability), in
Figure \@ref(fig:experiment-04-length-survival-probability), we show the
survival probability given an initial length. We observe that survival
is higher for cells that did not grow as filament if the initial length
was less than the average. In contrast, for filamented cells, the
probability of survival increased as cells length was longer at the
beginning of the experiment (see also Figure
\@ref(fig:experiment-03-length-temporal-distribution)). However, it is
noteworthy that the probability of survival had a limit in which a
higher initial length meant a lower probability of survival (see red
dotted lines in Figure
\@ref(fig:experiment-04-length-survival-probability)).

(ref:experiment-04-length-survival-probability-scap) Plasmid initial length survival probability.

(ref:experiment-04-length-survival-probability-cap) **Plasmid initial length survival probability.** We calculated the survival probability after comparing the population distributions of length with those of the cells that managed to survive. For non-filamented cells (blue dots), the survival probability is higher for those cells with initial lengths and small. It seems to decrease with a more extensive initial size. For their part, for filamented cells (red dots), the probability of survival increases according to their length but then declines when the cells are too long at first (see red dotted line). Therefore, in general, a small and moderate length or an initial length already filamented from the beginning increases the chances of survival.

<div class="figure">
<img src="02-experiment-analysis_files/figure-epub3/experiment-04-length-survival-probability-1.svg" alt="(ref:experiment-04-length-survival-probability-cap)" width="100%" />
<p class="caption">(\#fig:experiment-04-length-survival-probability)(ref:experiment-04-length-survival-probability-cap)</p>
</div>

## Discussion

Here, we evaluated different variables that could determine cell
survival upon exposure to toxic agents by studying two experimental
populations of *E. coli*, one strain with a resistance gene on the
chromosome and the other on multicopy plasmids. We identified two
variables that are predominantly responsible for cell survival: cell
length and GFP amount related to the cell's inherent resistance to the
toxic agent and heterogeneity in response times.

On the other hand, as other studies have already mentioned
[@heinrich2015; @wang2009], we examined cell activity and youth in a
minimalistic way. While the distribution of the number of divisions
exemplifies a broader and more uniform range for the surviving cells,
the cells that died showed a tendency to a lower number of divisions.
However, for the study of cellular youth at the time of exposure to the
toxic agent, the results did not show a clear pattern of behavior for
cell fate determination. Therefore, it would be interesting to study
cellular youth at a higher level of complexity in future studies to
understand its contribution to cell survival.

Interestingly, when we used temporal measurements of cell length, GFP,
DsRed, and if a cell divided, we could recapitulate, for the most part,
the fates of cellular states (see Sections \@ref(length-gfp-crucial) and
\@ref(increasing-the-complexity-of-the-system-and-analyzing-it-in-an-unsupervised-way-allows-a-correct-classification-of-cell-states)).
Thus, increasing the system's complexity led to better clustering cell
states, but not how these factors interact biologically in determining
cell survival. Therefore, we decided to postulate a mathematical model
that helps us understand the critical components in cell survival.
