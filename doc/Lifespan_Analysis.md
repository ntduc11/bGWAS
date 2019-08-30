
# Lifespan Analysis

In this example, we will use the data from Timmers et al to apply our
Bayesian GWAS approach to study lifespan.  
Here, we assume that the `bGWAS` package is already installed, that the
Z-matrix files have already been downloaded and stored in
“\~/ZMatrices”. If that is not the case, please follow the steps
described [here](../README.md).

``` r
library(bGWAS)

# Download data to working directory (~460 MB) if not already here
print(getwd())
if(!file.exists("lifegen_phase2_bothpl_alldr_2017_09_18.tsv.gz")) download.file(url = "https://datashare.is.ed.ac.uk/bitstream/handle/10283/3209/lifegen_phase2_bothpl_alldr_2017_09_18.tsv.gz?sequence=1&isAllowed=y", destfile = "lifegen_phase2_bothpl_alldr_2017_09_18.tsv.gz")

Lifespan_Timmers2019 = "lifegen_phase2_bothpl_alldr_2017_09_18.tsv.gz"
```

Now that we have the data in our working directory, we can launch the
analysis (with default parameters):

``` r
print(getwd())
```

    ## [1] "/Users/nmounier/Documents/SGG/Projects/Packaging/bGWAS/doc"

