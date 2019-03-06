# Getting started with Tableau Public

Tableau is a powerful data visualization tool, popular among both everyday users and data professionals.

Tableau Public is the free version of this tool; this tutorial was created using Tableau Public version 2019.1. There are several things to be aware of with regard to Tableau Public. It's free to download and use, but, aside from screenshots, the only way to save and share Tableau Public visualizations is to publish them to the Tableau Public website. That means they will be freely available on the web, and you will need to create a Tableau account in order to do this. Each Tableau Public user is allotted 10GB of space to store and share Tableau visualizations.

We will use Tableau Public to make several charts, which we will combine into a dashboard and a "story" that can be shared with a link or embedded on a webpage. [Here is a preview of what we'll make.](https://public.tableau.com/profile/miriam.posner#!/vizhome/IowaArtsGrants2015/Dashboard1?publish=yes) At the end of this tutorial, you'll find information on how to publish your Tableau workbook to the web. For this exercise, you will need two data files, both from [Gapminder Tools](https://www.gapminder.org/). 

* ![en_atm_co2e_pc.xlsx][1] (CO2 emissions in metric tons per capita)
* ![DataGeographies_v1_byGapminder.xlsx][2] (additional data for the 195 countries in the Gapminder dataset)

[1]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/data/en_atm_co2e_pc.xlsx
[2]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/data/DataGeographies_v1_byGapminder.xlsx

------

## 1. Import and prepare your data

After opening Tableau, you're presented with a list of file types you can choose to work with ("Connect"). Both of our data files are .xlsx files, so select **Microsoft Excel.** Then navigate to the file named **en_atm_co2e_pc.xlsx** you downloaded earlier and double-click to open it.

![][3]

[3]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/getting-started-with-tableau-public/connect.png

### 1.0 - Connect to the first data file

Tableau will connect to your file. Under "Connections" in the left sidebar, you should see the name of the file you opened, and below, under "Sheets," you should see a list of all the spreadsheets inside this Excel file (in this case, there is only one sheet). You will see a preview of this sheet in the lower pane of the main Data Source window. This preview of our Excel file is called a "connection" because Tableau is not really opening the file - it is opening a copy of it; this means that you will not make any changes to your original data files when you open them in Tableau.

![][4]

[4]:https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/getting-started-with-tableau-public/connection-preview.png

### 1.1 - Add column names

Column headers will be automatically generated, but we can see that the first row in the spreadsheet actually contains our column names. To fix this, click on the arrow next to the name of the file in the upper pane of the Data Source window to open a drop-down menu, and select **"Field names are in first row."** Now the column headers reflect the fact that our data consists of one column called "country" and many columns representing the CO2 emissions in metric tons per capita for each country, for the years 1960 to 2014.

![][5]

[5]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/getting-started-with-tableau-public/field-names.png

### 1.2 - Connect to the second data file

We have another Excel file that has additional information for each of the countries in our first file (the one with data on CO2 emissions). Let's open that one now. In the left sidebar, next to "Connections," click **Add** to add a second connector. Since our second file is also an Excel file, select **Microsoft Excel** and navigate to the file named **DataGeographies_v1_byGapminder.xlsx** that you downloaded earlier.

![][6]

[6]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/getting-started-with-tableau-public/add-connector.png

### 1.3 - Join the two spreadsheets

Now under "Connections," you will see both files, and if you select the Data Geographies file you just opened, you will see several sheets inside (listed under "Sheets" in the sidebar). The one we want is called **list-of-countries-etc**. 

![][7]

[7]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/getting-started-with-tableau-public/second-sheet.png

Drag **list-of-countries-etc** to the upper pane of the Data Source window, where the name of the first data connection is displayed. Tableau will recognize that you want to join these two datasets together. There are several options for joining, but we want to perform a **Full Outer** join to keep ALL the columns from both datasets. Click on **Full Outer** to indicate that we want to do a full outer join of our two datasets. 

![][8]

[8]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/getting-started-with-tableau-public/fulljoin.png

Then, under "Data Source," scroll down to select **country** and under "list-of-countries-etc" select **Name**. "Name" is the field that contains the name of the country in our second spreadsheet, and we want to match up our two spreadsheets using the field that contains each country's name.

![][9]

[9]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/getting-started-with-tableau-public/country-equals-name.png

### 1.4 - Pivot the year columns

In the lower pane of the Data Source window, you should now see a preview of our newly joined dataset! Use the scroll bars to see all of the columns in this new spreadsheet. In order to create visualizations of this data, we will need all of the year columns to be stacked or collapsed from "wide" to "long" format. To do this, click on the **1960** column and then scroll over and Shift + click on the **2014** column to select all of the year columns. Next, click the arrow at the top of the **2014** column and select **"Pivot"**. 

![][10]

[10]:

By telling Tableau to pivot all the year columns, you've created two new columns, which are automatically named **Pivot Field Names** and **Pivot Field Values**. Right-click on the column header for **Pivot Field Names** and select **"Rename"** - we want this column to be called **"Year"** since it now stores all the years that were previously used as column headers. Do the same thing to rename **Pivot Field Values** to **"CO2 per capita"**, as this column now stores the CO2 emission values by year for each country.

![][11]

[11]:

### 1.5 - Hide a redundant column

Notice that when we told Tableau to join our two datasets by the "country" and "Name" columns (which both hold the country names), Tableau kept both columns. To remove the redundant "Name" column, right-click on the **"Name"** column and select **"Hide"**. This will hide this redundant column from view.

### 1.6 - Export the joined dataset

Because Tableau *connects* to data files instead of directly opening them, when we make changes - such as joining two tables as we just did - we will need to save the changes explicitly. To do this, select **Data** on the navigation menu and click **"Export Data to CSV"**. Save the csv with the filename **"joined_co2_geography.csv"**. At this point, we will need to re-open this newly saved csv file, so go ahead and close the active Tableau workbook by selecting **File** --> **Close** from the navigation menu.

------

## 2. Create your first visualization

### 2.0 - Connect to the joined dataset

You should now be back on the Tableau Public home screen. (If you aren't, go up to **File** in the navigation menu and click **"Show Start Page"**.) This time, instead of opening Excel files, we will need to open a csv (or comma separated values) file. This is a kind of text file, so select **"Text file"** and open the **"joined_co2_geography.csv"** that you created earlier.

### 2.1 - Dimensions and measures

Tableau should recognize that the column headers are stored in the first row of our dataset, but if not, repeat **Step 1.1** as described above. At the bottom of the left sidebar, you should see a summary of all the pages you have open in your current Tableau Public workbook. Right now, you should just see **Data Source** and **Sheet 1**. Click over to **Sheet 1** now.

Tableau divides the fields in your dataset (that is, your columns) into **dimensions** and **measures**. Measures are fields whose values *measure* some attribute of your data (these are always numeric), while dimensions are fields whose values *describe* some attribute of your data (these can be categories, geographical or temporal scales, or other types of variables that do not measure a quantity).

In our dataset, we have **10 dimensions** and **3 measures** present in our actual spreadsheet, and Tableau has also calculated a few additional dimensions (such as "Measure Names") and additional measures (such as "Number of Records" and "Measure Values"). These automatically calculated dimensions and measures are distinguished by their italicized names.

### 2.2 - Discrete and continuous data

You may notice that most of our dimensions are coded in Tableau as blue - their icons are blue and a blue bubble appears around the names of the dimensions. Most of the measures, however, are green. This is because Tableau indicates **discrete data** using the color blue and **continuous data** using the color green. Discrete (also known as categorical or qualitative) data has values that are divided into discrete categories or classes, whereas continuous (also known as sequential or continuously varying) data has values that can be found anywhere within a range of possible values, such as the numbers from zero to a million.

While **most dimensions are discrete** and **most measures are continuous**, this may not be the case 100% of the time. In our dataset, the Year column, which is a dimension, is green because the Year values fall into a numeric range (in this case, between 1960 and 2014).

### 2.3 - 

------

## 3. Customize your visualization

------

## 4. Create another chart

------

## 5. Create a dashboard with multiple charts

------

## 6. Add interactivity and format your dashboard

------

## 7. Create a Tableau story

------

## 8. Export and share your visualizations





## 4. Your first visualization

Get started by clicking on **Applicant Arts Discipline** and drag it into the main section of the sheet (the **canvas**). It's not hugely exciting; you just see a list of arts disciplines.

There's a reason for that: Tableau doesn't know what you want it to count.

![][4]

[4]: images/getting-started-with-tableau-public/your-first-visualization.png

## 5. Tell Tableau which measure to use

We want Tableau to create a chart that visualizes the number of grants awarded per arts discipline. As we did when we used Excel to create a Pivot table, we want Tableau to summarize the values.

Luckily, Tableau has done this for us. Scroll to the bottom of the Data column, and look at the measure types that are in italics. You'll see that they contain the word **generated** next to them in parentheses. This means that these are numbers that Tableau has calculated for you.

You'll notice a measure called **Number of Records**. Since each record corresponds to a grant, that's the one we want. Click on this measure and drag it to the table on your canvas. Drop it in the second column of the table, where the values are currently represented as "Abc."

![][5]

[5]: images/getting-started-with-tableau-public/tell-tableau-which-measure-to-use.png

## 6. Choose the chart type you want

Once you've dropped the "Number of Records" measure, you'll see that they're nicely summarized for you in the table you created. You'll also notice that highlighted options appear in the palette of chart types on the right-hand side of your window. Now that you have measures, you have some chart options! Click on the bar chart.

![][6]

[6]: images/getting-started-with-tableau-public/choose-the-chart-type-you-want.png

## 7. Compare multiple values

You created a visualization! Now, let's see if we can create a stacked bar chart, the way we did with Excel. We'll show how **Application Instition Type** correlates with **Application Arts Discipline**.

Luckily, this is easy. Just drag the Application Institution Type measure onto the bar chart you've already created.

![][7]

[7]: images/getting-started-with-tableau-public/compare-multiple-values.png

## 8. Create a stacked bar chart

Now, let's switch to a stacked bar chart, so we can see the distinctions among institution types more clearly. You'll notice that as you hover over each segment, a tooltip gives you more information.

![][8]

[8]: images/getting-started-with-tableau-public/create-a-stacked-bar-chart.png

## 9. Give your chart a name

Click on your chart's title (it currently reads **Sheet 1**) to give it a more descriptive name.

![][9]

[9]: images/getting-started-with-tableau-public/give-your-chart-a-name.png

## 10. Start a new chart

Now let's make our second chart. Click on the **New worksheet** button (circled below) to begin our new visualization.

![][10]

[10]: images/getting-started-with-tableau-public/start-a-new-chart.png

## 11. Make a map

Tableau has automatically geocoded our geographic dimensions. You can tell because a tiny globe appears next to them. Drag **County** into the main canvas area, and give Tableau a moment to work.

![][11]

[11]: images/getting-started-with-tableau-public/make-a-map.png

## 12. You have a map!

Now that you've done a map, let's add a measure to it. Drag **Number of Records** into the main canvas area, on top of your map.

![][12]

[12]: images/getting-started-with-tableau-public/you-have-a-map-.png

## 13. Finish your map

Now the circles on your map grow larger as the number of grants awarded to that county increases. You can fine-tune the look of your map by altering the options in the **Marks window**. Give your new map a title, as you did for your chart.

![][13]

[13]: images/getting-started-with-tableau-public/finish-your-map.png

## 14. Create a dashboard

Now we'll combine our charts to create a **dashboard** -- a snapshot of multiple visualizations. Do that by clicking on the **Dashboard** button, circled below.

![][14]

[14]: images/getting-started-with-tableau-public/create-a-dashboard.png

## 15. Drag your sheets onto your dashboard

From the left-hand side of your dashboard's window, click on each of your sheets in turn and drag them into your main canvas. Very nice!

![][15]

[15]: images/getting-started-with-tableau-public/drag-your-sheets-onto-your-dashboard.png

## 16. Options for exporting

As I've mentioned, in order to make your visualization web-accessible, you will need to create a Tableau account and publish to Tableau's site. From there, you can embed your visualizations in other web pages. To begin this process, select **Save to Tableau Public As...** from the **File** menu. You will be prompted to begin the process of creating an account, logging in, and publishing to the web.

There's a *ton* more you can do with Tableau. You can begin learning about its other features [here](https://public.tableau.com/en-us/s/resources).

![][16]

[16]: images/getting-started-with-tableau-public/options-for-exporting.png
