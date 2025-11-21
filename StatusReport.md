Status Report


Within our project plan, we talked about our milestones and how we wanted to acquire the datasets, and begin understanding the data itself, as well as cleaning, formatting, and collecting it.
We also wanted to begin the adjustments, as well as merging the datasets, to make sure the data all made sense.


For that plan, both people helped with understanding what the columns of the data said, and also what the important columns were and what were unimportant. 
Afterwards, Seongwook started the project by adding the two datasets into a folder and using VS Code to do his work. Seongwook used an Excel to CSV function, as the plan was to use pandas, which is best with CSV.
To make sure the transformation from Excel to CSV was fine, he made sure to include all characters using the regex"[^0-9a-zA-Z_]", and also made the format all the same, lowercase and all.
After making sure we were calling the 2nd sheet of the Excel called annual, that function transformed it correctly, so next was to assign it to a name called xml_df for simplicity. The CSV was added normally and called csv_df. 


Afterwards, Seongwook looked at both columns' names, the shape, and just a small portion using the head of 3 to see the values. He found a similar column that can be used to combine the datasets.
The similar column was the date, specifically the year, as the XML file data was focused on the overall year. To account for this, Seongwook used the pandas function of datetime to transform the CSV's date and Excel data to have the same format.
Afterwards, Seongwook made a new column in excel_df called Year using the datetime to get it, and renamed the already existing List Year into just Year. 
Now with a column with the same name and similar values, he left merged the CSV, with just the Excel data value, as well as the year, ignoring the actual date of the Excel, as it was redundant. 
After merging, the two discussed what columns were unimportant to their questions, and dropped the columns called "Non Use Code", "Assessor Remarks", "OPM remarks", "Location", and "Date Recorded". The date recorded was dropped because there was already a date column with identical values.


This created a merged dataset containing all the csv_df values, which was the main focus, and the data value of the Excel that showed the average of the years.
Afterwards, Seongwook changed the date recorded to date to make the columns look nicer, and also focused our views on 2015 to 2023, as that was our desired time range in our project plans due to pre and post-COVID years.
Then Seongwook checked for any missing values, and after discussing togethor, decided to drop the unimportant rows and that had both Residential and property as empty, as if even one of the two values existed, there was something that the two could analyze.
Afterwards, Seongwook commited the code, and Alevtyna downloaded and worked on her part of the adjustment and got it read for analysis.

