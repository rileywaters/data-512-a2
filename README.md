# Bias in Data: data-512-a2

## Goal

Many datasets have significant bias that can over or under estimate a parameter leading to drastic changes in the results. If an analysis is done on a biased dataset, it's results could not reliably be applied to the larger population. 

This assignment explores the concept of bias by looking into Wikipedia articles on political figues in different countries. We see how article coverage and article quality differ in the different countries and regions. 

The data sources are as follows:
- Wikipedia articles dataset on politions by country (page_data.csv): https://figshare.com/articles/Untitled_Item/5513449
- Population data from the Population Reference Bureau (WPDS_2018_data.csv):
https://www.prb.org/international/indicator/population/table/

Both of these files are in this repository in data/source

To obtain a quality score of the articles, the ORES system is used. This is a machine learning system that predicts the quality of a wikipedia article and rates it as one of the following categories:

| Symbol | Description |
|--------|-------------|
| FA | Featured Article |
| GA | Good Article |
| B | B-class Article |
| C | C-class Article |
| Start | Start-class Article |
| Stub | Stub-class Article |

ORES documentation can be found here: https://www.mediawiki.org/wiki/ORES

## Value Descriptions

wp_wpds_politicians_by_country.csv and wp_wpds_countries-no_match.csv
These are the final cleaned and merged datasets with the ORES predictions. The latter contains only countries that were in one dataset but not the other.

| Value | Description |
|-------|-------------|
| country | Country name |
| article_name | Wikipedia page name |
| revision_id | ID for the wikipedia article revision |
| article_quality | Quality prediction from ORES |
| population | The country's population |

final_analysis_data.csv and final_analysis_data_regional.csv
These two files are used for the analysis. The first is the fields grouped by country. The second is the fields grouped by region.

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
FA and GA are conidered quality articles for this project.

This code is released under MIT License
'oresapi' package is used to interface with ORES. It has been released under MIT License and found here: https://github.com/halfak/oresapi/blob/master/
