SSIS & SQL Server project

*Practical situation : SQL Server et SSIS*

**Your goal :**

- Model a mini-datawarehouse (with the fact table and dimension tables) to store the collected data for analysis (star / snowflake model)

- Create an SSIS project allowing to integrate all this data, applying the modifications to the data you estimate are necessary

**Delivery :**

Your rendering should be in the form of a .ZIP archive containing the following:

\- A Word file explaining the important choices made during the project, showing clearly what has been achieved, and especially how

o This Word document must make it possible to understand all your project without even needing to open the solutions on which it rests

o During the correction, the Word document and the solutions will be analyzed and compared

o Do not forget to incorporate some screenshots (modeling, flow, ...)

o The chosen database modeling must be present in your Word rendering

\- The complete file of the SSIS solution

\- A .SQL file containing the scripts of the tables created (STA / ODS / DWH) in order to be able to run your feed solution



**

**Data :**

You will find a folder named "Data" in the project directory.

Inside are the files "Crimes\_in\_France\_1996\_2016" and "Departments\_mapping"

The first one contains information on the number of crimes and offenses recorded in France since 1996.

The data is arranged as follows:

\- Each column indicates the year and month statistics in the format YYYY\_MM

\- Each line represents a specific type of crime or offense

\- Each tab (sheet) represents a French department

The second is a mapping file between the department numbers and department name, as well as the associated region. Use it to consolidate your data.

**Remarks and hints about your SSIS project :**

|Libellé index|2016\_03|2016\_02|2016\_01|
| :- | :- | :- | :- |
|Règlements de compte entre malfaiteurs|8|6|11|
|Homicides pour voler et à l'occasion de vols|3|1|5|
• As it is, the data in the crime and crime file are not usable because the data per year are entered in **columns**.

It will be necessary to do the necessary at the level of transformations to pivot the data into rows.


In other words, this table :




Should end up in the following format :

|Libellé index|Période|Valeur|
| :- | :- | :- |
|Règlements de compte entre malfaiteurs|2016\_03|8|
|Règlements de compte entre malfaiteurs|2016\_02|6|
|Règlements de compte entre malfaiteurs|2016\_01|11|
|Homicides pour voler et à l'occasion de vols|2016\_03|3|
|Homicides pour voler et à l'occasion de vols|2016\_02|1|
|Homicides pour voler et à l'occasion de vols|2016\_01|5|






Use the « unpivot » transformation to realize this task.

• Take the time to read the topic, and imagine how many dimension tables can be created.

Do not forget to include in each time a "technical" key (the key whose value is generated at the dimension level) and, if it exists, a "business" key (the key whose value comes from the source file)

• At the transformations level, you will have to integrate checks on the data type of all the fields:

\- Are the "periods" correct (for example, "2016\_03" is correct but not "2016\_14")

\- Are numeric values really? Errors may have slipped into file ...

\- etc.

• Since the data are all located in one Excel file, with one department per tab, it will be necessary to perform a specific action to make this work of recovering on several tabs.

Below is a link explaining in detail how to get you out of it:

<https://www.mssqltips.com/sqlservertip/4157/how-to-read-data-from-multiple-excel-worksheets-with-sql-server-integration-services/>

Note that it is a bit **voluntary** complicated action, but I wish that you put it in place (with a lot of help thanks to the link) to understand which technique makes it possible to answer this particular problematic, namely to extract data from an Excel file with multiple sheets!

- Regarding the different "steps" to be respected in a datawarehouse loading process, as seen during the course, I want to be able to see the 3 studied zones : STA ODS DWH.

\- Extracting data from a source to a first table

\- Various transformations to apply on the data

\- Integration of the processed data into the final tables (fact table and dimension tables)

- Don’t forget about the technical and functional rejects !

