# Customer-data-feature-Engineering

Marketplace Features

Script will work as pipeline for data processing and feature generation. We need to change only path for files for reuse with different data source.
Created pre-processing and feature generation functions which will be called in main code.


Pre-processing data
•	Visitor log data table contains users’ interaction with website. We need to create features user wise, so only considering records where userid is available.
•	Created a function for time Pre-processing, it parses string date and unixtime to datetime.
•	We have 21 days window, so created a day column which have range between 1 to 21 days. It is calculated by subtracting starting day number minus 1 with VisitDateTime. For ex:
Starting date is 7th may,2021 then starting day number will be 6 (7-1) and subtracting VisitDateTime with this number. 
•	Merging Visitorlog table data with user table.
•	Imputing missing 'VisitDateTime' and 'day' values with minimum datetime values respective to webClientID.

Feature Generation functions
We will define function for each feature, then that function can be called in main code.
After all features are generated, they will be merged with userid into single dataframe using reduce function.
No_of_days_Visited_7_Days
•	We will use 'day' column for generating a flag of user activeness in website for 7 days window, day should be greater 14 and less than 22 for flag to be 1.
•	Calculated number of unique values of day by userid where flag of 7 days is 1.
•	Joining with user table on userid.
•	Filling na values with 0.

No_Of_Products_Viewed_15_Days
•	Created a flag column (‘product15’) for non-null product ids with day window range of 15 days.
•	ProductID have upper and lower case, so converting all to lower case.
•	Calculating count of unique product id with respect to user id where flag is 1.
•	Joining with user table on userid. 
•	Filling na values with 0.

User_Vintage
•	Calculated difference between signup date and 28th may,2018 in days.


Most_Viewed_product_15_Days
•	Converting Activity column to lowercase.
•	Creating flag for Users which page loaded product in between 15 days window.
•	Calculated count of each productid viewed by UserID.
•	Considering max count of productid for each userid, here we will use transform function with max aggregation for getting index number. Filtered max count rows with index number.
•	There can be multiple productids with same number of pageload, so created another dataframe where specifying maximum time for each product id.
•	Merging max time and max count dataframe.
•	Considering only productids with max time using transform function, this will give productids with max count and max time.
•	Some products were viewed at same time, so considering one of those products.
•	Merging data with user table, and we will get some user id with null productids.
•	Filling null productids with product101.

Most_Active_OS
•	Converted OS values to lowercase.
•	Calculated count of OS by userids.
•	Considering OS with maximum count.
•	Some OS have same count, so considering one of them.

Recently_Viewed_Product
•	Filtered users with pageload activity.
•	Calculated most recent viewed product by userids.
•	For some userids there are multiple products with recent most time, so considering one of them.
•	Merging data with user table, and we will get some user id with null productids.
•	Filling null productids with product101.

Pageloads_last_7_days
•	Filtered users with pageload activity and previously generated 7 days flag column.
•	Calculated count of pageload by userid.
•	Merging with user table and filling na with 0.

Clicks_last_7_days
•	Filtered users with clicks activity and previously generated 7 days flag column.
•	Calculated count of clicks by userid.
•	Merging with user table and filling na with 0.














  


