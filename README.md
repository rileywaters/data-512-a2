# Bias in Data: data-512-a2

## Goal

Many datasets have significant bias that can over or under estimate a parameter leading to drastic changes in the results. If an analysis is done on a heavily biased dataset, its results could not reliably be applied to the larger population. It is important to identify what potential biases could exist in your data source and how they may affect your findings.

This assignment explores the concept of bias by looking into Wikipedia articles on political figues in different countries. We see how article coverage and article quality differ in the different countries and regions. It is shown that there exists significant regional bias within these articles that could affect any analysis done on Wikipedia data. The jupyter notebook hcds-a2-bias contains the step-by-step process to this discovery.

## Data Sources
The data sources are as follows:
- Wikipedia articles dataset on politions by country (page_data.csv): https://figshare.com/articles/Untitled_Item/5513449
- Population data from the Population Reference Bureau (WPDS_2018_data.csv):
https://www.prb.org/international/indicator/population/table/

Both of these files are in this repository in data/source

To obtain a quality score of the articles, the ORES system is used. ORES documentation can be found here: https://www.mediawiki.org/wiki/ORES. This is a machine learning system that predicts the quality of a wikipedia article and rates it as one of the following categories:

| Symbol | Description |
|--------|-------------|
| FA | Featured Article |
| GA | Good Article |
| B | B-class Article |
| C | C-class Article |
| Start | Start-class Article |
| Stub | Stub-class Article |

## Resources
This analysis was written in Python 3.6 running on a Jupyter Notebook environment.
Documentation for Python can be found here: https://docs.python.org/3.6/
Documentation for Jupyter Notebook can be found here: http://jupyter-notebook.readthedocs.io/en/latest/

'pandas' 0.25 is used to manipulate the data. Documentation here: https://pandas.pydata.org/pandas-docs/version/0.25/. It is available under BDS License: https://github.com/pandas-dev/pandas/blob/master/LICENSE
'oresapi' package is used to interface with ORES. It has been released under MIT License and found here: https://github.com/halfak/oresapi/

## Value Descriptions

wp_wpds_politicians_by_country.csv and wp_wpds_countries-no_match.csv

These are the final cleaned and merged datasets with the ORES predictions. The latter contains only countries that were in one dataset but not the other. The former is the dataset used in the analysis.

| Value | Description |
|-------|-------------|
| country | Country name |
| article_name | Wikipedia page name |
| revision_id | ID for the wikipedia article revision |
| article_quality | Quality prediction from ORES |
| population | The country's population |

final_analysis_data.csv and final_analysis_data_regional.csv

These two files contain aggregated fields used for the analysis. The first is the fields grouped by country. The second is the fields grouped by region.

| Value | Description |
|-------|-------------|
| country | Country name |
| region | Region name |
| articles_count | Total number of articles in the geographic area |
| population | Population of the geographic area |
| quality_articles_count | Number of quality articles in the geographic area |
| relative_quality | The percent of quality articles over the total articles |
| coverage | The percent of articles over the population|


## Considerations
Some rev ids were not found by ORES. These ids are stored in error_rev_ids.csv

'FA' and 'GA' are conidered quality articles for this project.

This code is released under MIT License

## Writeup and Implications
I expected to find some bias in the data prior to beginning this assignment. I know that English wikipedia is used overwhelmingly in English speaking countries, so there must be more pages in those countries. I also assumed that Wikipedia contributers are primarily based in North America or Europe, so there must also be more pages about politians in those regions. I found both of these to be true for the most part.

I found some more potential sources of bias while conducting this assignment. The contributor population is not the only parameter that could provide a source of bias in the dataset. Human interest plays a large role in the quality and coverage of articles. Some countries like North Korea, Syria, Saudi Arabia have very high quality articles. This is likely because there are many modern conflicts associated with these countries and so there is a lot of interest in their politians. However, these articles are likely not written by people from those countries (I don't think North Korea can access Wikipedia). 

It suprised me that many countries seem to have 0 'quality' articles. I looked into some of the individual predictions from the ORES system and, while I agreed with it most of the time, I did find a couple pages where I disagreed. The ORES system is flawed just like all other current ML solutions involving text. The results may change a lot by what the ORES system was trained on.

North America has one of the lower coverages which suprised me at first. Coverage seems to be largely affected by the population of the region. The highest coverage countries all have very small populations while the lowest coverage countries all have higher populations, with a few exceptions.

A realistic scenario might involve training text classifiers on Wikipedia data, such as the classifier we explored in class. Wikipedia has a lot of openly available text so it makes sense that organizations would use it to train their NLP models. However, it is now evident that any NLP model trained solely on Wikipedia data would involve a lot of bias, as there is massive regional disparity on the number of articles, the people writing them, and their quality.
