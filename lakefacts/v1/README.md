# Lake facts (v1)
One JSON per lake (`<state>/<app key>.json`), same key as the contour pack. Every fact carries its source (document, page, year, credit).
Facts feed the odds engine and Riggs's lake knowledge; the app says nothing when a fact is missing (owner 10-31).
Fields so far: species_present (presence from agency sampling), secchi_ft, ph, alkalinity_mg_l, conductivity_umhos,
growing_degree_days_50F, growing_season_days, max_depth_ft, mean_depth_ft, year_constructed, shoreline_dev_index.
Built by `rigology-app/tools/inhs_facts.py` (Illinois: INHS Compendium of 143 Illinois Lakes Vol. 1, 1993).
