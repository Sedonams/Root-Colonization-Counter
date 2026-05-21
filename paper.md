---
title: 'A Digital Microscopy Counter: Keyboard-Driven Web Application for Rapid Counting and Data Integrity Stewardship'
tags:
  - arbuscular mycorrhizal fungi
  - root colonization
  - web application
  - microscopy
  - soil ecology
authors:
  - name: Sedona Marie Spann
    orcid: 0009-0006-9844-1235
    affiliation: "1"
affiliations:
 - name: School of Earth and Sustainability, Northern Arizona University, Flagstaff, Arizona, United States
   index: 1
date: 20 May 2026
bibliography: paper.bib
---

# Summary

“Scoring” or quantifying fungal root colonization is a foundational task in 
plant-soil ecology. Current methods rely commonly on physical hand counters
necessitating post hoc data transcription, which is inherently inefficient and 
introduces potential error. The Radical Root Colonization Counter, a lightweight 
web application, was designed to streamline grid intersect root scoring. This 
tool enables rapid counting using personalized keyboard key combinations, audio
feedback for quality control, customizable counter categories, and automated 
session data recording. Each sample “score” (total structure counts of one 
sample) is stored locally and can append, or be exported as, a csv file ready 
for statistical analyses.By removing manual transcription, adding immediate 
audio confirmation of structures recorded, and streamlining data input as well
as output, this application improves the efficiency and data integrity of 
human-scored root colonization workflows. The design process of this tool also 
demonstrates the utility of iterative, user-driven development supported by 
AI-assisted prototyping in the creation of specialized tools used for improving
scientific methods.

# Statement of need

Quantification of root colonization is an informative and often cost effective 
metric in studies of plant-microbe interactions and soil ecosystem function 
[@Brundrett:2009]. Innovative tools, such as AMFinder [@Evangelisti:2021], 
can score root images digitally, and with more accuracy than grid 
intersect methods; but this technique requires the user to scan or photograph 
each slide and have the technical proficiency to utilize the software. 
Therefore the decision is often made to use common human-scoring approaches, 
those being grid intersect methods, which rely on visual assessment of a 
representative subsample of root segments under compound microscope and 
classification of observed fungal root-colonizers that vary by experiment 
(e.g., Arbuscular Mycorrhizal Fungal (AMF)  Structures, dark septate endophytes, 
non-am hyphae, plasmodiophorids, olpidium structures). Counting is often done 
on hand counters followed by transcription of scores from the counter onto a 
paper worksheet or into a digital spreadsheet. Grid intersect methods have 
several limitations. First, each button on a hand counter corresponds to a 
structure, counter buttons are often being relabeled in a shared lab based on 
personal preference and an experiment's ‘structures-present’ specificity. This 
can add time to set up when button locations must be relabeled between scoring 
sessions. Second, transcription of counts from physical into digital datasets is 
time-consuming and introduces opportunities for scribal error. Third, all buttons
produce the same “click” sound, which can increase error at speed because the 
sound confirms a button press, but not necessarily the correct button. Both new 
and old hand counters are also known to erroneously ‘click’ yet not add to a count, 
therefore best practice necessitates looking up from a slide to make sure the 
counter has counted, adding unnecessary mental load and seconds to every 
intersection (a single root scored on a slide). Seconds will become minutes when 
the user has 100 - 150 root intersections to count. Lastly, there is an inspiring 
abundance of research into the computational automation of human-scoring, yet an 
absence of simple, customizable digital tools tailored to the widely used 
human-scoring workflow. To address these shortcomings, the `Radical Root 
Colonization Counter` was developed, a lightweight, browser-based web application 
designed to facilitate rapid and specialized scoring techniques enabling the 
generation of data ready for statistical analyses without transcription. The tool 
also emphasizes minimal technical interaction, real-time audio and visual feedback, 
and instant generation of structured datasets. The counter is hosted on the github 
page: sedonams.github.io/Root-Colonization-Counter/. 

`Gala` was designed to be used by both astronomical researchers and by
students in courses on gravitational dynamics or astronomy. It has already been
used in a number of scientific publications [@Pearson:2017] and has also been
used in graduate courses on Galactic dynamics to, e.g., provide interactive
visualizations of textbook material [@Binney:2008]. The combination of speed,
design, and support for Astropy functionality in `Gala` will enable exciting
scientific explorations of forthcoming data releases from the *Gaia* mission
[@gaia] by students and experts alike.

# State of the field                                                                                                                  

Several tools exist for galactic dynamics computations:                                                     
`galpy` [@Bovy:2015] is a Python package with similar goals,
providing orbit integration and potential classes for galactic dynamics.                                                              
`NEMO` [@Teuben:1995] is a well-established, comprehensive stellar dynamics                                                           
toolbox written primarily in C, offering extensive functionality but with a                                                           
steeper learning curve and less integration with modern Python workflows.                                                             
Other tools like `GalPot` provide specific Milky Way potential models but lack                                                        
the broader dynamical analysis capabilities.                                                                                          
                                                                                                                                        
