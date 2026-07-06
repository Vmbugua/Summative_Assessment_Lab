# Aviation Accidents Safety Analysis
 
## Business Problem
An airline/aircraft insurer client wants to know which aircraft makes and models show low rates of total destruction and low likelihood of fatal/serious passenger injury in an accident, along with general risk factors at play. Recommendations are split separately for small vs. large aircraft.
 
## Data
NTSB aviation accident data, 1948–2023 (`OriginalAviationData.csv`). Filtered to:
- Accidents from **1983 onward** (40-year assumed aircraft lifetime)
- **Professional builds only** (Amateur.Built == No)
- **Accidents only** (excludes Incidents, which are non-substantial by definition)
- **Airplanes only** (Aircraft.Category)
Cleaned dataset saved as `CleanedAviationData.csv`.
 
## Repo Structure
- `Aviation_Accidents_Cleaning.ipynb` — data loading, filtering, cleaning, feature construction
- `Aviation_Accidents_Data_Analysis.ipynb` — EDA, safety comparisons, recommendations
- `OriginalAviationData.csv` — raw data
- `CleanedAviationData.csv` — cleaned data used for analysis
## Key Derived Metrics
- **Destroyed.Aircrafts** — binary flag, 1 if Aircraft.damage == "Destroyed"
- **Fatal.Serious.Rate** — (fatal + serious injuries) / total occupants per accident
- **Make_Model** — combined identifier since model names repeat across makes
- Aircraft split into **small vs. large** using a 20-passenger threshold (based on average passengers per Make_Model)
- All group comparisons required a minimum sample size (small: n≥30, large: n≥10) to ensure statistically reliable results
## Key Findings & Recommendations
 
**Small Aircraft**
- Overall mean injury rate: 29.3% | destruction rate: 11.1%
- Best-supported pick: **Maule** (16.5% injury rate, n=215)
- Best-supported model: **Maule M-5-210C**
**Large Aircraft**
- Overall mean injury rate: 10.3% | destruction rate: 9.3%
- **Mcdonnell Douglas** shows the most consistent low-risk profile (tight distribution, few catastrophic outliers)
- Boeing has a larger sample (n=341) but shows a bimodal pattern — most accidents are low-injury, but a distinct subset are catastrophic (near 100% injury rate)
- Best-supported large aircraft models: **Boeing 777**, **Boeing 757** (both near 0% injury rate)
**Contributing Factors**
1. **Weather Condition** — VMC (clear) shows far lower destruction (~7%) and injury (~24%) rates than IMC (~36% / ~64%)
2. **Phase of Flight** — Landing and Taxi are safest (~1%); Climb and Maneuvering are highest risk (~28–36%)
## Limitations
- Small aircraft occupant counts include crew (not passenger-only)
- Broad.phase.of.flight missing in ~85% of records; findings based on the recorded subset
- Large aircraft sample sizes are limited (as few as 8 Make_Model types met the minimum threshold)
 
