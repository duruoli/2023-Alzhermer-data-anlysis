
# Background Information

## Amyloid[+] indicator:
- Pittsburgh compound B (PiB): a radioactive chemical to image beta-amyloid plaques in scans (priority, more decisive than CSF)
- CSF Cerebrospinal fluid: Aβ1–42 levels and the **Aβ1–42/Aβ1–40**(normalized by Aβ1–40) ratio are markers of amyloid pathology
  - Aβ1–40 doesn't differ between [+] and [-], measure the total Aβ1
  - normalization decreases the variance(dispersion of distribtuiton)

## covariates
- ε4 allele(/alio/等位基因） of APOE(gene): the strongest genetic risk factor for AD
  - ApoE has 3 major alleles: 2,3,4; ApoE4 is the high-risk indicator of AD
  - Everyone has two alleles of ApoE (one inherited from each parent)
  - ApoE4 related to slower **clearance rate** of Abeta => higher risk of AD
  - Even without ApoE4 can have AD

- CDR: Clinical Dementia Rating (Clinical evaluation) => classical diagnose method for AD
- Hippocampo volumn: AD=>small volumn => less neurons 
  - less neurons =*perhaps*=> less APP and sAPPbeta, Abeta, ect, thus potential risk: sAPPbeta indeed a biomarker, its lower value only due to less neurons (need normalization => also need hippocamp as a control variable)
- Total ventricular volume: the volume of the ventricles within the brain; an indicator for brain shrinkage, i.e., AD=>large volumn
- BMI: AD-thin

## biomarker candidate(predictor)
- sAPP: soluable amyloid precursor protein (APP); Cleavage by different enzymes(alpha, beta-secretase)+cut in different places => sAPPalpha, sAPPbeta
  - sAPPalpha vs sAPPbeta (production preclude each other)
  - **normalization**: sAPPbeta/sAPPalpha <= people have different APP levels (different baseline)
- sAPPalpha: good, protective, synaptic plasticity(memory, learning)
- sAPPbeta: Bad => amyloid-beta peptide => form Abeta (plaques)
  - Total Ab / sAPPb production rate ratio: infer efficiency or likelihood of the conversion of sAPPb to Abeta
  - sAPPα and sAPPβ tend to be positively correlated, without necessarily competing with each other (formed in different comaprtments)
- Abeta peptide: form plauques (many forms, e.g., Abeta40)
- FTR(Fractional Turnover Rate): “update rate” how fast sAPPalpha is synthesized and degraded (metabolism dynamic); clearance rate from the individual compartment(?)
- FCR(fractional clearance rate): only focus on breakdown rate vs FTR: dynamics
  ![image 80%](https://github.com/duruoli/2023-Alzhermer-data-anlysis/assets/82813264/715f6c08-4c43-443b-86dc-48532fd76232)


# Data Details
## "Artificial" variables
- FCR (clearance from the whole system) = 1 / [Delay Time + (1/FTR)]
- Production Rate = Concentration x FCR
  - Assume: production rate = clearance rate (production rate = concentration x FCR(fraction of the substance cleared per unit time) = (total) clearance rate)

## Response variable Amyloid[+]
- 35% subjects don't have PiB data
