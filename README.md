# Metabolomics in Alzheimer's Disease
Metabolomics Data Science MSc project looking at significant metabolites found in Alzheimer's Disease (AD) patients in comparison to patients with mild cognitive impairment (MCI) and cognitive normal (CN) controls.
***
## Table of Contents
1. [General Info](#general-info)
    * [Aims](#aims)
    * [Challenges](#challenges)
2. [Technologies](#technologies)
3. [Methods](#methods)
    * [Statistical and ML](#statistical-and-machine-learning-methods)
    * [Visualisation](#visualisation-techniques)
5. [Results](#results)
6. [List of Documents](#list-of-documents)
7. [References](#references)
    * [Methodological](#methodological-sources)
    * [Literature](#literature)
***
## General Info
Metabolomics is a field of research which is new and fast growing. It looks at biological compounds extracted from minimally invasive tissue and fluid samples such as blood plasma, urine and cerebral spinal fluid (CSF). These compounds can be used to determine a person’s health status as well as what they are at risk of.

The field is very data heavy and its newness makes it the perfect environment for innovation. It’s an ideal space for data science projects with a focus on social/public good.

This project takes an [existing dataset](https://www.metabolomicsworkbench.org/data/DRCCMetadata.php?Mode=Study&StudyID=ST000046) consisting of 1909 metabolites and three groups (CN, MCI and AD) of 15 individuals, produced by the Mayo Clinic in [2013](https://pubmed.ncbi.nlm.nih.gov/23700429/) and uses various statistical and machine learning methods to extract metabolites significant to Alzheimer’s disease (AD).

In existing literature there is little in the way of overlap in results from study to study, and thus whilst AD has been covered a number of times in the short life of the field of Metabolomics, there is no defined list of metabolites which are significant to this disease and backed up over multiple studies. 
In this paper, the significant metabolites were compared against metabolites found significant by other literature with the hope of providing some clarity to the noise.

### Aims
This study aims to find metabolites with a statistically significant influence on individuals with AD from the existing dataset and to compare these results with the metabolites named as significant in other studies. This is done in the hope to either provide clarity by aligning with existing results or to illustrate that a lack of agreed "good practice" techniques within the metabolomics field results in inconsistent and irreproducible results.

### Challenges
One of the biggest challenges was related to the specific dimensions of the dataset, with far more metabolites than observations (individual samples). This caused interference in initial attempts at statistical analysis and is the suspected cause for the unusual results in the VIF test. A related issue was the minimal numbers of sample sizes. With only 15 individual samples per cognitive type there is a reasonable possibility that any metabolites found to be significant may not occur in other datasets - this seems to be a common issue with the metabolomics field in general, and there certainly seems to be a lack of consensus in significant metabolites for AD throughout the existing literature.

Other common issues in this field relate to a lack of consensus around best practices in data analysis methods. This is addressed by [Lee and Styczynski (2018)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6532628/) and was the given motivation behind the development of the No Skip k Nearest Neighbour (NS-kNN) method of imputation. This in itself brought its own challenge as the code produced by Lee and Styczynski was in the Matlab Language and needed to be translated into Python before use.
***
## Technologies
A list of technologies used within the project:
* [IPy](http://ipython.org/): Version 7.6.3
* [Jupyter Notebooks](https://www.anaconda.com/): Version 6.3.0
* [matplotlib](https://matplotlib.org/stable/users/installing/index.html): Version 3.3.4
* [missingno](https://github.com/ResidentMario/missingno): Version 0.4.2
* [NetworkX](https://networkx.org/documentation/stable/install.html): Version 2.5
* [pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/install.html): Version 1.2.4
* [plotly](https://plotly.com/python/getting-started/): Version 5.9
* [Python](https://www.python.org/downloads/release/python-388/): Version 3.8.8
* [scikit learn](https://scikit-learn.org/stable/install.html): Version 0
* [seaborn](https://seaborn.pydata.org/installing.html): Version 0.11.1
* [statsmodels](https://www.statsmodels.org/dev/install.html): Version 0.12.2
* [Yellowbrick](https://www.scikit-yb.org/en/latest/quickstart.html): Version 1.4

[Matlab](https://uk.mathworks.com/products/get-matlab.html) was not directly used within the project however the language must be mentioned as Lee and Styczynski used it to write the original NS-kNN code.
***
## Methods
### Statistical and Machine Learning Methods
* #### [No Skip k Nearest Neighbour (NS-kNN)](https://github.com/gtStyLab/NSkNN/blob/master/functions/NSkNNData_HM.m)
  * Used for imputation in dealing with missing values
  * Specifically designed to improve accuracy for values in data missing not at random (MNAR)
  * Particularly useful for metabolite data where missing values can be due to Limit of Detection (LOD) levels in mass spectrometry
* #### Variance Inflation Factor (VIF) Testing
  * Used in conjunction with additional visualisation techniques mentioned below to test for multicollinearity
* #### Principal Component Analysis (PCA)
  * Unsupervised Machine Learning Method
  * Finds the optimum number of components to explain the maximum variance in the data
  * Useful for high dimensions of features (e.g., 1909 metabolites)
  * Useful for simplifying complex data when there are high levels of multicollinearity
  
    *A new dataframe was created using the principle components to explain 95% of the variance, and this dataframe was used in the remaining tests and stored as a csv file.*
* #### Partial Least Squares - Discriminant Analysis (PLS-DA)
  * Supervised Machine Learning Method
  * Used to determine whether known groups are actually different
  * Used to determine which features best describe the differences between the known groups
  ##### Drawbacks
    * Can be detrimental to use on its own. See [Brereton and Lloyd (2014)](https://analyticalsciencejournals.onlinelibrary.wiley.com/doi/epdf/10.1002/cem.2609?saml_referrer)
* #### Logistic Regression
  * Supervised Machine Learning method (borrowed from statistics)
  * One of the most common methods of analysis in metabolomics
  * Useful for prediction and classifiaction
  * Builds a regression model to predict the probability that a given data entry belongs to the category numbered as “1”
  
  Cross Validation was then used to assess accuracy and performance of the model.
  
### Visualisation Techniques
  * #### Multicollinearity
    * ##### Cluster Map (using Seaborn)
      * Can be difficult to interpret with large datasets such as metabolomics data
    * ##### Interactive Network Graph (using NetworkX)
      * Adjustable correlation threshold (recommended to be set at 0.95) allows direct comparisons between different levels
      * Panning, zoom and selection tools make interpretation and manipulation accessible
      * Visualisation of direct relationships between correlated metabolites
      ###### Drawbacks
      * Threshold slider must be moved once after restarting kernel to produce a display
      * Can still be difficult to interpret if high levels of multicollinearity exist and plot is zoomed out (making it difficult to use in academic write ups)
      * Large metabolite names can create visual noise
  * #### PCA
    * ##### Scatter Graph (using Yellowbrick) - colour coded by cognitive status
    * ##### Elbow Visualiser (using matplotlib) - explained variance against principal components
  * #### PLS-DA
    * Visual comparison between AD and CN, MCI and CN and, AD and MCI
    * Initial line plot using principal components to compare potential for outliers
    * Scatter plot based on PLS regression scores to check for seperation between the profiles of each of the three groups

***
## Results
### Multicollinearity
* #### Visualisation
  * Clustermap displayed a clear clusters of highly positively correlated metabolites
      * individual metabolites could not be identified due to large size of dataset
  * Interactive network graph was able to visualise direct relationships between correlated metabolites
     * e.g. the direct relationship between C5H6N4O4S and AsnProLys
* #### VIF Test
  * Displayed infinity values for every metabolite, regardless of the specific programming method used
      * Normal techniques to reduce/remove this error (including log transforming the data, and removing the highest correlated values) did not change these results
  * Did not appear to match up with the correlation values produced by the correlation matrix used by the visualisation methods above

Whilst the VIF test appears to be inconclusive, between the VIF results and the visualisation techniques, it was clear that there were some levels of multicollinearity in this dataset. In order to undertake analysis methods such as logistic regression, this needed to be removed.

### PCA
   * #### Visualisation
      * Production of a scatter graph colour coded by cognitive status revealed that data contained no specific clusters
      * Elbow plot did not show a clear change to indicate a specifically optimal number of principle components
   * Explained Variance Ratio indicated that the first 40 (out of a potential 45) components would explain 95% of the variance in the data
      * The first 29 components would explain 80% of the variance

### PLS-DA
   * #### Alzheimer's Disease against Cognitive Normal
      * Initial visual comparison of components by cognitive type suggested a lack of obvious outliers although there were a couple of clear differences in spike height (but these did not go out with the range of the rest of the data)
      * On plotting the PLS Regression scores there is visible separation between AD and CN values on Latent Variable 1
   * #### Mild Cognitive Impairment against Cognitive Normal
      * Initial visual comparison of components by cognitive type indicated some potential outliers in the CN data
      * On plotting the PLS Regression scores there is visible separation between MCI and CN values on Latent Variable 1
   * #### Alzheimer's Disease against Mild Cognitive Impairment
      * Initial visual comparison of components by cognitive type indicated some potential outliers in the AD data
      * On plotting the PLS Regression scores there is clear and significant visible separation between AD and MCI values on Latent Variable 1
### Logistic Regression
***
## List of Documents
* Document 1 - README.md (this file)
* Document 2 - Full project code
* Document 3 - Additional tables
* Document 4 - Data
* Document 5 - Write Up
***
## References
### Methodological Sources
Boccard, J. and Rutledge, D.N. (2013). [A consensus orthogonal partial least squares discriminant analysis (OPLS-DA) strategy for multiblock Omics data fusion](https://www.sciencedirect.com/science/article/pii/S0003267013001700?via%3Dihub). Analytica Chimica Acta, [online] 769, pp.30–39. doi:10.1016/j.aca.2013.01.022.

Brereton, R.G. and Lloyd, G.R. (2014). [Partial least squares discriminant analysis: taking the magic away](https://analyticalsciencejournals.onlinelibrary.wiley.com/doi/10.1002/cem.2609). Journal of Chemometrics, [online] 28(4), pp.213–225. doi:10.1002/cem.2609.

Lee and Styczynski, M.P. (2018). [NS-kNN: a modified k-nearest neighbors approach for imputing metabolomics data](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6532628/). Metabolomics, [online] 14(12), p.153. doi:10.1007/s11306-018-1451-8.

Lee, M. and Hu, T. (2019). [Computational Methods for the Discovery of Metabolic Markers of Complex Traits. Metabolites](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6523328/), 9(4), p.66. doi:10.3390/metabo9040066.

Ruiz-Perez, D., Guan, H., Madhivanan, P., Mathee, K. and Narasimhan, G. (2020). [So you think you can PLS-DA?](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-019-3310-7#:~:text=PLS-DA%20can%20be%20thought%20of%20as%20a%20%E2%80%9Csupervised%E2%80%9D,as%20for%20classification%20%5B%209%20%E2%80%93%2011%20%5D.) BMC Bioinformatics, [online] 21(S1). doi:10.1186/s12859-019-3310-7.

Szymańska, E., Saccenti, E., Smilde, A.K. and Westerhuis, J.A. (2011). [Double-check: validation of diagnostic statistics for PLS-DA models in metabolomics studies.](https://link.springer.com/article/10.1007/s11306-011-0330-3) Metabolomics, [online] 8(S1), pp.3–16. doi:10.1007/s11306-011-0330-3.
### Literature
Cao, B., Wang, D., Pan, Z., Brietzke, E., McIntyre, R.S., Musial, N., Mansur, R.B., Subramanieapillai, M., Zeng, J., Huang, N. and Wang, J. (2019). [Characterizing acyl-carnitine biosignatures for schizophrenia: a longitudinal pre- and post-treatment study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6336814/). Translational Psychiatry, 9(1). doi:10.1038/s41398-018-0353-x.

Clish, C.B. (2015).[ Metabolomics: an emerging but powerful tool for precision medicine](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4850886/). Cold Spring Harbor Molecular Case Studies, [online] 1(1). doi:10.1101/mcs.a000588.

Cummings, J. (2017). [Lessons Learned from Alzheimer Disease: Clinical Trials with Negative Outcomes](https://ascpt.onlinelibrary.wiley.com/doi/full/10.1111/cts.12491). Clinical and Translational Science, [online] 11(2), pp.147–152. doi:10.1111/cts.12491.

Douaud, G., Groves, A.R., Tamnes, C.K., Westlye, L.T., Duff, E.P., Engvig, A., Walhovd, K.B., James, A., Gass, A., Monsch, A.U., Matthews, P.M., Fjell, A.M., Smith, S.M. and Johansen-Berg, H. (2014). [A common brain network links development, aging, and vulnerability to disease](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4267352/). Proceedings of the National Academy of Sciences, 111(49), pp.17648–17653. doi:10.1073/pnas.1410378111.

He, Y., Yu, Z., Giegling, I., Xie, L., Hartmann, A.M., Prehn, C., Adamski, J., Kahn, R., Li, Y., Illig, T., Wang-Sattler, R. and Rujescu, D. (2012). [Schizophrenia shows a unique metabolomics signature in plasma](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3432190/pdf/tp201276a.pdf). Translational Psychiatry, [online] 2(8), pp.e149–e149. doi:10.1038/tp.2012.76.

Human Metabolome Database. (2021). Human Metabolome Database: Showing metabocard for [Hypoxanthine (HMDB0000157)](https://hmdb.ca/metabolites/HMDB0000157). [online],[Accessed 28 Jun. 2022].

Huo, Z., Yu, L., Yang, J., Zhu, Y., Bennett, D.A. and Zhao, J. (2020). [Brain and blood metabolome for Alzheimer’s dementia: findings from a targeted metabolomics analysis](https://pubmed.ncbi.nlm.nih.gov/31785839/). Neurobiology of Aging, [online] 86, pp.123–133. doi:10.1016/j.neurobiolaging.2019.10.014.

Illig, T., Gieger, C., Zhai, G., Römisch-Margl, W., Wang-Sattler, R., Prehn, C., Altmaier, E., Kastenmüller, G., Kato, B.S., Mewes, H.-W., Meitinger, T., de Angelis, M.H., Kronenberg, F., Soranzo, N., Wichmann, H.-E., Spector, T.D., Adamski, J. and Suhre, K. (2010). [A genome-wide perspective of genetic variation in human metabolism](https://www.nature.com/articles/ng.507). Nature Genetics, [online] 42(2), pp.137–141. doi:10.1038/ng.507 163 metabolites in plasma.

Kaddurah-Daouk, R. (2006). [Metabolic Profiling of Patients with Schizophrenia](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1551921/). PLoS Medicine, [online] 3(8), p.e363. doi:10.1371/journal.pmed.0030363.

Manchester, M. and Anand, A. (2017). Chapter Two - [Metabolomics: Strategies to Define the Role of Metabolism in Virus Infection and Pathogenesis](https://www.sciencedirect.com/science/article/abs/pii/S0065352717300015). Advances in Virus Research, [online] 98, pp.57–81.

Mittelstrass, K., Ried, J.S., Yu, Z., Krumsiek, J., Gieger, C., Prehn, C., Roemisch-Margl, W., Polonikov, A., Peters, A., Theis, F.J., Meitinger, T., Kronenberg, F., Weidinger, S., Wichmann, H.E., Suhre, K., Wang-Sattler, R., Adamski, J. and Illig, T. (2011). Discovery of Sexual Dimorphisms in Metabolic and Genetic Biomarkers. PLoS Genetics, [online] 7(8), p.e1002215. doi:10.1371/journal.pgen.1002215 [Metabolite inclusion criteria for ‘Schizophrenia shows a unique metabolomics signature in plasma’](https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1002215#s4).

Petersen, R.C. (2004). [Mild cognitive impairment as a diagnostic entity](https://onlinelibrary.wiley.com/doi/full/10.1111/j.1365-2796.2004.01388.x?sid=nlm%3Apubmed). Journal of Internal Medicine, [online] 256(3), pp.183–94. doi:10.1111/j.1365-2796.2004.01388.x.

Proitsi, P., Kim, M., Whiley, L., Simmons, A., Sattlecker, M., Velayudhan, L., Lupton, M.K., Soininen, H., Kloszewska, I., Mecocci, P., Tsolaki, M., Vellas, B., Lovestone, S., Powell, J.F., Dobson, R.J.B. and Legido-Quigley, C. (2016). [Association of blood lipids with Alzheimer’s disease: A comprehensive lipidomics analysis](https://alz-journals.onlinelibrary.wiley.com/doi/10.1016/j.jalz.2016.08.003). Alzheimer’s & Dementia, [online] 13(2), pp.140–151. doi:http://dx.doi.org/10.1016/j.jalz.2016.08.003.

Ribe, A.R., Laursen, T.M., Charles, M., Katon, W., Fenger-Grøn, M., Davydow, D.S., Chwastiak, L., Cerimele, J.M. and Vestergaard, M. (2015). [Long-term Risk of Dementia in Persons With Schizophrenia: A Danish Population-Based Cohort Study](https://www.researchgate.net/publication/282659507_Long-term_Risk_of_Dementia_in_Persons_With_Schizophrenia_A_Danish_Population-Based_Cohort_Study). JAMA Psychiatry, [online] 72(11), pp.1–7. doi:10.1001/jamapsychiatry.2015.1546.

Rubin, E. (2016). [The Relationship Between Schizophrenia and Dementia](https://www.psychologytoday.com/us/blog/demystifying-psychiatry/201603/the-relationship-between-schizophrenia-and-dementia#:~:text=Many%20had%20clinical%20features%20seen%20in%20persons%20with) | Psychology Today. [online] www.psychologytoday.com.  [Accessed 24 May 2022].

Schneider, L.S. and Sano, M. (2009). [Current Alzheimer’s disease clinical trials: Methods and placebo outcomes](https://www.sciencedirect.com/science/article/abs/pii/S1552526009021281). Alzheimer’s & Dementia, 5(5), pp.388–397. doi:10.1016/j.jalz.2009.07.038.

Trushina, E., Dutta, T., Persson, X.-M.T., Mielke, M.M. and Petersen, R.C. (2013). [Identification of Altered Metabolic Pathways in Plasma and CSF in Mild Cognitive Impairment and Alzheimer’s Disease Using Metabolomics](https://pubmed.ncbi.nlm.nih.gov/23700429/). PLoS ONE, [online] 8(5), p.e63644. doi:10.1371/journal.pone.0063644.

Wang, G., Zhou, Y., Huang, F.-J., Tang, H.-D., Xu, X.-H., Liu, J.-J., Wang, Y., Deng, Y.-L., Ren, R.-J., Xu, W., Ma, J.-F., Zhang, Y.-N., Zhao, A.-H., Chen, S.-D. and Jia, W. (2014). [Plasma Metabolite Profiles of Alzheimer’s Disease and Mild Cognitive Impairment](https://pubmed.ncbi.nlm.nih.gov/24694177/). Journal of Proteome Research, [online] 13(5), pp.2649–2658. doi:10.1021/pr5000895.

White, K.E. and Cummings, J.L. (1996). [Schizophrenia and Alzheimer’s disease: Clinical and pathophysiologic analogies](https://www.sciencedirect.com/science/article/abs/pii/S0010440X96900358?via%3Dihub). Comprehensive Psychiatry, 37(3), pp.188–195. doi:10.1016/s0010-440x(96)90035-8.

Yu, Z., Kastenmüller, G., He, Y., Belcredi, P., Möller, G., Prehn, C., Mendes, J., Wahl, S., Roemisch-Margl, W., Ceglarek, U., Polonikov, A., Dahmen, N., Prokisch, H., Xie, L., Li, Y., Wichmann, H.-E., Peters, A., Kronenberg, F., Suhre, K. and Adamski, J. (2011). [Differences between Human Plasma and Serum Metabolite Profiles](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0021230). PLoS ONE, [online] 6(7), p.e21230. doi:10.1371/journal.pone.0021230 163 Metabolites in Plasma (NB: Some authors the same as Schizophrenia Data source. Potentially questionable credibility given authors referenced themselves).
