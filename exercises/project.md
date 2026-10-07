# Final Project: Database Creation and Exploration

- Name: Kim Hummel
- Course: Database for Analytics
- Module: 7
- Database Used: US Department of Veterans Affairs Data Catalog
- Tools Used: PostgreSQL

## Original Data Source

I was searching for larger data sets and came upon the veterans database. I was originally looking at their suicide prevention data, but it was taking a long time to download so I started exploring their other data. As I was searching the database, there were multiple data sets labeled for the year 2023. As I looked at each data set, they were descriptors of veterans. I knew these could be joined together and analyzed.

https://www.data.va.gov/browse?sortBy=relevance&pageSize=20&limitTo=datasets&q=2023

[Link to Raw Data Files: project7_raw_data](.data/project7_raw_data)

## Formatting Data

Before I uploaded the data I reformated the column names to align with standard practices and to lessen the chances of misspellings and typos on my part.

When I tried to load the data from the csv files into PostgreSQL I kept getting error messages because the numerical values in the column had a comma in them, so it read it as two numbers in the same cell. In order to correct this I changed the data type from integer to text and was then able to upload the CSV. Then I used AI to help me remove the comma from the cells and then I changed the data type back into an integer.

![Data Type Change](./data/p7_images/data_type.png)

## Clean Data

### County_Data_2023

The county_data_2023 in the fact table. It is a CSV file that has 7 columns and 781,200 rows. It has one date column, two integer columns, and four text columns. The data is time stamped from the date it was pulled. It then contains every county in every state, and breaks down the number of veterans there based on age group and gender.

|Column Name| Data Type| Description|
|:------------:|:------------:|:-------------------------:|
|pull_date| date| It is time stamped without a timezone. It is the same for every row.|
|fips| integer| An ID number for each county in each state.|
|county_state| text| Follows the County, State Abbreviation format.|
|just_state| text| Is just that, the state.|
|age_group| text| 4 options: 17 to 44, 45 to 64, 65 to 84, 85 and older.|
|sex| text| Either male or female.|
|veterans| integer| The number of veterans in that group: county, per age group per gender.|


![county_data_2023 Select *](./data/p7_images/data_county_2023.png)


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