``` r
Lifespan_bGWAS = bGWAS(name = "Lifespan_Timmers2019",
                       GWAS = Lifespan_Timmers2019)
```

    ## <<< Preparation of analysis >>> 
    ## > Checking parameters 
    ## The name of your analysis is: "Lifespan_Timmers2019". 
    ## The Z-Matrix files are stored in "/Users/nmounier/ZMatrices".  
    ## # Preparation of the data... 
    ## The conventional GWAS used as input is: "lifegen_phase2_bothpl_alldr_2017_09_18.tsv.gz".  
    ##    SNPID column, ok - ALT column, ok - REF column, ok - BETA column, ok - SE column, ok
    ## Posterior effects will be rescaled using BETA and SE.The analysis will be run in the folder: "/Users/nmounier/Documents/SGG/Projects/Packaging/bGWAS/doc".  
    ## The p-value threshold used for selecting MR instruments is: 1e-06.  
    ## The minimum number instruments required for each trait is: 3.  
    ## The distance used for pruning MR instruments is: 500Kb.  
    ## Distance-based pruning will be used for MR instruments.  
    ## No shrinkage applied before performing MR.The p-value threshold used for stepwise selection will be derived according to the number of Prior GWASs used.  
    ## No shrinkage applied before performing calculating the prior.Significant SNPs will be identified according to p-value. The threshold used is :5e-08.  
    ## The distance used for pruning results is: 500Kb.  
    ## Distance-based pruning will be used for results.  
    ## <><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><> 
    ## <<< Identification of significant prior GWASs for MR >>>  
    ## > Creating the Z-Matrix of strong instruments 
    ## # Loading the ZMatrix... 
    ## Selecting studies :
    ## 38 studies 
    ## 209,840 SNPs 
    ## # Adding data from the conventional GWAS : 
    ##  "lifegen_phase2_bothpl_alldr_2017_09_18.tsv.gz" 
    ## Done! 
    ## 197,681 SNPs in common between prior studies and the conventional GWAS 
    ## # Thresholding... 
    ## 134,807 SNPs left after thresholding 
    ## Neuroticism (GPC) - Smoking - ever smoked (TAG) - Smoking - age of onset (TAG) : removed (less than 3 instrument after thresholding) 
    ## 35 studies left after thresholding 
    ## Pruning MR instruments... 
    ##    distance : 500Kb 
    ## 1,934 SNPs left after pruning 
    ## Anorexia (GCAN) - Openness to Experience (GPC) - Extraversion (GPC) - Insulin (MAGIC) - 2010 - HOMA-IR (MAGIC) - Depression (PGC) - Autism (PGC) - Smoking - cigarettes per day (TAG) - Smoking - former smoker (TAG) : removed (less than 3 strong instrument after pruning) 
    ## 26 studies left after thresholding+pruning 
    ## 1,927 SNPs left after removing studies with only one strong instrument 
    ## > Performing MR  
    ## #Preparation of the MR analyses to identify significant studies... 
    ## Studies tested : Body Mass Index (GIANT) - Schizophrenia (PGC) - 2014 - Coronary Artery Disease (CARDIoGRAM) - Type 2 Diabetes (DIAGRAM) - Years of Schooling (SSGAC) - Glucose (ENGAGE) - Crohns Disease (IBD) - Ulcerative Colitis (IBD) - HDL Cholesterol (GLGC) - LDL Cholesterol (GLGC) - Total Cholesterol (GLGC) - Triglycerides (GLGC) - Glucose (MAGIC) - 2010 - HOMA-B (MAGIC) - Glucose (MAGIC) - Insulin (MAGIC) - Heart Rate (HRgene) - Height (GIANT) - Parkinsons - Neuroblastoma - Multiple Sclerosis - Systolic Blood Pressure (ICBP) - Diastolic Blood Pressure (ICBP) - Schizophrenia (PGC) - 2013 - Schizophrenia (PGC) - College Completion (SSGAC)
    ## Conventionnal GWAS of interest : lifegen_phase2_bothpl_alldr_2017_09_18.tsv.gz
    ## # Univariate regressions for each trait... 
    ##   Number of trait-specific instruments per univariate regression: 
    ##   . Body Mass Index (GIANT) : 89 
    ##   . Schizophrenia (PGC) - 2014 : 6 
    ##   . Coronary Artery Disease (CARDIoGRAM) : 12 
    ##   . Type 2 Diabetes (DIAGRAM) : 12 
    ##   . Years of Schooling (SSGAC) : 80 
    ##   . Glucose (ENGAGE) : 11 
    ##   . Crohns Disease (IBD) : 43 
    ##   . Ulcerative Colitis (IBD) : 75 
    ##   . HDL Cholesterol (GLGC) : 72 
    ##   . LDL Cholesterol (GLGC) : 57 
    ##   . Total Cholesterol (GLGC) : 73 
    ##   . Triglycerides (GLGC) : 51 
    ##   . Glucose (MAGIC) - 2010 : 10 
    ##   . HOMA-B (MAGIC) : 6 
    ##   . Glucose (MAGIC) : 17 
    ##   . Insulin (MAGIC) : 5 
    ##   . Heart Rate (HRgene) : 14 
    ##   . Height (GIANT) : 522 
    ##   . Parkinsons : 382 
    ##   . Neuroblastoma : 353 
    ##   . Multiple Sclerosis : 153 
    ##   . Systolic Blood Pressure (ICBP) : 8 
    ##   . Diastolic Blood Pressure (ICBP) : 9 
    ##   . Schizophrenia (PGC) - 2013 : 19 
    ##   . Schizophrenia (PGC) : 107 
    ##   . College Completion (SSGAC) : 3 
    ## Done! 
    ## # Stepwise selection (all traits)... 
    ## The p-value threshold used for stepwise selection is 0.0019 (26 Prior GWASs tested).  
    ## Adding the first study :Years of Schooling (SSGAC) 
    ##   iteration 1: 1 studies 
    ## #Run model 
    ## #Test if any study can be added with p<0.0019 
    ## Adding one study :LDL Cholesterol (GLGC) 
    ## Done! 
    ## #Update model 
    ## #Test if any study has p>0.0019 now 
    ##   iteration 2: 2 studies 
    ## #Run model 
    ## #Test if any study can be added with p<0.0019 
    ## Adding one study :Body Mass Index (GIANT) 
    ## Done! 
    ## #Update model 
    ## #Test if any study has p>0.0019 now 
    ##   iteration 3: 3 studies 
    ## #Run model 
    ## #Test if any study can be added with p<0.0019 
    ## Adding one study :Coronary Artery Disease (CARDIoGRAM) 
    ## Done! 
    ## #Update model 
    ## #Test if any study has p>0.0019 now 
    ##   iteration 4: 4 studies 
    ## #Run model 
    ## #Test if any study can be added with p<0.0019 
    ## Adding one study :Diastolic Blood Pressure (ICBP) 
    ## Done! 
    ## #Update model 
    ## #Test if any study has p>0.0019 now 
    ##   iteration 5: 5 studies 
    ## #Run model 
    ## #Test if any study can be added with p<0.0019 
    ## Adding one study :Height (GIANT) 
    ## Done! 
    ## #Update model 
    ## #Test if any study has p>0.0019 now 
    ##   iteration 6: 6 studies 
    ## #Run model 
    ## #Test if any study can be added with p<0.0019 
    ## Adding one study :Type 2 Diabetes (DIAGRAM) 
    ## Done! 
    ## #Update model 
    ## #Test if any study has p>0.0019 now 
    ##   iteration 7: 7 studies 
    ## #Run model 
    ## #Test if any study can be added with p<0.0019 
    ## #Update model 
    ## #Test if any study has p>0.0019 now 
    ## It converged! 
    ## # Final regression... 
    ## The studies used are: 
    ## - Years of Schooling (SSGAC)
    ## - LDL Cholesterol (GLGC)
    ## - Body Mass Index (GIANT)
    ## - Coronary Artery Disease (CARDIoGRAM)
    ## - Diastolic Blood Pressure (ICBP)
    ## - Height (GIANT)
    ## - Type 2 Diabetes (DIAGRAM)
    ## Estimating adjusted R-squared: 
    ## - in-sample adjusted R-squared for the all-chromosomes multivariate regression is 0.3211 
    ## - out-of-sample R-squared (masking one chromosome at a time), for the multivariate regression will be estimated when calculating the prior. 
    ## <><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><> 
    ## <<< Estimation of the prior >>>  
    ## > Creating the full Z-Matrix  
    ## # Loading the ZMatrix... 
    ## Selecting studies :
    ## 7 studies 
    ## 6,811,310 SNPs 
    ## # Adding data from the conventional GWAS : 
    ##  "lifegen_phase2_bothpl_alldr_2017_09_18.tsv.gz" 
    ## Done! 
    ## 6,513,704 SNPs in common between prior studies and the conventional GWAS 
    ## > Computing prior  
    ## # Calculating the prior chromosome by chromosome... 
    ##    Chromosome 1
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 2
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 3
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 4
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 5
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 6
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 7
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 8
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 9
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 10
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 11
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 12
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 13
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 14
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 15
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 16
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 17
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 18
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 19
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 20
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 21
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ##    Chromosome 22
    ## Running regression, 
    ## Calculating prior estimates for SNPs on this chromosome, 
    ## Calculating prior standard errors for SNPs on this chromosome, 
    ## ## Out-of-sample R-squared for MR instruments across all chromosomes is 0.3131
    ## ## Out-of-sample squared correlation for MR instruments across all chromosome is 0.3145
    ## ## Correlation between prior and observed effects for all SNPs is 0.2006
    ## ## Correlation between prior and observed effects for SNPs with GWAS p-value < 0.001 is 0.6078
    ## Done! 
    ## <><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><> 
    ## <<< Calculation of Bayes Factors and p-values >>>  
    ## > Calculating them for all SNPs  
    ## # Computing observed Bayes Factor for all SNPs... 
    ## Done! 
    ## # Computing BF p-values... 
    ##    using a distribution approach: 
    ## ... getting approximated p-values using non-linear quantiles  
    ## ... checking p-values near significance threshold  
    ##     everything is ok!  
    ## Done! 
    ## > Pruning and identifying significant SNPs 
    ##    Starting with 6,513,704 SNPs 
    ## # Selecting significant SNPs according to p-values... 
    ## 795 SNPs left 
    ## Done! 
    ## # Pruning significant SNPs... 
    ##    distance : 500Kb 
    ## 25 SNPs left 
    ## Done! 
    ## <><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
    ## Time of the analysis: 36 minute(s) and 15 second(s).

