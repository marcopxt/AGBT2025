# **"Enhancing breeding efficiency: assessing the impact of SimpleMating algorithm for long-term genetic gain and diversity"**.

Authors: Marco Antonio Peixoto, Felipe Ferrão, Marcio Resende Jr.


Ouput from the analyses for AGBT 2025 of the abstract.

 The simulations were conducted using AlphaSimR (Gaynor et al. 2021), as follows:


### **Case 1**

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

### Case 2

The second set of simulations focused on a clonal breeding program. After recombination through crosses, the best individuals will be selected and that clone will be assessed through the pipeline. The simulations setting were:

i. Base genome. The base genome was created following the generic settings in the *species* argument. A total of 300 QTLs per chromosome (12 pairs) was simulated. 
ii. Trait.  A trait with 0.5 of heritability was simulated. Additive and domiance effects were assigned to the trait (being varDD and ddMean 0.2 and 0.5, respectively). 
iii. A clonal breeding program was then simulated and a 15 years of burn-in was used to generate a commom starting point for all scenarios. From here, all scenarios took place. 
iv. Genomic model. For the genomic model, the last four year of data (genotypes and phenotypes) were used to calibrate a model and the deploymet was used to select the best individuals and to create the mating plan in some scenarios (more details below). The BGLR package (Perez and de los Campos (2021)) was used to fit a GBLUP (for predictig individuals) and an BayesB (for estimating marker effects), depending on each phase of the breeding program and scenarios were being used.

Then, the scenarios below were implementedv for comparision. They were:

**GS**: A breeding program were the 80 crosses randomly assigned after a selection of top indivduals (truncated genomic selection followed by randomly generation of a mating plan). The genomic model here used targeted only additive effects.

**GPCP**: genomic prediction of cross-performance scenario. The individuals candidates to crosses were coming from the first clonal phase and all possible combinations were estimated. We used SimpleMating (Peixoto et al. 2024) to predict genomic prediction of cross-performance of each cross, as follows:



$$
MF1 = \sum_{i=1}^{n} \left[ a_i \left( p_i - q_i - y_i \right) + d_i \left( 2 p_i q_i + y_i \left( p_i - q_i \right) \right) \right]
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



2. Clonal breeding program

3. ### Genomic Estimated Breeding Value (GEBV)-Based Usefulness
Using genomic selection:  

**UC = GEBV + k ⋅ SD(GEBV)**  

where:  
- **GEBV** is the average genomic estimated breeding value of the progeny.  
- **SD(GEBV)** is the standard deviation of the progeny’s GEBVs.  

### Usefulness with Dominance and Epistasis
For cases where dominance and epistatic effects are considered:

**UC = μ + k₁ ⋅ σ_A + k₂ ⋅ σ_D + k₃ ⋅ σ_I**

where:  
- **σ_D** and **σ_I** are dominance and epistatic standard deviations.  
- **k₁, k₂, k₃** are weighting factors.  



