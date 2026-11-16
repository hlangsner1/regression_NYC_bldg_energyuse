# regression_NYC_bldg_energyuse
# This project demonstrates that the expected independent variables are not always explanatory of the model results. In this case, age of building, floor space, and energy mix were not as important as building operations and metering nuances as a determinant of emissions performance of New York City hotels in Manhattan. Many of the buildings made in the 1970-1990s before the implementation of Local Law 97 are less efficient than much older buildings. 

Cross-sectional OLS analysis of 2024 NYC Local Law 84 benchmarking data, estimating how building vintage, fuel mix, size and borough relate to energy and emissions intensity in NYC hotels, with heteroskedasticity-robust (HC3) standard errors.

I cleaned the 2024 LL84 disclosure file (39,090 properties). I dropped implausible Site EUI values (below 10 or above 1,000 kBtu/ft²) and invalid construction years, and kept properties with 1–4 buildings. Where Borough was missing, I filled it in from the ZIP code. After exploring the full portfolio, I narrowed to hotels (n ≈ 650) so I’d be comparing buildings with similar operating profiles. I estimated two OLS models with the same predictors: log Site EUI, and total GHG intensity (kgCO₂e/ft²). The predictors were construction-era bands, log gross floor area, natural gas share of site energy, and borough fixed effects, with Manhattan as the reference. I used HC3 robust standard errors because the residuals were heteroskedastic and non-normal.

Fuel mix and location explained more than building age. Each 10-point increase in gas share was associated with about 6.6% higher EUI. Hotels in Queens, Brooklyn and the Bronx ran about 22–27% lower EUI than comparable Manhattan hotels. Mid-century buildings (1940–1979) were the only vintage band with a significant EUI penalty, about 16%. The models explain 19% of the variation in EUI and 10% of the variation in GHG intensity, so most of it comes from factors the disclosure data doesn’t capture, such as operations, amenities and HVAC systems.

Data Source and Year: NYC_Building_Energy_and_Water_Data_Disclosure_for_Local_Law_84_2023_to_Present_(Data_for_Calendar_Year_2022-Present from NYC Open Data https://data.cityofnewyork.us/

Row count before: 39090
Row count post cleaning: 29590

Cleaning Steps: 
eliminating any year earlier than 1800 and after 2024 in  "Year Built" 
Converting three columns into numeric values
Controlling likely illogical values in ite EUI (kBtu/ft²
Limiting the model to listings of no more than 4 buildings under an id

Model Used: 
Cross-sectional OLS with categorical fixed effects (treatment coding)
Log-linear specification for EUI, so you can read coefficients as approximate percentage differences
HC3 heteroskedasticity-consistent covariance
Exploratory analysis with Pearson and Spearman correlations and LOWESS smoothing before the models