We can look at the results more in details.

## Prior GWASs used

``` r
print(getwd())
```

    ## [1] "/Users/nmounier/Documents/SGG/Projects/Packaging/bGWAS/doc"

``` r
coefficients_plot_bGWAS(Lifespan_bGWAS)
```

<img src="LifespanAnalysis/Lifespan_v1.0.0-results1-1.png" width="100%" />

7 prior GWASs are used to create the prior, the multivariate causal
effect estimates are consistent with what we would expect. On this
figure, the multivariate causal effect estimate and the 95% interval
from the multivariate MR model using all chromosomes (blac dot and bars)
as well as the per-chromosome estimates (grey bars) are represented for
each prior GWASs. Coronary Artery Disease (CAD) has the strongest
negative effect on lifespan. High Diastolic Blood Pressure (DBP) and
Body Mass Index (BMI) also decreases lifespan. We can also see that
education, in this case the number of years of schooling, has a positive
effect on lifespan.

Overall, the squared correlation between prior and observed effects is
about 0.04 and goes up to 0.369 when we consider only SNPs having at
least a moderate effect on lifespan (observed p-value \< 0.001).

With this approach, we identified
`nrow(extract_results_bGWAS(Lifespan_bGWAS))`:

``` r
# all hits
knitr::kable(extract_results_bGWAS(Lifespan_bGWAS) %>% transmute(rsid, chrm_UK10K, pos_UK10K, z_obs, mu_prior_estimate, mu_prior_std_error, z_obs, BF, BF_p=as.character(format(BF_p, scientific=T))))
```

