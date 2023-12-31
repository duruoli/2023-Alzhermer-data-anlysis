# Preprocession

## Imbalance
1. Missing of Race and Hippocampal_Vol is balance between + and - groups
2. MICE-pmm: 5 imputation
   - balanced: Sexcode, Race
   - imbalanced: Age + BMI + ApoE_Status + APOE + apoE4dose + Cognitive_Impairment_Binary_Score + CDR + CDR_SOB + Hippocampal_Vol

## Outliers
1. Abnormal values
- No ApoE4 -> AD: over production rate

-----------Appendix--------------------------
1. Imbalance
detect imbalance:
- summary statistics: mean
- visualization
- statistical test: Mann-Whitney U test (for two groups), Kruskal-Wallis test (for more than two groups)
*non-normal distribution

Statistical test

**1. continuous:**
   
check normality (descriptive statistics, histogram, Q-Q plot, Shapiro-Wilk test)

**R**: qqnorm(x), qqline(x, col = 2), shapiro.test(x)

  
=> not very *strong* non-normal => size of 80 is large enough for ignoring normality assumption to use t-test

**"strong" or not**:  descriptive statistics(vs normality: skewness=0, kurtosis=3); clear deviations from the Q-Q line;  Shapiro-Wilk test (p-value<< 0.01)


=> very strong non-normal => non-parametric test: Mann-Whitney U test (for comparing two groups)

**R**: wilcox.test(group1, group2); by context

**2. categorical:**
   
*expected frequencies* of all cells > 5? : avoid extreme imbalances(in order to meet chi-square distribution)

**R**: chisq.test(data)$expected **OR** contingency table => corresponding row total * column total/overall total

  
=> yes, all >5 => chi-square test

**R**: chisq.test(data)


=> no + 2x2 tables => Fisher's exact test

**R**: fisher.test(data)

=> no + more than 2x2 => combines certain categories


  

