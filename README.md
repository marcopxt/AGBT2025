 **"Enhancing breeding efficiency: assessing the impact of SimpleMating algorithm for long-term genetic gain and diversity"**.

Authors: Marco Antonio Peixoto, Felipe Ferrão, Marcio Resende Jr.


Ouput from the analyses for AGBT 2025 of the abstract.

link1



### **Case 1**

The first set of simulations focused on a breeding program with two heterotic groups. The idea is two mimic a maize breeding breeeding program, with development of lines through doubled haploid production and the development of comercial hybrids created with combinations from the two heterotic groups. The simulations were conducted using AlphaSimR (Gaynor et al. 2021), as follows:

i. Base genome. The base genome was created following the maize settings in the *species* argument. A total of 300 QTLs per chromosome was simulated. 
ii. Trait.  A trait with 0.5 of heritability was simulated. Additive and domiance effects were assigned to the trait (being varDD and ddMean 0.2 and 0.92, respectively). 
iii. A breeding program was then simulated and a 15 years of burn-in was simulated. From here, all scenarios took place. 
iv. Genomic model. For the genomic model, the last three year of data (genotypes and phenotypes) were used to calibrate a model and the deploymet was used to select the best individuals and to create the mating plan in some scenarios (more details below). The BGLR package (Paulino and de los Campos (2021)) was used to fit a GBLUP (for predictig individuals) and an BayesB (for estimating marker effects), depending on each phase of the breeding program and scenarios were being used.

For more details on the simulation parameters, please, see Peixoto et al. (2024).

The second step was to implement the different scenarios for comparision. They were:

**GS**: A breeding program were the 40 crosses from each heterotic pools were randomly assigned after a selection of top indivduals (truncated genomic selection followed by randomly generation of a mating plan). 


**OCS**: Optimum cross-selection scenario. The individuals candidates to crosses were coming from the double haploid population and all possible combinations were estimated for each heterotic group. For such, we used SimpleMating (Peixoto et al. 2024) to predict usefulness of each cross, as follows:

### Usefulness Criterion (UC)
The usefulness criterion evaluates the expected genetic gain from a cross:

**UC = μ + k ⋅ σ_A**

where:  
- **μ** is the mean genetic value of the progeny.  
- **σ_A** is the additive genetic standard deviation of the progeny.  
- **k** is a weighting factor.  

### Genomic Estimated Breeding Value (GEBV)-Based Usefulness
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






###

2. Clonal breeding program
