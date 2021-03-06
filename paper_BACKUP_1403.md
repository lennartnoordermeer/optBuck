---
title: optBuck – An R package for handling single-grip forest harvester data and bucking optimization
tags:
- R
- Forestry
- Harvester data
- Optimal bucking
authors: 
- name: Lennart Noordermeer 
- name: Terje Gobakken
affiliations: 
- name: Faculty of Environmental Sciences and Natural Resource Management, Norwegian University of Life Sciences
<<<<<<< HEAD:paper.Rmd

=======
  
>>>>>>> 48aa701b29631b617203e8664ec866a7fc9cebf4:paper.md
date: 12 May 2022
bibliography: References.bib

aas-doi: 10.3847/xxxxx
aas-journal: Journal of Open Source Software
---

# Summary

The R package optBuck provides a set of functions for reading and handling production files from forest harvesters and computing the optimum bucking outcome for harvested trees. The package is based on harvested production report (hpr) files in the StanFord 2010 data format [@arlinger2012stanford], retrieved from single-grip harvesters. Functionality includes the extraction of production data on harvested stems, produced logs, and the bucking outcome for each harvested stem. Additionally, information on assortments, such as the species, dimension and quality requirements, and price matrices can be extracted from the hpr files. These data can then be used as input parameters in a bucking algorithm, which maximizes the total stem value using dynamic programming [@bellman1954theory; @faaland1984log]. Thus, apart from providing tools to extract and process data from single-grip harvesters, optBuck provides a means to evaluate bucking outcomes and perform sensitivity analyses and economic simulations based on harvester data.

# Statement of need

Single-grip harvesters record large amounts of standardized production data during operation. Sensors mounted on the harvester head record log dimensions and volumes, and each cut is allocated a time stamp and stored on an on-board computer. The operator selects and records tree species and timber grades, providing information on the characteristics and quality of the harvested logs. Additionally, most operating systems can be coupled with Global Navigation Satellite Systems [@olivera2016exploring], providing spatial data on the machine’s operation path and harvested trees. Harvester data are a key source of information in the fields of harvester productivity assessment, forest inventory, operation management and bucking optimization [@kemmerer2021using].   

Bucking, i.e., cutting felled trees into logs, is a primary task in timber harvesting and has great impact on the value of the produced timber (e.g. Bowers, 1998, Olsen et al., 1991). A given stem can be bucked into different numbers of logs with different dimensions, assortments, and values. Many such potential outcomes typically exist, whereby suboptimal bucking typically results in reduced timber quality and volume utilization and can reduce the economic value of the stem substantially. Besides being used in on-board computers in harvesters to aid machine operators in bucking harvested stems, bucking algorithms have found widespread application in research. For example, studies have used bucking algorithms for timber market assessments [@nybakk2007bucking; @puumalainen1998optimal] and economic simulations [@gobakken2000effect; @malinen2007comparing].   

Although machine manufacturers provide software solutions for handling production data obtained from harvesters, few other software tools, and no R packages, currently provide the functionality to read and process hpr files. In addition, no R package currently provides a bucking algorithm which can be used for bucking optimization. Apart from reading and managing information obtained from hpr files, optBuck can thus be used to evaluate the bucking efficiency (Figure 1) as well as for research purposes.

<<<<<<< HEAD:paper.Rmd
# Example features

Below we demonstrate some features of the package using example data. We refer to the package pdf manual for the complete range of features.
```{r, echo=T, message=F, results='hide'}
#installation
devtools::install_github("https://github.com/lennartnoordermeer/optBuck",force=T)
library(XML);library(optBuck)
```
Path to the external example data: 
```{r, echo=T, message=F, results='hide'}
hprfile=system.file("extdata",
                    "example.hpr",
                    package = "optBuck")
```
Extract production data:
```{r, echo=T, message=F, results='hide'}
PriceMatrices=getPriceMatrices(hprfile)
ProductData=getProductData(hprfile)
Logs=getLogs(hprfile)
StemProfile=getStemprofile(hprfile,Logs)
PermittedGrades=getPermittedGrades(hprfile)
SpeciesGroupDefinition=getSpeciesGroupDefinition(hprfile)
LengthClasses=getLengthClasses(hprfile)
```
Extract the bucking outcomes:
```{r, echo=T, message=F, results='hide'}
Bucking=getBucking(hprfile, PriceMatrices, ProductData, StemProfile, LengthClasses)
```
Compute the optimal bucking outcomes:
```{r, echo=T, message=F}
OptimalBucking=optBuck_hpr(hprfile,
                           PriceMatrices,
                           ProductData,
                           StemProfile,
                           PermittedGrades,
                           SpeciesGroupDefinition)
head(OptimalBucking)[,c(1:4,7,9)]
```
Bucking outcomes can be plotted and compared for given stems:
```{r, echo=T, message=F, results='hide'}
Stem=337463
Actual=plotBucking(Bucking, StemProfile,
                   Stem, ProductData)
Optimal=plotBucking(OptimalBucking, StemProfile,
                    Stem, ProductData)
library(ggpubr)
ggarrange(Actual,Optimal,nrow=2,align="v",
                         common.legend = T,legend="bottom",
                         labels = c("Actual","Optimal"))
```
=======
![Figure 1. Evaluating the bucking outcome from a harvester production file.](Figure.png){ width=75% }
>>>>>>> 48aa701b29631b617203e8664ec866a7fc9cebf4:paper.md

# Funding details

The optBuck package was developed as part of the project SmartForest, funded by Research council of Norway (project no. 309671). 


# References
