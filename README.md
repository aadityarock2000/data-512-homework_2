# Homework 2 of DATA 512
##### Author: Aaditya Parthasarathy

## Overview

This project delves into the concept of bias in data through an analysis of Wikipedia articles about cities in various US states. It aims to uncover variations in the coverage of US cities on Wikipedia across different states and assess the disparities in article quality. The assignment involves scrutinizing potential data bias, including identifying states with the most and least coverage relative to their populations, as well as the proportion of high-quality articles. Additionally, it ranks Census Divisions based on articles per person and the proportion of high-quality articles. Further insights and findings are discussed in the reflection at the end of this README.


### Licenses
The code used in this project is licensed under the MIT license. Also, this repo uses code developed by Dr. David W. McDonald for use in Data 512 which is provided under Creative Commons CC-BY license. (https://creativecommons.org/ and https://creativecommons.org/licenses/by/4.0/). The code snippets can be found in the helper_code folder

### API informaion

1. MediaWiki REST API for English Wikipedia: https://www.mediawiki.org/wiki/API:Main_page.
2. ORES API information: https://www.mediawiki.org/wiki/ORES.
3. ORES API Documentation: https://ores.wikimedia.org/docs.
4. LiftWing documentation for ORES: https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing/Usage.


## Data File Information

### Input data files:

1. 'data/us_cities_by_state_SEPT.2023.csv': Contains a dataset of Wikipedia article pages about US cities categorized by state. This is structured as state, city and url of the article's Wikipedia page
2. 'data/NST-EST2022-POP.xlsx': Provides population estimates for all US states. We mainly use the 2022 estimates for the analysis.
3. 'data/US States by Region - US Census Bureau.xlsx': Offers a listing of states organized by US census regional divisions for the 50 states.

### Intermediary data files:

1. 'data/ores_files' - folder containing the JSON files of names and quality scores in batches of 5000 articles.
2. 'data/all_page_info_dict.json' - file with city names and its corresponding last revision id.
3. 'data/cleaned_us_cities_by_state_with_id.csv' - CSV file with cleaned states/cities and merged info with the 'data/all_page_info_dict.json' for further processing.
4. 'data/merged_data_ores.json' - This is the concatenation of all the JSON files in the 'ores_files' folder

### Final outputs

1. 'data/wp_scored_city_articles_by_state.csv' - This file contains the final, merged data on states, their regions, populations, article titles, article revision ids, and article qualities. This is the end result of the 'data_processing.ipynb' file.


## Known Issues and Special Considerations

1. There are duplicate entries in the 'data/us_cities_by_state_SEPT.2023.csv', which needs to be cleaned.
2. There are different naming conventions used between the 'data/us_cities_by_state_SEPT.2023.csv' and the others, hence it needs to be cleaned.
3. Asynchronous functions are used, which can result in a data loss if not tracked. Also this was done due to the non async functions taking hours to process data (5+ hours). This async functions with proper rate limiting makes it faster to obtain data (10 mins vs 5 hours for the whole dataset.).
    - It is important to note that as we use async funtions, it is possible that one might get restricted after continuous use of the function. PLEASE EXERCISE CAUTION WHEN THE ASYNC FUNCTIONS ARE RUN, and read through the API read limits before running the code.


## Reproduction of the Analysis:

1. Place the 3 input files in the data folder (Provided).
2. Get your API keys following the directions from the 'helper_code/wp_ores_liftwing_example.ipynb'
3. Run the data_processing.ipynb to obtain the intermediary files for analysis (Provided; no need to run again.). Please use the async functions sparingly to avoid API restrictions, and follow the directions in the Notebook to reproduce the same intermediary files.
4. Run the data_analysis.ipynb to view the results/tables.


## Research Implications
