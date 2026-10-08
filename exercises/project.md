# Final Project: Database Creation and Exploration

- Name: Kim Hummel
- Course: Database for Analytics
- Module: 7
- Database Used: US Department of Veterans Affairs Data Catalog
- Tools Used: PostgreSQL

## Original Data Source

I was searching for larger data sets and came upon the veterans database. I was originally looking at their suicide prevention data, but it was taking a long time to download so I started exploring their other data. As I was searching the database, there were multiple data sets labeled for the year 2023. As I looked at each data set, they were descriptors of veterans. I knew these could be joined together and analyzed.

https://www.data.va.gov/browse?sortBy=relevance&pageSize=20&limitTo=datasets&q=2023

[Link to Raw Data Files: project7_raw_data](../data/project7_raw_data/)

I originally pulled 5 spreadsheets to use as a database, but realized that one was redundant and that five was too many to work with for this project, so I narrowed it down to three. The three spreadsheets I used for this project are: county_data_2023, disability_by_county_2023, and poverty_disability_2023.

## Formatting Data

Before I uploaded the data I reformated the column names to align with standard practices and to lessen the chances of misspellings and typos on my part. I also made any missing values blank so it would bring up a "null" output instead of having to worry about which tables has dashes and which ones were blank.

When I tried to load the data from the csv files into PostgreSQL I kept getting error messages because the numerical values in the column had a comma in them, so it read it as two numbers in the same cell. In order to correct this I changed the data type from integer to text and was then able to upload the CSV. Then I used AI to help me remove the comma from the cells and then I changed the data type back into an integer.

![Data Type Change](../data/p7_images/data_type.png)

## Clean Data

### county_data_2023

The county_data_2023 in the fact table. It is a CSV file that has 7 columns and 781,200 rows. It has one date column, two integer columns, and four text columns. The data is time stamped from the date the data was pulled. It then contains every county in every state, and breaks down the number of veterans there based on age group and gender.

|Column Name| Data Type| Description|
|:------------:|:------------:|:-------------------------|
|pull_date| date| It is time stamped without a timezone. It is the same for every row.|
|fips| integer| An ID number for each county in each state. It is the foreign key for disability_by_county_2023 table.|
|county_state| text| Follows the County, State Abbreviation format.|
|just_state| text| Is just that, the state.|
|age_group| text| 4 options: 17 to 44, 45 to 64, 65 to 84, 85 and older.|
|sex| text| Either male or female.|
|veterans| integer| The number of veterans in that group: county, per age group per gender.|


![county_data_2023 Select *](../data/p7_images/county_data_2023.png)

### disability_by_county_2023

The disability_by_country_2023 is a dimension table whose key to the fact table is its FIPS code. It has 14 columns and 3,147 rows. There are two text columns and 12 integer columns. The table shows each county in each state, and then breaks down the total recipients by age, gender, and the percent of their service connected disability.

|Column Name| Data Type| Description|
|:------------:|:------------:|:-------------------------|
|fips_code| integer| An ID number for each county in each state.|
|state| text| The name of the state the county resides in.|
|county_name| text| The name of the county.|
|total_recipients| Integer| The total number of veterans that receive VA disability compensation benefits.|
|scd_0_20_percent| Integer| The number of veterans with a service-connected disability rating between 0% and 20%.|
|scd_30_40_percent| Integer| The number of veterans with a service-connected disability rating between 30% and 40%.|
|scd_50_60_percent| Integer| The number of veterans with a service-connected disability rating between 50% and 60%.|
|scd_70_90_percent| Integer| The number of veterans with a service-connected disability rating between 70% and 90%.|
|scd_100_percent| Integer| The number of veterans with a service-connected disability rating of 100%.|
|age_17_44| Integer| The number of veterans in the county that are receiving VA disability compensation benefits and are between the ages of 17 and 44.|
|age_45_64| Integer| The number of veterans in the county that are receiving VA disability compensation benefits and are between the ages of 45 and 64.|
|age_65_older| Integer| The number of veterans in the county that are receiving VA disability compensation benefits that are 65 and older.|
|male| Integer| The number of veterans in the county that are receiving VA disability compensation benefits that are male.
|female| Integer| The number of veterans in the county that are receiving VA disability compensation benefits that are female.

![disability_by_county_2023 Select *](../data/p7_images/disability_by_county_2023.png)


### poverty_disability_2023

The poverty_disability_2023 table is a dimension table. The key that connects it to the fact table will be age_group. It has 6 columns and 48 rows. One of the columns is a time stamp, four are text, and one is an integer. It tells the number of veterans that, time stamped per year, then broken down by rural or urban, the age group (under 65 or 65 and older), below or above poverty level, and then has a disability or not.

|Column Name| Data Type| Description|
|:------------:|:------------:|:-------------------------|
|pull_date| date| It is time stamped without a timezone. It is the same for every row.|
|urban_rural| text| Whether or not the veteran lives in an urban or rural area.|
|age_group| text| Whether or not they are less than 65 years old, or if they are 65 years or older.|
|poverty| text| Whether or not the veteran lives below the poverty line, or at or above the poverty line.|
|disability| text| Either the veteran has a disability or does not have a disability.|
|veterans| integer| The number of veterans that fit into the category.|


![disability_by_county_2023 Select *](../data/p7_images/disability_by_county_2023.png)

## Structure

I created a star warehouse that had the county_data_2023 as the fact table, and the two other tables as the dimension tables. 


Do this for the rest of the tables, and then a star chart like we did in module 6. That will take care o the data part.

#### Outline from Canva

- The initial data source
- The format of your data, include count of column and rows.
- Show a data dictionary - a table describing each data attribute/feature/column.
- Describe some of the obstacles you overcame to transform the data.
- Show your table structure including data types
- Select * from each of your tables
- Show some interesting queries from your tables.  Include:
   - At least one join
   - At least one query where you group by and aggregate data

Narrate your process, demonstrate the complexity of your dataset, share your challenges and solutions, and for max credit, summarize insights gained from your work.
