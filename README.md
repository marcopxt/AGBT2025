# Enhancing breeding efficiency: assessing the impact of SimpleMating algorithm for long-term genetic gain and diversity.

**Marco Antonio Peixoto, Felipe Ferrão, Marcio Resende Jr.**

***


Details on the simulations for the abstract with the title before mentioned presented at the AGBT 2025.


### Introduction
The simulations were conducted using AlphaSimR (Gaynor et al. 2021). The mate allocation and restrictions to build mating plans in the scenarios was made using SimpleMating package (Peixoto et al. 2024) [link](https://github.com/Resende-Lab/SimpleMating)

<br>

### Material and Methods

##### **Case 1**

The first set of simulations focused on a breeding program with two heterotic groups. The idea is two mimic a maize breeding breeeding program, with development of lines through doubled haploid production and the development of comercial hybrids created with combinations from the two heterotic groups. The simulations for this case follow:

i. Base genome. The base genome was created following the maize settings in the *species* argument. A total of 300 QTLs per chromosome was simulated. 
ii. Trait.  A trait with 0.5 of heritability was simulated. Additive and domiance effects were assigned to the trait (being varDD and ddMean 0.2 and 0.92, respectively). 
iii. A breeding program was then simulated and a 15 years of burn-in was simulated. From here, all scenarios took place. 
iv. Genomic model. For the genomic model, the last three year of data (genotypes and phenotypes) were used to calibrate a model and the deploymet was used to select the best individuals and to create the mating plan in some scenarios (more details below). The BGLR package (Paulino and de los Campos (2021)) was used to fit a GBLUP (for predictig individuals) and an BayesB (for estimating marker effects), depending on each phase of the breeding program and scenarios were being used.

For more details on the simulation parameters, please, see Peixoto et al. (2024).

The second step was to implement the different scenarios for comparision. They were:

**GS**: A breeding program were the 40 crosses from each heterotic pools were randomly assigned after a selection of top indivduals (truncated genomic selection followed by randomly generation of a mating plan). 

**MPV**: Mid-parental value scenario. The individuals candidates to crosses were coming from the double haploid population and all possible combinations were estimated for each heterotic group. For such, we used SimpleMating (Peixoto et al. 2024) to predict the mid-parental values (UC) of each cross, as follows


$$
MPV = (GEBV_{p1} + GEBV_{p2})/2
$$

where:  
- GEBV is the genomic value predicted for each parent envolved in a cross (parent 1 and parent 2 - p1 and p2)  

The optimization of this scenario was made using the SimpleMating algorithm and a restriction on inbreeding was made by setting it to 0 and the maximum numer of contributions was set 3. Then, a mating plan was generated for each heterotic group.


**OCS**: Optimum cross-selection scenario. The individuals candidates to crosses were coming from the double haploid population and all possible combinations were estimated for each heterotic group. For such, we used SimpleMating (Peixoto et al. 2024) to predict Usefulness Criterion (UC) of each cross, as follows

$$
**UC = μ + ihσ**
$$

where:  
- **μ** is the mid-parental value of of the progeny.  
- **σ** is the additive genetic standard deviation of the progeny.
- **h** is the squared root of heritability.
- **i** is the selection intensity.  

The optimization of this scenario was made using the SimpleMating algorithm and a restriction on inbreeding was made by setting it to 0 and the maximum numer of contributions was set 3. Then, a mating plan was generated for each heterotic group.

**OpCS**: Optimal contribution selection. In this scenario, individuals candidates to crosses were coming from the first clonal phase and contributions were imposed for generating a crossing plan. The restriction were made in both, maximizing the genetic gain and restricting inbreeding (40% angle) using AlphaMate software (Gorjanc et al. 2028). A total of 40 crosses were also generated at the begging of each cycle for each heterotic group. The optimization was performed in the EBV values.


##### Set two

The second set of simulations focused on a clonal breeding program. After recombination through crosses, the best individuals will be selected and that clone will be assessed through the pipeline. The simulations setting were:

i. Base genome. The base genome was created following the generic settings in the *species* argument. A total of 300 QTLs per chromosome (12 pairs) was simulated. 
ii. Trait.  A trait with 0.5 of heritability was simulated. Additive and domiance effects were assigned to the trait (being varDD and ddMean 0.2 and 0.5, respectively). 
iii. A clonal breeding program was then simulated and a 15 years of burn-in was used to generate a commom starting point for all scenarios. From here, all scenarios took place. 
iv. Genomic model. For the genomic model, the last four year of data (genotypes and phenotypes) were used to calibrate a model and the deploymet was used to select the best individuals and to create the mating plan in some scenarios (more details below). The BGLR package (Perez and de los Campos (2021)) was used to fit a GBLUP (for predictig individuals) and an BayesB (for estimating marker effects), depending on each phase of the breeding program and scenarios were being used.

Then, the scenarios below were implemented for comparision. They were:

**GS**: A breeding program were the 80 crosses randomly assigned after a selection of top indivduals (truncated genomic selection followed by randomly generation of a mating plan). The genomic model here used targeted only additive effects.

**GPCP**: genomic prediction of cross-performance scenario. The individuals candidates to crosses were coming from the first clonal phase and all possible combinations were estimated. We used SimpleMating (Peixoto et al. 2024) to predict genomic prediction of cross-performance of each cross, as follows:



$$
GPCP = \sum_{i=1}^{n} \left[ a_i \left( p_i - q_i - y_i \right) + d_i \left( 2 p_i q_i + y_i \left( p_i - q_i \right) \right) \right]
$$


where:
- $a_i$ = Additive effect at locus *i*.  
- $d_i$ = Dominance effect at locus *i*.  
- $p_i$ = Frequency of the first allele at locus *i*.  
- $q_i$ = Frequency of the second allele at locus *i* ($q_i = 1 - p_i$).  
- $y_i$ = Indicator variable representing genotypic deviations.  
- $n$ = Total number of loci.  

The optimization of this scenario was made using the SimpleMating algorithm and a restriction on inbreeding was made by setting it to 0 and the maximum numer of contributions was set 3. Then, a mating plan was generated.


**OCS**: The individuals candidates to crosses were coming from the first clonal phase and all possible combinations were estimated. We used SimpleMating (Peixoto et al. 2024) to predict genomic prediction of cross-performance of each cross (as above described), as follows:

$$
**UC = GPCP + ihσ**
$$

where:  
- **GPCP** is the genomic prediction of cross-performance of of the progeny.  
- **σ** is the total genetic standard deviation of the progeny, which combines the addivite and dominance standard deviation.
- **h** is the squared root of heritability.
- **i** is the selection intensity.  

The optimization of this scenario was made using the SimpleMating algorithm and a restriction on inbreeding was made by setting it to 0 and the maximum numer of contributions was set 3. Then, a mating plan was generated for each heterotic group.

**OpCS**: Optimal contribution selection. In this scenario, individuals candidates to crosses were coming from the first clonal phase and contributions were imposed for generating a crossing plan. The restriction were made in both, maximizing the genetic gain and restricting inbreeding (40% angle) using AlphaMate software (Gorjanc et al. 2028). A total of 80 crosses were also generated at the begging of each cycle.


### Results


![Optim](../assets/images/Mate_Allocation.png){:width="40%" align="right"}

***