| rsid       | chrm\_UK10K | pos\_UK10K |     z\_obs | mu\_prior\_estimate | mu\_prior\_std\_error |           BF | BF\_p        |
| :--------- | ----------: | ---------: | ---------: | ------------------: | --------------------: | -----------: | :----------- |
| rs429358   |           1 |  226237618 |  19.327786 |           1.4769473 |              1.185686 | 1.467887e+52 | 2.704073e-80 |
| rs10455872 |          10 |   37196047 |  10.281536 |           1.8779506 |              1.114773 | 8.741030e+15 | 3.528841e-26 |
| rs8042849  |           3 |   13384532 |  10.659387 |           0.1103939 |              1.084015 | 2.480031e+13 | 1.298723e-22 |
| rs11065979 |           4 |  137826792 | \-7.128082 |         \-1.6730147 |              1.131280 | 1.046698e+08 | 5.983488e-15 |
| rs2891168  |           6 |   86929591 |   6.601322 |           1.9599063 |              1.148937 | 1.835130e+07 | 8.576140e-14 |
| rs6511720  |           1 |  194047517 |   5.630731 |           3.3639409 |              1.203012 | 1.715581e+06 | 3.580849e-12 |
| rs8039305  |           3 |   24197617 |   6.413708 |           1.2254351 |              1.092939 | 1.253924e+06 | 5.916490e-12 |
| rs12924886 |           2 |  177100492 |   5.679317 |           2.2737479 |              1.092808 | 4.848462e+05 | 2.740447e-11 |
| rs61348208 |          11 |  104415621 |   5.823361 |           1.4487778 |              1.082599 | 1.914917e+05 | 1.244648e-10 |
| rs9393691  |           9 |   25616157 | \-5.570119 |         \-1.7169124 |              1.090056 | 1.241246e+05 | 2.533583e-10 |
| rs6719980  |          15 |   67150296 | \-5.406948 |         \-2.0140965 |              1.117846 | 1.151044e+05 | 2.867957e-10 |
| rs1230666  |          20 |   34088151 | \-5.804747 |         \-1.1755926 |              1.084836 | 1.023964e+05 | 3.476352e-10 |
| rs646776   |          20 |   24777265 | \-4.907710 |         \-4.1174475 |              1.195173 | 9.585604e+04 | 3.875245e-10 |
| rs56179563 |           8 |  123452475 |   5.190489 |           2.3991295 |              1.110002 | 8.276393e+04 | 4.935786e-10 |
| rs1275922  |          15 |   97402291 | \-5.816777 |         \-0.5943870 |              1.095019 | 3.040337e+04 | 2.588792e-09 |
| rs59234174 |           6 |   80328206 | \-5.127057 |         \-1.2962002 |              1.084586 | 1.188369e+04 | 1.239443e-08 |
| rs6558008  |           7 |   39617245 | \-5.424368 |         \-0.7778364 |              1.083506 | 1.159131e+04 | 1.292187e-08 |
| rs62477737 |           8 |   71432846 | \-5.269231 |         \-0.9908613 |              1.085216 | 1.083516e+04 | 1.446615e-08 |
| rs66720652 |           4 |   58305294 | \-5.346728 |         \-0.8580309 |              1.081783 | 1.055530e+04 | 1.511394e-08 |
| rs7742789  |           9 |   37523652 | \-5.299223 |         \-0.8823839 |              1.085563 | 9.642818e+03 | 1.758482e-08 |
| rs10465231 |           6 |  128337016 | \-5.155534 |         \-0.9065802 |              1.085858 | 6.360363e+03 | 3.534545e-08 |
| rs7599488  |          16 |   49438040 | \-4.662859 |         \-1.8924839 |              1.094489 | 6.194382e+03 | 3.695131e-08 |
| rs12459965 |           1 |  201155236 |   4.425792 |           2.5662130 |              1.091147 | 5.499658e+03 | 4.513166e-08 |
| rs2519093  |           6 |  170070135 | \-4.517091 |         \-2.1886219 |              1.111998 | 5.364198e+03 | 4.706506e-08 |
| rs2297359  |          10 |   36687959 |   5.407404 |           0.4532031 |              1.080801 | 5.286313e+03 | 4.823741e-08 |

``` r
# new hits (compared to conventional GWAS)
extract_results_bGWAS(Lifespan_bGWAS) %>%
  mutate(obs_p = 2*pnorm(-abs(z_obs))) %>%
  filter(obs_p>5e-8) -> NEW
knitr::kable(NEW %>% transmute(rsid, chrm_UK10K, pos_UK10K, z_obs, mu_prior_estimate, mu_prior_std_error, z_obs, BF, BF_p=as.character(format(BF_p, scientific=T))))
```

