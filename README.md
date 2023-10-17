# Homework 2 of DATA 512
##### Author: Aaditya Parthasarathy

## Overview

This project delves into the concept of bias in data through an analysis of Wikipedia articles about cities in various US states. It aims to uncover variations in the coverage of US cities on Wikipedia across different states and assess the disparities in article quality. The assignment involves scrutinizing potential data bias, including identifying states with the most and least coverage relative to their populations, as well as the proportion of high-quality articles. Additionally, it ranks Census Divisions based on articles per person and the proportion of high-quality articles. Further insights and findings are discussed in the reflection at the end of this README.


### Licenses
The code used in this project is licensed under the MIT license. 

Also, this repo uses code developed by Dr. David W. McDonald for use in Data 512 which is provided under Creative Commons CC-BY license. (https://creativecommons.org/ and https://creativecommons.org/licenses/by/4.0/). The code snippets can be found in the helper_code folder

### API informaion

1. MediaWiki REST API for English Wikipedia: https://www.mediawiki.org/wiki/API:Main_page.
2. ORES API information: https://www.mediawiki.org/wiki/ORES.
3. ORES API Documentation: https://ores.wikimedia.org/docs.
4. LiftWing documentation for ORES: https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing/Usage.


## Data File Information

### Input data files:

1. `data/us_cities_by_state_SEPT.2023.csv`: Contains a dataset of Wikipedia article pages about US cities categorized by state. This is structured as state, city and url of the article's Wikipedia page
2. `data/NST-EST2022-POP.xlsx`: Provides population estimates for all US states. We mainly use the 2022 estimates for the analysis.
3. `data/US States by Region - US Census Bureau.xlsx`: Offers a listing of states organized by US census regional divisions for the 50 states.

### Intermediary data files:

1. `data/ores_files` - folder containing the JSON files of names and quality scores in batches of 5000 articles.
2. `data/all_page_info_dict.json` - file with city names and its corresponding last revision id.
3. `data/cleaned_us_cities_by_state_with_id.csv` - CSV file with cleaned states/cities and merged info with the `data/all_page_info_dict.json` for further processing.
4. `data/merged_data_ores.json` - This is the concatenation of all the JSON files in the `ores_files` folder

### Final outputs

1. `data/wp_scored_city_articles_by_state.csv` - This file contains the final, merged data on states, their regions, populations, article titles, article revision ids, and article qualities. This is the end result of the `data_processing.ipynb` file.
2. The resutls of the analysis are in the `data_analysis.ipynb` file as outputs.

## Known Issues and Special Considerations

1. There are duplicate entries in the `data/us_cities_by_state_SEPT.2023.csv`, which needs to be cleaned.
2. There are different naming conventions used between the `data/us_cities_by_state_SEPT.2023.csv` and the others, hence it needs to be cleaned.
3. Asynchronous functions are used, which can result in a data loss if not tracked. Also this was done due to the non async functions taking hours to process data (5+ hours). This async functions with proper rate limiting makes it faster to obtain data (10 mins vs 5 hours for the whole dataset.).
    - It is important to note that as we use async funtions, it is possible that one might get restricted after continuous use of the function. PLEASE EXERCISE CAUTION WHEN THE ASYNC FUNCTIONS ARE RUN, and read through the API read limits before running the code.


## Reproduction of the Analysis:

1. Place the 3 input files in the data folder (Provided).
2. Get your API keys following the directions from the `helper_code/wp_ores_liftwing_example.ipynb`
3. Run the data_processing.ipynb to obtain the intermediary files for analysis (Provided; no need to run again.). Please use the async functions sparingly to avoid API restrictions, and follow the directions in the Notebook to reproduce the same intermediary files.
4. Run the data_analysis.ipynb to view the results/tables.


## Research Implications

### My learnings

1. It is always important to check duplicates using multiple methods when unfamiliar with the dataset
2. Use Async functions to speed up data retreival from APIs, keeping in mind the Rate limits.

### Findings

**Potential biases expected in the dataset:**

Various types of biases can impact the content on Wikipedia. One such factor would be population based, wherecities with larger population would have a lot of people giving greater attention to detail in contract to places with lesser population, leading to less and poorer quality articles. Sometimes, a place might be more historically significant and it makes more sense that people like historians would monitor quality of such articles, leading to newly formed places with less articles.

**Using English Wikipedia as a data source:**

Most of Wikipedia's data is crowd sourced, making it difficult to monitor the quality and bias in the datasets. Many articles lack citations as these are not written by professional historians who verify every fact and document them, but by the common people. This adds up to the quality issues seen for many places. Finally, the data is ever-changing and this leads to an uncentainity of the articles being either updated continuously for accuracy or sometimes bad actors can add in intentional misinformation. It is also likely that more educated and internet savvy demographics would have a higher number and quality of articles than less literate places.

**Usefulness of dealing with biased/limited data:**

Though having faith in and basing decisions on biased or restricted data may pose challenges, it offers noteworthy advantages. Firstly, such data can provide valuable historical insights, enabling researchers to unearth the transformation of societal perspectives on specific subjects over time. Secondly, researchers can harness biased Wikipedia data to explore the socio-cultural influences affecting available information, thus elucidating how societies shape digital knowledge repositories. Moreover, analyzing biased data can reveal how both the media and the public interpret and respond to Wikipedia content, subsequently shaping the dynamics of online information dissemination and public discourse.

**Problems of dealing with biased/limited data:**

Dealing with biased data generally draws criticism and demands efforts to rectify the bias. In the case of a data source like Wikipedia, these challenges escalate rapidly. One immediate concern is that the analysis may produce skewed results, favoring overrepresented groups. This, in turn, could reinforce stereotypes, defeating the primary purpose of the analysis. Using such data in fields like policing and lawmaking could have severe ethical implications.


## Contact:
- Name - Aaditya Parthasarathy
- Email - aadi2000@uw.edu