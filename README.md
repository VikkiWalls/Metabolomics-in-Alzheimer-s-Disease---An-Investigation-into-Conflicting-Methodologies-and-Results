# Metabolomics-in-Alzheimers
Metabolomics Data Science MSc project looking at data of Alzheimer's patients
***
## Table of Contents
1. [General Info](#general-info)
2. [Technologies](#technologies)
3. [Methods](#methods)
4. [References](#references)
***
## General Info
Metabolomics is a field of research which is new and fast growing. It looks at biological compounds extracted from minimally invasive tissue and fluid samples such as blood plasma, urine and cerebral spinal fluid (CSF). These compounds can be used to determine a person’s health status as well as what they are at risk of.

The field is very data heavy and its newness makes it the perfect environment for innovation. It’s an ideal space for data science projects with a focus on social and/or public good.

This project takes an existing dataset produced by the Mayo Clinic in 2013 and uses various statistical and machine learning methods to extract metabolites significant to Alzheimer’s disease (AD).

The significant metabolites were then compared against metabolites found significant by other literature to determine the reliability of metabolomics testing for this disease.
***
## Technologies
A list of technologies used within the project:
* [Jupyter Notebooks](https://www.anaconda.com/): Version 6.3.0
* [Python](https://www.python.org/downloads/release/python-388/): Version 3.8.8
* [pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/install.html): Version 1.2.4
* [matplotlib](https://matplotlib.org/stable/users/installing/index.html): Version 3.3.4
* [missingno](https://github.com/ResidentMario/missingno): Version 0.4.2
* [scikit learn](https://scikit-learn.org/stable/install.html): Version 0
* [plotly](https://plotly.com/python/getting-started/): Version 5.9
* [seaborn](https://seaborn.pydata.org/installing.html): Version 0.11.1
* [statsmodels](https://www.statsmodels.org/dev/install.html): Version 0.12.2
* [NetworkX](https://networkx.org/documentation/stable/install.html): Version 2.5
* [IPy](http://ipython.org/): Version 7.6.3
* [Yellowbrick](https://www.scikit-yb.org/en/latest/quickstart.html): Version 1.4
***
## Methods
### Statistical Mehtods Used
* [No Skip k Nearest Neighbour (NS-kNN)](https://github.com/gtStyLab/NSkNN/blob/master/functions/NSkNNData_HM.m)
* Principle Component Analysis (PCA)
* Partial Least Squares - Discriminant Analysis (PLS-DA)
***
## References
### Methods
Boccard, J. and Rutledge, D.N. (2013). [A consensus orthogonal partial least squares discriminant analysis (OPLS-DA) strategy for multiblock Omics data fusion](https://www.sciencedirect.com/science/article/pii/S0003267013001700?via%3Dihub). Analytica Chimica Acta, [online] 769, pp.30–39. doi:10.1016/j.aca.2013.01.022.

Brereton, R.G. and Lloyd, G.R. (2014). [Partial least squares discriminant analysis: taking the magic away](https://analyticalsciencejournals.onlinelibrary.wiley.com/doi/10.1002/cem.2609). Journal of Chemometrics, [online] 28(4), pp.213–225. doi:10.1002/cem.2609.

Lee and Styczynski, M.P. (2018). [NS-kNN: a modified k-nearest neighbors approach for imputing metabolomics data](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6532628/). Metabolomics, [online] 14(12), p.153. doi:10.1007/s11306-018-1451-8.
### Literature
Cao, B., Wang, D., Pan, Z., Brietzke, E., McIntyre, R.S., Musial, N., Mansur, R.B., Subramanieapillai, M., Zeng, J., Huang, N. and Wang, J. (2019). [Characterizing acyl-carnitine biosignatures for schizophrenia: a longitudinal pre- and post-treatment study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6336814/). Translational Psychiatry, 9(1). doi:10.1038/s41398-018-0353-x.

Clish, C.B. (2015).[ Metabolomics: an emerging but powerful tool for precision medicine](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4850886/). Cold Spring Harbor Molecular Case Studies, [online] 1(1). doi:10.1101/mcs.a000588.

Cummings, J. (2017). [Lessons Learned from Alzheimer Disease: Clinical Trials with Negative Outcomes](https://ascpt.onlinelibrary.wiley.com/doi/full/10.1111/cts.12491). Clinical and Translational Science, [online] 11(2), pp.147–152. doi:10.1111/cts.12491.