| rsid       | chrm\_UK10K | pos\_UK10K |     z\_obs | mu\_prior\_estimate | mu\_prior\_std\_error |         BF | BF\_p        |
| :--------- | ----------: | ---------: | ---------: | ------------------: | --------------------: | ---------: | :----------- |
| rs6719980  |          15 |   67150296 | \-5.406948 |         \-2.0140965 |              1.117846 | 115104.415 | 2.867957e-10 |
| rs646776   |          20 |   24777265 | \-4.907710 |         \-4.1174475 |              1.195173 |  95856.035 | 3.875245e-10 |
| rs56179563 |           8 |  123452475 |   5.190489 |           2.3991295 |              1.110002 |  82763.931 | 4.935786e-10 |
| rs59234174 |           6 |   80328206 | \-5.127057 |         \-1.2962002 |              1.084586 |  11883.686 | 1.239443e-08 |
| rs6558008  |           7 |   39617245 | \-5.424368 |         \-0.7778364 |              1.083506 |  11591.306 | 1.292187e-08 |
| rs62477737 |           8 |   71432846 | \-5.269231 |         \-0.9908613 |              1.085216 |  10835.161 | 1.446615e-08 |
| rs66720652 |           4 |   58305294 | \-5.346728 |         \-0.8580309 |              1.081783 |  10555.302 | 1.511394e-08 |
| rs7742789  |           9 |   37523652 | \-5.299223 |         \-0.8823839 |              1.085563 |   9642.818 | 1.758482e-08 |
| rs10465231 |           6 |  128337016 | \-5.155534 |         \-0.9065802 |              1.085858 |   6360.363 | 3.534545e-08 |
| rs7599488  |          16 |   49438040 | \-4.662859 |         \-1.8924839 |              1.094489 |   6194.382 | 3.695131e-08 |
| rs12459965 |           1 |  201155236 |   4.425792 |           2.5662130 |              1.091147 |   5499.658 | 4.513166e-08 |
| rs2519093  |           6 |  170070135 | \-4.517091 |         \-2.1886219 |              1.111998 |   5364.198 | 4.706506e-08 |
| rs2297359  |          10 |   36687959 |   5.407404 |           0.4532031 |              1.080801 |   5286.313 | 4.823741e-08 |

``` r
manhattan_plot_bGWAS(Lifespan_bGWAS)
```

<img src="LifespanAnalysis/Lifespan_v1.0.0-results3-1.png" width="100%" />

We can use direct effects to identify SNPs significantly acting on
lifespan independently from the prior GWASs used to create the prior:

``` r
# new hits (compared to conventional GWAS)
extract_results_bGWAS(Lifespan_bGWAS) %>%
  mutate(direct_z = mu_direct_estimate / mu_direct_std_error,
        direct_p = 2*pnorm(-abs(direct_z))) %>%
  filter(direct_p<5e-8) -> DIRECT
knitr::kable(DIRECT %>% transmute(rsid, chrm_UK10K, pos_UK10K, z_obs, mu_prior_estimate, mu_prior_std_error,  mu_direct_estimate, mu_direct_std_error, direct_z, direct_p=as.character(format(direct_p, scientific=T))))
```

| rsid       | chrm\_UK10K | pos\_UK10K |   z\_obs | mu\_prior\_estimate | mu\_prior\_std\_error | mu\_direct\_estimate | mu\_direct\_std\_error | direct\_z | direct\_p    |
| :--------- | ----------: | ---------: | -------: | ------------------: | --------------------: | -------------------: | ---------------------: | --------: | :----------- |
| rs429358   |           1 |  226237618 | 19.32779 |           1.4769473 |              1.185686 |            17.850838 |               1.551081 | 11.508644 | 1.193398e-30 |
| rs10455872 |          10 |   37196047 | 10.28154 |           1.8779506 |              1.114773 |             8.403586 |               1.497571 |  5.611478 | 2.006052e-08 |
| rs8042849  |           3 |   13384532 | 10.65939 |           0.1103939 |              1.084015 |            10.548993 |               1.474818 |  7.152742 | 8.506164e-13 |

Among these hits…: Not APOE (or CHRNA, but smoking not used so makes
sense?) … needs to be looked at a bit more\!  
Should we also look at non significant SNPs (based on BFs) but with
significant direct effects? -\> create a function to extract SNPs having
significant direct (posterior) SNPs independently of prior/BFs?