# Getting started with Tableau Public

Tableau is a powerful data visualization tool, popular among both everyday users and data professionals.

Tableau Public is the free version of this tool; this tutorial was created using Tableau Public version 2019.1. There are several things to be aware of with regard to Tableau Public. It's free to download and use, but, aside from screenshots, the only way to save and share Tableau Public visualizations is to publish them to the Tableau Public website. That means they will be freely available on the web, and you will need to create a Tableau account in order to do this. Each Tableau Public user is allotted 10GB of space to store and share Tableau visualizations.

We will use Tableau Public to make several charts, which we will combine into a dashboard that can be shared with a link or embedded on a webpage. [Here is a preview of what we'll make.](https://public.tableau.com/profile/rachel.starry#!/vizhome/GettingStartedGuide/GlobalCO2Emissionspercapita) At the end of this tutorial, you'll find information on how to publish your Tableau workbook to the web. For this exercise, you will need two data files, both from [Gapminder Tools](https://www.gapminder.org/). 

* ![en_atm_co2e_pc.xlsx][1] (CO2 emissions in metric tons per capita)
* ![DataGeographies_v1_byGapminder.xlsx][2] (additional data for the 195 countries in the Gapminder dataset)

[1]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/data/en_atm_co2e_pc.xlsx
[2]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/data/DataGeographies_v1_byGapminder.xlsx

<br>

------

# Table of Contents

1. [Import and prepare your data](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#1-import-and-prepare-your-data)
2. [Create your first visualization](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#2-create-your-first-visualization)
3. [Customize your visualization](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#3-customize-your-visualization)
4. [Create another chart](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#4-create-another-chart)
5. [Create a bar chart](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#4-create-another-chart)
6. [Create a dashboard](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#6-create-a-dashboard)
7. [Add interactivity and format your dashboard](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#7-add-interactivity-and-format-your-dashboard)
8. [Export and share your visualizations](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#8-export-and-share-your-visualizations)

------

## 1. Import and prepare your data

After opening Tableau, you're presented with a list of file types you can choose to work with ("Connect"). Both of our data files are .xlsx files, so select **Microsoft Excel.** Then navigate to the file named **en_atm_co2e_pc.xlsx** you downloaded earlier and double-click to open it.

![][3]

[3]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/connect.png

<br>

### 1.0 - Connect to the first data file

Tableau will connect to your file. Under "Connections" in the left sidebar, you should see the name of the file you opened, and below, under "Sheets," you should see a list of all the spreadsheets inside this Excel file (in this case, there is only one sheet). You will see a preview of this sheet in the lower pane of the main Data Source window. This preview of our Excel file is called a "connection" because Tableau is not really opening the file - it is opening a copy of it; this means that you will not make any changes to your original data files when you open them in Tableau.

![][4]

[4]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/connection-preview.png

<br>

### 1.1 - Add column names

Column headers will be automatically generated, but we can see that the first row in the spreadsheet actually contains our column names. To fix this, click on the arrow next to the name of the file in the upper pane of the Data Source window to open a drop-down menu, and select **"Field names are in first row."** Now the column headers reflect the fact that our data consists of one column called "country" and many columns representing the CO2 emissions in metric tons per capita for each country, for the years 1960 to 2014.

![][5]

[5]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/field-names.png

<br>

### 1.2 - Connect to the second data file

We have another Excel file that has additional information for each of the countries in our first file (the one with data on CO2 emissions). Let's open that one now. In the left sidebar, next to "Connections," click **Add** to add a second connector. Since our second file is also an Excel file, select **Microsoft Excel** and navigate to the file named **DataGeographies_v1_byGapminder.xlsx** that you downloaded earlier.

![][6]

[6]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/add-connector.png

<br>

### 1.3 - Join the two spreadsheets

Now under "Connections," you will see both files, and if you select the Data Geographies file you just opened, you will see several sheets inside (listed under "Sheets" in the sidebar). The one we want is called **list-of-countries-etc**. 

![][7]

[7]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/second-sheet.png

<br>

Drag **list-of-countries-etc** to the upper pane of the Data Source window, where the name of the first data connection is displayed. Tableau will recognize that you want to join these two datasets together. There are several options for joining, but we want to perform a **Full Outer** join to keep ALL the columns from both datasets. Click on **Full Outer** to indicate that we want to do a full outer join of our two datasets. 

![][8]

[8]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/fulljoin.png

<br>

Then, under "Data Source," scroll down to select **country** and under "list-of-countries-etc" select **Name**. "Name" is the field that contains the name of the country in our second spreadsheet, and we want to match up our two spreadsheets using the field that contains each country's name.

![][9]

[9]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/country-equals-name.png

<br>

[Read more about joining datasets in Tableau here.](https://onlinehelp.tableau.com/current/pro/desktop/en-us/joining_tables.htm)

<br>

### 1.4 - Pivot the year columns

In the lower pane of the Data Source window, you should now see a preview of our newly joined dataset! Use the scroll bars to see all of the columns in this new spreadsheet. In order to create visualizations of this data, we will need all of the year columns to be stacked or collapsed from "wide" to "long" format. To do this, click on the **1960** column and then scroll over and Shift + click on the **2014** column to select all of the year columns. Next, click the arrow at the top of the **2014** column and select **"Pivot"**. 

![][10]

[10]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/pivot.png

<br>

By telling Tableau to pivot all the year columns, you've created two new columns, which are automatically named **Pivot Field Names** and **Pivot Field Values**. Right-click on the column header for **Pivot Field Names** and select **"Rename"** - we want this column to be called **"Year"** since it now stores all the years that were previously used as column headers. Do the same thing to rename **Pivot Field Values** to **"CO2 per capita"**, as this column now stores the CO2 emission values by year for each country.

![][11]

[11]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/pivot-rename.png

<br>

### 1.5 - Hide a redundant column

Notice that when we told Tableau to join our two datasets by the "country" and "Name" columns (which both hold the country names), Tableau kept both columns. To remove the redundant "Name" column, right-click on the **"Name"** column and select **"Hide"**. This will hide this redundant column from view.

![][12]

[12]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/hide-name-column.png

<br>

### 1.6 - Export the joined dataset

Because Tableau *connects* to data files instead of directly opening them, when we make changes - such as joining two tables as we just did - we will need to save the changes explicitly. To do this, select **Data** on the navigation menu and click **"Export Data to CSV"**. Save the csv with the filename **"joined_co2_geography.csv"**. At this point, we will need to re-open this newly saved csv file, so go ahead and close the active Tableau workbook by selecting **File** --> **Close** from the navigation menu.

<br>

------

## 2. Create your first visualization


### 2.0 - Connect to the joined dataset

You should now be back on the Tableau Public home screen. (If you aren't, go up to **File** in the navigation menu and click **"Show Start Page"**.) This time, instead of opening Excel files, we will need to open a csv (or comma separated values) file. This is a kind of text file, so select **"Text file"** and open the **joined_co2_geography.csv** that you created earlier.

![][13]

[13]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/open-textfile.png

<br>

### 2.1 - Dimensions and measures

Tableau should recognize that the column headers are stored in the first row of our dataset, but if not, repeat [**Step 1.1**](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#11---add-column-names) as described above. At the bottom of the left sidebar, you should see a summary of all the pages you have open in your current Tableau Public workbook. Right now, you should just see **Data Source** and **Sheet 1**. Click over to **Sheet 1** now.

![][14]

[14]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/open-csv-sheet1.png

<br>

Tableau divides the fields in your dataset (that is, your columns) into **dimensions** and **measures**. Measures are fields whose values *measure* some attribute of your data (these are always numeric), while dimensions are fields whose values *describe* some attribute of your data (these can be categories, geographical or temporal scales, or other types of variables that do not measure a quantity).

![][15]

[15]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dimensions-measures.png

<br>

In our dataset, we have **10 dimensions** and **3 measures** present in our actual spreadsheet, and Tableau has also calculated a few additional dimensions (such as "Measure Names") and additional measures (such as "Number of Records" and "Measure Values"). These automatically calculated dimensions and measures are distinguished by their italicized names.

<br>

### 2.2 - Discrete and continuous data

You may notice that most of our dimensions are coded in Tableau as blue - their icons are blue and a blue bubble appears around the names of the dimensions. Most of the measures, however, are green. This is because Tableau indicates **discrete data** using the color blue and **continuous data** using the color green. Discrete (also known as categorical or qualitative) data has values that are divided into discrete categories or classes, whereas continuous (also known as sequential or continuously varying) data has values that can be found anywhere within a range of possible values, such as the numbers from zero to a million.

While **most dimensions are discrete** and **most measures are continuous**, this may not be the case 100% of the time. In our dataset, the Year column, which is a dimension, is green because the Year values fall into a numeric range (in this case, between 1960 and 2014).

<br>

### 2.3 - Data types

You may also notice that there are a variety of symbols next to each of our dimensions and measures. The **globe** symbol next to "Country," as well as "Latitude" and "Longitude," indicates spatial data, and the pound sign **#** next to "Year" and "CO2 per capita" represents numeric data. There are additional types of data, such as text (represented by **"Abc"**) and date (represented by a **calendar** symbol).

<br>

### 2.4 - Make a map

It's time to create our first visualization! All it takes to create a visualization in Tableau is to drag-and-drop one or more of our fields (that is - our dimensions and measures) onto the canvas. Try dragging **"Country"** from Dimensions onto the middle of the blank canvas area in **Sheet 1**. Because "Country" is spatial data, Tableau knows to create a map. It's as easy as that!

![][16]

[16]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/initial-map.png

<br>

### 2.5 - Add a measure to the map

A dot is added to the map for each country in our dataset. This isn't very helpful, so let's add another field that will tell Tableau how large each dot on the map should be. Try dragging **"CO2 per capita"** from Measures onto the map. Because "CO2 per capita" is a measure, Tableau knows to resize the points on the map (also known as "marks") with this measure. 

![][16b]

[16b]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/map-sized.png

<br>

### 2.6 - Give the sheet a name

Sheet 1 now contains a visualization, so it's a good idea to give the sheet a name so you will be able to distinguish it from other visualizations, once you have created more than one in your Tableau workbook. Right-click on **"Sheet 1"** and select **Rename** - you can give your visualizations any name you want, but let's keep it simple and call this sheet **"Map"**.

![][17]

[17]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/rename-sheet.png

<br>

------

## 3. Customize your visualization


### 3.0 - Customize the map marks

Now that you have a visualization, you can customize it in many ways. Notice that in between the left sidebar (where our data fields are displayed) and the main canvas, there is a set of panes labeled "Pages", "Filters", and "Marks". We want to look at the **"Marks"** pane right now. Notice that when we added **CO2 per capita** to the map, Tableau assumed that we wanted to view the SUM of CO2 emissions for each country, since our dataset includes CO2 emissions across many years. You can click on the arrow next to **"SUM(CO2 per capita)"** in the Marks pane to see the other kinds of calculations Tableau can perform when you ask it to display a measure, such as Average, Median, or Maximum. For now, we want to visualize the total CO2 emissions per capita for each country in our dataset, so leave or reset the calculation to SUM.

![][18]

[18]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/map-co2-marks.png

<br>

### 3.1 - Edit dot size

Inside the **Marks** pane, click on **Size**. The dots on our map are fairly small - let's make them all larger and easier to see by dragging the Size slider to the right a bit, as shown.

![][19]

[19]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/marks-size.png

<br>

### 3.2 - Edit dot color

We can also change the color of the dots on the map to reflect the intensity of CO2 emissions per capita for each country. In general, the human brain can better distinguish between color contrasts than between relative sizes of circles, so adding a color scale to our dots will make the map easier to read. To color the dots based on total CO2 emissions, drag **"CO2 per capita"** from Measures to the **Color** box inside the **Marks** pane.

![][20]

[20]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/marks-color.png

<br>

To the right of the canvas, Tableau displays the legends for your visualization. You may have to minimize the **"Show Me"** toolbar (at the top right corner of the Tableau window) in order to see the legends. A legend was added for the size of the dots, and now there is also a legend for the color scale. We can customize this color scale by clicking on **Color** inside the **Marks** pane. Select **"Edit Colors..."** to select a different color scale. In the pop-up window, scroll down to select the **"Temperature Diverging"** color palette, and click OK. You may also want to make the dots on the map slightly transparent since at some zoom levels, the dots overlap each other. (In the example shown, **80% opacity** has been selected.)

![][21]

[21]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/marks-color-scale-opacity.png

<br>

### 3.3 - Change the chart title

While "Map" is a useful name for our sheet, you may want to have a more descriptive title for your visualization. To edit the chart title, right-click on the title **"Map"** above the canvas, and select **"Edit title..."**.

![][22]

[22]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/chart-title-edit.png

<br>

In the pop-up window, give your map a new title and click OK.

![][23]

[23]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/chart-title-custom.png

<br>

------

## 4. Create another chart

### 4.0 - Create a new worksheet

Now let's create another visualization. At the bottom of the Tableau window, click on the **"New Worksheet"** button to create a new sheet.

![][24]

[24]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/new-worksheet.png

<br>

### 4.1 - Create a line chart

Now that we have created a map that visualizes the total CO2 emissions across the globe, we might want to create a chart to complement our map that visualizes how the amount of CO2 emissions per capita changed over time. 

Tableau's **"Show Me"** tool bar allows you to see what kinds of charts you can create with particular kinds of data. To do this, Ctrl + click on the dimensions and measures you want to add to the chart - in this case, Ctrl + click on both **"Year"** under Dimensions and **"CO2 per capita"** under Measures. In the **Show Me** toolbar, charts that you can make with these two fields will be highlighted. Click on the picture of the **line chart** in the Show Me toolbar, and Tableau will generate a chart with the data from the selected fields.

![][25]

[25]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/line-chart.png

<br>

### 4.2 - Add a detail to the line chart

When we selected "Year" and "CO2 per capita" to create the line chart, Tableau again automatically performed a SUM calculation to display the total CO2 emissions per year for all countries. If we want to see the breakdown of individual countries' CO2 emissions, we can drag the **"Country"** field from Dimensions onto the line chart. Now, in the **Marks** pane, "Country" appears as a **detail** in the line chart, and a line for each country's emissions appears on the chart. 

![][26]

[26]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/country-detail.png

<br>

Notice that again, by default, Tableau assumes that we want to visualize the SUM of CO2 emissions, but since each line represents a single country's values over time, there is no need to add values together. What we really want is for Tableau to simply use the **"CO2 per capita"** values themselves. To do this, click on the arrow next to **"CO2 per capita"** in the **Rows** pane above the canvas, and select **"Attribute"** instead of "Measure(SUM)". While in this instance, this change doesn't make a difference in the way our line chart is drawn, for other datasets you will often want to visualize a measure directly, rather than performing a calculation on it first.

![][27]

[27]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/change-measure-to-attribute.png

<br>

### 4.3 - Edit the line colors

Since both the map and the line chart visualize CO2 emission values, we may want to use the same color palette for both. Tell Tableau to color-code the lines according to each country's CO2 emissions, by dragging **"CO2 per capita"** from **Measures** to the **Color** box on the **Marks** pane, or directly onto the line chart canvas. Tableau will now use this measure to color the lines on the chart. Again, while it won't affect this particular chart, if you want to visualize actual values rather than a SUM or another calculation, you'll also need to change this for the color detail of **"CO2 per capita"** in the **Marks** pane.

To make the colors of our line chart match the map, click on **Color** in the **Marks** pane and edit the color palette, selecting the **Temperature Diverging** palette we used for the map, as in [**Step 3.2**](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#32---edit-dot-color) above. To ensure that Tableau uses the full color range from green to red, in the **Edit Colors** pop-up window, check the box that says **"Use Full Color Range"**.

![][28]

[28]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/full-color-range.png

<br>

### 4.4 - Finish customizing the line chart

Finish customizing your line chart by renaming the sheet and the chart title, as in [**Step 2.6**](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#26---give-the-sheet-a-name) and [**Step 3.3**](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#33---change-the-chart-title) above.

<br>

------

## 5. Create a bar chart

Now that we've walked through creating visualizations in two different ways - by dragging and dropping dimensions or measures directly onto a blank canvas ([**Step 2.4**][step24]) and by using the **Show Me** toolbar ([**Step 4.1**][step41]) - it's your turn to experiment! 

[step24]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#24---make-a-map
[step41]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#41---create-a-line-chart

Start by creating a new worksheet. This time, we want to create a **stacked bar chart** that visualizes the **total CO2 emissions per capita** for each of the **World bank regions**, colored by all the countries in each region.

Hint: Start by adding the two primary dimensions/measures to the map that you want to visualize. Then think about how we added color/details using the Marks pane earlier (in [**Step 3.2**][step32] and [**Step 4.3**][step43]). Take some time to experiment, but if you get stuck, you can read specific instructions on how to create this chart [by clicking here.](https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#how-to-create-the-bar-chart-for-step-50)

[step32]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#32---edit-dot-color
[step43]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/getting-started-with-tableau-public.md#43---edit-the-line-colors

The image below shows the finished visualization.

![][29]

[29]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/finished-bar-chart.png

<br>

------

## 6. Create a dashboard

### 6.0 - Create a new dashboard

A dashboard in Tableau is a kind of snapshot of multiple visualizations, allowing you to create custom infographics with your visualizations right in Tableau Public. You can customize dashboards by adding text, images, video - even webpages! - as well as various kinds of interactivity. 

Start by clicking the **New Dashboard** button at the bottom of the Tableau window.

![][30]

[30]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/new-dashboard.png

<br>

### 6.1 - Resize your dashboard

The first thing you'll want to do when creating a dashboard is decide whether you want it to be a fixed size - the default setting - or whether you want it to resize automatically to fit any screen it is displayed on. In this instance, we want our dashboard to resize automatically. On the left sidebar of your dashboard, under **Size**, click the arrow to open a drop-down menu with a few size options. This opens a window that allows you to choose a custom size for your dashboard; next to **Range**, click the arrow and select **"Automatic"**.

![][31]

[31]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/resize-automatic.png

<br>

### 6.2 - Add a visualization to your dashboard

Notice that below **Size** on the left sidebar is a section called **Sheets**. You should see a list of all the visualizations you created earlier, including Map, Line Chart, and Bar Chart. Adding visualizations to the dashboard is as easy as dragging and dropping your sheets onto the canvas.

Try it now by dragging **Map** to the blank canvas. Tableau automatically fills the canvas with your map visualization and adds the map legends to the far right side of the dashboard. Your dashboard should look like the image below.

![][32]

[32]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dashboard-map-only.png

<br>

### 6.3 - Add additional visualizations to your dashboard

We also want to add the line chart to this dashboard. If you click and drag **Line Chart** onto the canvas, Tableau will highlight in grey different sections of the canvas where you can add the line chart. We want it to appear below our map, so move your cursor to the lower half of the canvas until that part of the dashboard is highlighted, then release your cursor.

![][33]

[33]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dashboard-add-line-chart.png

<br>

The line chart should now appear in the lower half of the dashboard, and its legend has also been added to the right-hand side of the dashboard, under the map legends.

![][34]

[34]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dashboard-map-line-chart.png

<br>

### 6.4 - Edit dashboard legends

The legends for the map don't add much in terms of readability, so we can remove them from the dashboard. If you click on the uppermost legend (all are called **"CO2 per capita"** but the topmost one should show the map bubble sizes), you should see an **X** and some other manipulation tools appear on the legend. Click the **X** to remove the legend from the dashboard.

![][35]

[35]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dashboard-remove-legend.png

<br>

Do the same for the other map legend (the **"CO2 per capita"** legend whose scale reads 0 to 2985). We should keep the legend for the line chart, however, since we will want users to be able to see the range of total CO2 emissions for each country when they interact with the line chart. It is possible to move legends around by making them **floating legends**. Do this by clicking on the **"More Options"** arrow that appears next to the legend after you've clicked on it, and selecting **"Floating"**. 

![][36]

[36]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dashboard-legend-options.png

<br>

Now you can use the grey bar that appears on top of the legend to move it around your dashboard. Move it down so it appears closer to the line chart, as shown below.

![][37]

[37]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dashboard-with-legend.png

<br>

### 6.5 - Add and edit bar chart

Now let's add the bar chart to the right half of the dashboard. Click and drag **Bar Chart** until Tableau highlights with grey the entire right half of the dashboard, as shown below.

![][38]

[38]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dashboard-add-bar-chart.png

<br>

Tableau will add the bar chart as well as its legend to the right side of the dashboard. Move the **"CO2 per capita"** legend so it's on top of the line chart again, and remove the **"Country"** legend for the bar chart, since we don't need to include that in the dashboard (users can hover over the bar chart to see country information).

![][39]

[39]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dashboard-bar-chart-legends.png

<br>

Since the bar chart has horizontal bars, there is a lot of wasted space below it on the dashboard. Tableau makes it easy to turn horizontal bar charts into vertical column charts by swapping the rows and columns. To do this, switch back to the **Bar Chart** worksheet. Under the navigation menu is a toolbar with lots of icons. You'll want to click the **"Swap Rows and Columns"** icon, as shown below.

![][40]

[40]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/swap-rows-and-columns.png

<br>

### 6.6 - Resize dashboard tiles

Now head back to your dashboard. The column chart fits much better on the right-hand side of the dashboard! You can eliminate the rest of the empty space by hovering over the borders between the visualizations on the dashboard until the **double-arrow cursor** appears. Then click and drag to resize your bar chart so there is no extra white-space in the dashboard.

![][41]

[41]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/dashboard-resize-tiles.png

<br>

------

## 7. Add interactivity and format your dashboard

### 7.0 - Make the map a filter for the line chart

The dashboard is already looking pretty good! We can add to its interactivity by linking the map and line chart with a filter; this means that when a user clicks on a point on one chart, the relevant data point on another chart will be isolated. Let's make the map a filter for our line chart. To do this, click on the map in your dashboard and select the **funnel icon** on the chart manipulation tools, as shown below.

![][42]

[42]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/map-as-filter.png

<br>

### 7.1 - Remove interactivity from the bar chart

Test out the interactivity: if you click on a map point, such as Qatar (the country with the highest total CO2 emissions per capita) the other charts in the dashboard automatically update to show the relevant information for that country. Click again to de-select a specific country. 

While we want the line chart to update, we don't necessarily want the stacked bar chart to update when users interact with the map. To tell the bar chart not to update, click on it and in the drop-down menu for **"More Options"**, select **"Ignore Actions"**. Now try interacting with the map; the bar chart should no longer update when you click on different countries.

![][43]

[43]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/ignore-actions.png

<br>

### 7.1 - Freeze the line chart Y axis

You may notice that as you click on different countries on the map, whenever the line chart updates, Tableau re-draws the Y axis to scale, depending on the CO2 emission values for any given country. Using a different scale for the Y axis for each country doesn't allow users to consistently compare the data across countries, so we want to freeze the Y axis so that it uses the same scale no matter which country's data is visible. To do this, right-click on the line chart's Y axis and select **"Edit Axis..."**. 

![][44]

[44]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/edit-axis.png

<br>

In the pop-up window that appears, under **"Range"** select **"Fixed"** and then close out of the pop-up window (you do not need to click anywhere else to save this setting). Now when the line chart is re-drawn to display different countries' CO2 emissions, the Y axis will remain at the original scale.

![][45]

[45]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/edit-axis-fixed.png

<br>

### 7.3 - Add blank space and a dashboard title

It is possible to create very elaborate dashboards by incorporating text boxes, images, and other multimedia elements by dragging items from the **Objects** section at the bottom of the left sidebar. Experiment with these components by dragging them onto your dashboard; you can undo any action by clicking the **Undo** button on the icon toolbar or clicking **Ctrl + z**. 

For now, we can make our dashboard slightly more readable by adding a tiny bit of blank space between our charts, so there is more of a boundary between them. Under **Objects**, drag **Blank** to the canvas until the grey highlighted area is located between the map and line chart, then release your cursor. A blank tile is now located between the two visualizations. Resize the map and line chart until there is only a small blank area between them. 

![][46]

[46]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/add-blank.png

<br>

You can also add a blank area between the bar chart and the two charts on the left side of the dashboard. These blank areas help visually separate each of the charts in our dashboard. 

Go ahead and add a chart title as well! At the very bottom of the left sidebar, check the box that says **"Show dashboard title"**. Then rename the dashboard title in the same way you renamed chart titles, by right-clicking on it. You can format the text of the dashboard title; in the example shown, the words "CO2 Emissions" have been made bold and red.

![][47]

[47]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/add-title.png

<br>

------

## 8. Export and share your visualizations

To save and share your visualizations or dashboard, you will need to have a Tableau account so that you can save your workbook to your public Tableau profile. To publish your workbook, make sure you have your dashboard open (or whichever sheet or dashboard you want to be visible when someone views your workbook), and in the navigation menu select **"File"** --> **"Save to Tableau Public As..."**. Give your workbook a name, and click **Save**. A browser window should open automatically and take you to the public view of your workbook.

![][48]

[48]: https://github.com/rachelstarry/getting-started-with-tableau/blob/master/images/save-as.png

<br>

If you have not already created an account or logged into Tableau, you will be prompted to begin this process when you select **Save**. You can choose whether or not to make your workbooks publicly visible. [Follow the instructions in this article][save] if you would like to learn how to make your visualizations private or save workbooks locally to your computer.

There's a *lot* more you can do with Tableau. You can [begin learning about its other features here](https://public.tableau.com/en-us/s/resources)!

[save]: https://www.olgatsubiks.com/single-post/2017/03/20/How-to-save-Tableau-Public-workbooks-privately-on-your-computer

<br>

------

#### How to create the bar chart for Step 5.0:

1. Ctrl + click to select both **"World bank region"** under Dimensions and **"CO2 per capita"** under Measures, and select the recommended bar chart in the **Show me** toolbar.
2. Drag **"Country"** from under Dimensions to the bar chart canvas or to the **Details** box on the **Marks** pane.
3. Drag **"Country"** from under Dimensions to the **Color** box on the **Marks** pane.
4. Rename the sheet to **"Bar Chart"** and rename the chart title to **"Total CO2 emissions by world region"**. 

<br>