`Gala` was built rather than contributing to existing projects for several                                                            
reasons. First, `Gala` was designed from the ground up to integrate seamlessly                                                        
with the Astropy ecosystem, using `astropy.units` and `astropy.coordinates`                                                           
as core dependencies rather than optional features. This tight integration                                                            
enables natural workflows for astronomers already using Astropy. Second,                                                              
`Gala`'s object-oriented API with consistent interfaces across subpackages                                                            
(potentials, integrators, dynamics) provides a more modular and extensible                                                            
design than alternatives available at the time. Third, `Gala` fills a specific                                                        
niche between simple demonstration codes and full N-body simulation packages                                                          
like `Gadget` [@Springel:2005] – it focuses on the common tasks in galactic                                                             
dynamics research (orbit integration, potential evaluation, coordinate                                                                
transformations) while maintaining both performance through C implementations                                                         
and usability through its Python interface.  

# Software design

`Gala`'s design philosophy is based on three core principles: (1) to provide a
user-friendly, modular, object-oriented API, (2) to use community tools and
standards (e.g., Astropy for coordinates and units handling), and (3) to use
low-level code (C/C++/Cython) for performance while keeping the user interface
in Python. Within each of the main subpackages in `gala` (`gala.potential`,
`gala.dynamics`, `gala.integrate`, etc.), we try to maintain a consistent API
for classes and functions. For example, all potential classes share a common
base class and implement methods for computing the potential, forces, density,
and other derived quantities at given positions. This also works for
compositions of potentials (i.e., multi-component potential models), which
share the potential base class but also act as a dictionary-like container for
different potential components. As another example, all integrators implement a
common interface for numerically integrating orbits. The integrators and core
potential functions are all implemented in C without support for units, but the
Python layer handles unit conversions and prepares data to dispatch to the C
layer appropriately.Within the coordinates subpackage, we extend Astropy's
coordinate classes to add more specialized coordinate frames and
transformations that are relevant for Galactic dynamics and Milky Way research.

# Research impact statement

`Gala` has demonstrated significant research impact and grown both its user base
and contributor community since its initial release. The package has evolved
through contributions from over 18 developers beyond the original core developer
(@adrn), with community members adding new features, reporting bugs, and
suggesting new features.

While `Gala` started as a tool primarily to support the core developer's
research, it has expanded organically to support a range of applications across
domains in astrophysics related to Milky Way and galactic dynamics. The package
has been used in over 400 publications (according to Google Scholar) spanning
topics in galactic dynamics such as modeling stellar streams [@Pearson:2017],
Milky Way mass modeling, and interpreting kinematic and stellar population
trends in the Galaxy. `Gala` is integrated within the Astropy ecosystem as an
affiliated package and has built functionality that extends the widely-used
`astropy.units` and `astropy.coordinates` subpackages. `Gala`'s impact extends
beyond citations in research: Because of its focus on usability and user
interface design, `Gala` has also been incorporated into graduate-level galactic
dynamics curricula at multiple institutions.

`Gala` has been downloaded over 100,000 times from PyPI and conda-forge yearly
(or ~2,000 downloads per week) over the past few years, demonstrating a broad
and active user community. Users span career stages from graduate students to
faculty and other established researchers and represent institutions around the
world. This broad adoption and active participation validate `Gala`'s role as
core community infrastructure for galactic dynamics research.

# Mathematics

Single dollars ($) are required for inline mathematics e.g. $f(x) = e^{\pi/x}$

Double dollars make self-standing equations:

$$\Theta(x) = \left\{\begin{array}{l}
0\textrm{ if } x < 0\cr
1\textrm{ else}
\end{array}\right.$$

You can also use plain \LaTeX for equations
\begin{equation}\label{eq:fourier}
\hat f(\omega) = \int_{-\infty}^{\infty} f(x) e^{i\omega x} dx
\end{equation}
and refer to \autoref{eq:fourier} from text.

# Citations

Citations to entries in paper.bib should be in
[rMarkdown](http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html)
format.

If you want to cite a software repository URL (e.g. something on GitHub without a preferred
citation) then you can do it with the example BibTeX entry below for @fidgit.

For a quick reference, the following citation commands can be used:
- `@author:2001`  ->  "Author et al. (2001)"
- `[@author:2001]` -> "(Author et al., 2001)"
- `[@author1:2001; @author2:2001]` -> "(Author1 et al., 2001; Author2 et al., 2002)"

# Figures

Figures can be included like this:
![Caption for example figure.\label{fig:example}](figure.png)
and referenced from text using \autoref{fig:example}.

Figure sizes can be customized by adding an optional second parameter:
![Caption for example figure.](figure.png){ width=20% }

# AI usage disclosure

No generative AI tools were used in the development of this software, the writing
of this manuscript, or the preparation of supporting materials.

# Acknowledgements

We acknowledge contributions from Brigitta Sipocz, Syrtis Major, and Semyeong
Oh, and support from Kathryn Johnston during the genesis of this project.

# References
