8/16/2023
Questions & Ideas

a. Seek clarification on comments in the "SAP_va_JDZ" file:

- "It is likely that only one will be included due to collinearity.":  

Could you clarify what is meant by "included" in this context? Are we referring to including them as control variables?
By "collinearity," is the reference to the covariates such as the two APOE covariates, and the two CDR covariates?  

If my understanding is correct, I would like to emphasize that  adding control variables often addresses the "imbalance" rather than the "collinearity" problem. E.g., if the mean or distribution of  "Age"  is quite different between Amyloid[+] and Amyloid[-], "Age" should be added as a control variable to handle this "imbalance"

- "Data should be adjusted for Sex and Age (or at least considered for adjustment)":  Am I correct in understanding that this adjustment refers to including "Sex" and "Age" as control variables in our regression model?

b. Logistic regression

- Regressing on only one independent variable of interest at a time: Is this a standard method to find biomarkers in our field?(sorry if my question is stupid). From a statistical standpoint, while this simplifies interpretation, I am concerned that it may overlook important combined effects between different independent variables

- New idea:
Could we explore "aggregate biomarkers" by regressing on pre-selected groups of independent variables? For instance, we might consider groups like (sAPPbeta/sAPPalpha Molar Production Rate Ratio, sAPPbeta/sAPPalpha FTR, sAPPbeta/sAPPalpha FCR). By careful selection, it could allow us to capture more complex relationships without risking collinearity and over-fitting. Your expertise on feasible combinations would be invaluable.

Answer: Yes (sAPPbeta/sAPPalpha)
