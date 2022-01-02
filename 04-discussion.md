# Discussion {#general-discussion}

Bacterial cell survival is part of a complex biological system, which is
one of the fundamental problems of the health sector in this century. In
this work, we have analyzed the role of filamentation in cell survival
through multiple levels of complexity. Inquiring, one step at a time,
into the ecology of bacterial stress.

First, we exposed two bacterial strains, one with an antibiotic
resistance gene on the chromosome and one on multicopy plasmids, in a
stressful environment with ampicillin. In both cases, we observed four
states in the cells at the end of the experiment: live filamented, live
non-filamented, dead filamented, and dead non-filamented cells. By
inspecting the specific characteristics of each category, we were able
to identify that cell length was indeed related to the probability of
survival. In addition, we showed that each cell's inherent resistance
defined whether or not filamentation would occur for the plasmid strain,
where low resistance values were conducive to filamentation.

However, the growth rate was critical in determining the final cellular
state. We observed that moderate growths mainly were related to
survival. In contrast, rapid growth was associated with cell death.
Previous findings, in addition, could have other explanations that are
not mutually exclusive, such as the cell cycle or how fast a given cell
was dividing. So the contribution of these variables in conjunction with
filamentation could be a future study of interest to improve our
understanding of cell survival.

Our next step was to abstract the fundamental information to define a
mathematical model that would help us better understand the workings of
filamentation in cell survival. We postulated a mathematical model built
from a system of differential equations that considers the cell's
geometric relationships (i.e., a pill shape) against exposure to a toxic
substance in the environment. We assume that the consumption of
antibiotics by the cell is perceived through its surface area ($SA$),
while the cell volume ($V$) defines its concentration. Consequently,
since the rate of change of $SA$ is lower than $V$, this results in a
transient reduction in the intracellular concentration of the toxin.

In the experiments, we showed how cells begin to filament upon a pulse
of antibiotics, and from this, it would begin their bid for survival.
The model allowed us to consider thousands of different cells to
precisely determine the impact of filamentation on their survival. For
instance, upon incremental exposure to the toxic substance, a cell can
increase its lifetime window by simply growing. If the antibiotic wears
off before the cell reaches a threshold of death for some reason, it
will have paid off; the cell will have won the bet, and it will have
survived. Conversely, if a cell can not grow as a filament, it will
depend entirely on its inherent resistance levels.

In addition to the increase in the expected lifetime of the cell upon
exposure to a toxic agent, the model showed us that filamentation could
confer an increase in the Minimum Inhibitory Concentration (MIC). So if
a cell can grow as filament, a higher amount of the toxic agent will be
needed to kill it. However, bacteria generally live in heterogeneous
populations, and sometimes their inherent resistance levels will play a
vital role in their survival.

The model showed us that heterogeneity in toxin-antitoxin response
systems could represent a double-edged sword for cell survival depending
on the time of exposure to the toxin. Heterogeneity could be favorable
for survival if the time of exposure to the toxic agent is longer than
the time at which the population without heterogeneity dies completely,
while it would be detrimental otherwise. Thus, globally, filamentation,
both at the individual and population scale, is crucial for resilience.

However, although our model's advantages are its simplicity, ease of
interpretation, and reproducibility of the biological phenomenon in
question, it also entails limitations to be considered in further work.

Our model assumes zero growth if the cell does not reach the
filamentation threshold. While this may be true at the population
average level, the reality is that cells are constantly growing and
dividing. Integrating constant growth and division events could help us
understand in more detail how, under what conditions, and why
filamentation might be beneficial or detrimental when considering new
transition states.

Another limiting factor is the lack of a system that penalizes prolonged
filamentation. Once the cell filaments, our model considers only two
possible scenarios, the cell can either continue with filamentation for
its entire lifetime or die from crossing a toxic agent threshold.
However, we can suggest that maintaining a filamentary state carries an
energetic and membrane material cost that may be difficult to supply.
Thus, a cell could die from spending too long in the filamentation state
if exposure to the toxic agent does not cease.

The model does not consider what happens after the death of a cell or
its interactions with other population members. We could hypothesize
different scenarios: for instance, filament cells could absorb a more
significant amount of the toxic agent so that some surrounding cells
will not perceive much threat. On the other hand, if a cell dies,
eventually, the capabilities of the cell membrane disappear, and its
contents can diffuse into the environment. Hence, this would represent
an increase in the toxic agent's local concentration that nearby cells
could acquire. How would this change the overall dynamics of the system?
What would be the new cellular states when evaluating filamentation in
the context of cellular communities?

In conclusion, although we based our model on experimental evidence, it
does not consider all possible biological aspects. However, this allowed
us to analyze and better understand filamentation as a mechanism capable
of increasing the resilience of a bacterial population against a toxic
agent exposure, for example, antibiotics. Therefore, the generation of
new models and experiments to understand filamentation in-depth and its
implications for bacterial survival will be necessary to help us combat
the current problem of antibiotic resistance.
