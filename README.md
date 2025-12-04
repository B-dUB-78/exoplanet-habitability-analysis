# exoplanet-habitability-analysis
A BigQuery SQL + Tableau case study analyzing exoplanet habitability using temperature, star type, radius, and ESI metrics.
 Exoplanet Habitability Analysis – BigQuery SQL + Tableau Case Study
By Bobby W. Hayden
🌍 Overview
📊 Data Source

This project uses exoplanet data from Kaggle:

Habitable Tidally-Locked Planets Candidates
by Roy F. Ayala
🔗 https://www.kaggle.com/datasets/royfayala/habitable-tidally-locked-planets-candidate
This project analyzes 70+ confirmed exoplanets using NASA-derived datasets to evaluate potential habitability.
Using Google BigQuery SQL, I cleaned, merged, and explored planetary characteristics such as:

Earth Similarity Index (ESI)

Surface temperature

Stellar type

Planetary radius (Earth radii)

Orbital characteristics

Four key dimensions were analyzed:

Habitability categories (based on ESI)

Star type influence on habitability

Temperature ranges

Planetary size (Earth radii)

Final visualizations will be produced in Tableau to create a polished, interactive dashboard.

🧪 Dataset

Data sourced from a custom case-study dataset combining:

confirmed_exoplanets

tidally_locked_habitable

habitable_candidates_raw

After cleaning and joining, a unified table was created:

exoplanet_case_study.merged_exoplanets


The analysis uses floats for radius, temperature, ESI, and orbital parameters.

🛠️ Skills Demonstrated

SQL (BigQuery)

Data cleaning & merging

CTEs, CASE statements, aggregations

Feature engineering (habitability scoring)

Statistical summaries

Data visualization (Tableau)

Scientific interpretation of planetary systems

Portfolio documentation (GitHub)

📊 Analysis & SQL Queries

Below are the core SQL queries used to analyze exoplanet habitability.

1️⃣ Habitability by ESI
SELECT
  CASE
    WHEN esi >= 0.8 THEN 'High Habitability'
    WHEN esi >= 0.5 THEN 'Moderate Habitability'
    ELSE 'Low Habitability'
  END AS habitability_category,
  COUNT(*) AS planet_count,
  ROUND(AVG(esi), 3) AS avg_esi,
  ROUND(AVG(pl_radius_earth), 2) AS avg_radius,
  ROUND(AVG(tsurf_k - 273.15), 1) AS avg_temp
FROM `bigquerypractice-473221.exoplanet_case_study.merged_exoplanets`
GROUP BY habitability_category
ORDER BY avg_esi DESC;

Results
Category	Planet Count	Avg ESI	Avg Radius (R⊕)	Avg Temp (°C)
High Habitability	23	0.863	2.06	12.3
Moderate Habitability	46	0.682	2.37	-10.2
Low Habitability	1	0.475	—	-68.4
