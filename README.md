# Voter Sentiment and News-Opinion Analytics for US Presidential Race using Microsoft Fabric"

Project Overview: A Sentiment Analysis Report on US Presidential Election, 2024.

Problem Statement:

- Lack of real-time insights: The inability to monitor and analyze global news trends and public sentiment in real-time limits our ability to respond quickly to emerging issues and opportunities.

- Overwhelming data: The vast amount of news and opinion data available online makes manual analysis time-consuming and inefficient.

- Poor decision-making: Lack of data-driven insights leads to suboptimal decision-making, potentially impacting our business operations, reputation, and competitive position.

Project Goal:

Develop a data-driven solution to analyze global News and opinions data from the web to generate actionable insights.

Improve decision-making processes and gain a competitive advantage.

Project Scope:

1.Create and configure a Google Custom Search Engine JSON API to extract US Presidential Election related data globally

2. Use  Data Factory in Fabric environment to ingest data(in Jason format) from  Google Custom Search Engine API into Lake Database (Subset of One-Lake Storage in Microsoft Fabric).

3.Transform the data(Jason Format) in One Lake Storage into proper table structure that has pre-defined Schema and this table will be stored as a Delta tables through using Synapse Data Engineering Microsoft Fabric tool. A Spark Notebook is use to clean and transform the Jason file into cleaned data store in  delta tables.

4. Use the Synapse Data Science Tool to predict the sentiment of the ingested News data, using the Text Analysis model and load the final data to the Lake database

5. Importing curated sentiment analysis data into Power BI. This is used to create a News dashboard to monitor the latest News for the day.

6. Data Activator to configure alerts in Power BI visuals to predict the sentiment of the News-Positive, Negative or Neutral

7. Orchestrate the whole process as an End-to-End Pipeline using Fabric Data Factory.

***Tools Used

***SOLUTION ARCHITECTURE

STEPS


ENVIRONMENT SETUP
1.DATA SOURCE :Create and configure a Google Custom Search Engine API as real-time data source.

Prerequisite: A Gmail account
Steps:
- Log on to Google Cloud Platform: https://console.cloud.google.com/welcome?project=genial-reporter-434522-j4
- On the top-left, Click on "My Google Search API"
- From the dropdown, on the top-right, click "New Project"
- Under "Project Name" to the left, Input your project name <My Google Search API 2>
- Then, click "Create" button.
Then on Google Cloud Window, Under Quick Access
- Click on "API Apis& Service" tab,--> Library-->
- From the appear window, scroll down and choose "Custom Search API"
- Click "Enable"
- To the top-left, click on "Credentials" button.
- At the top, click "+ Create Credentials"
- From the drop-down, click "API Key"
- Copy and save generated API key in a secure place, then  click close button
- Then click on "Enable APIs & Service" to the left.
- Then, click on "Custom Search API" below.
- To your mid-right, under (Explore), click "TRY IN API EXPLORER"
This take you to a new window
- Click on "Get A KEY"
- An <Enable Custom Search API> title appears, click on the drop-down <Select or Create Project>
- Pick the name of the project you created in step 4 above <My Google Search API 2>
- Click NEXT
- Click on "SHOW KEY"
- Copy API Key  to secure place. The same API as the first API
- Click DONE
Back on The Programmable Search Engine
- Click on the highlighted "Control Panel". A new window appears< Create a new search engine>
- Field <Name Your Search Engine> : "Business Insight"
- Field <What to search> : "Search the entire web"
- Field <Search Setting> : Check "Image Search" and "Safe Search"
- Click "Create"
Your New Search Engine has been created . Copy the Search Engine ID

Use this Code Snippet as your Google CSE JSON API call

https://www.googleapis.com/customsearch/v1?key=YOUR_API_KEY&cx=YOUR_SEARCH_ENGINE_ID&q=SEARCH_QUERY&searchType=image

Where
Customize Google URL for your CSE = <https://www.googleapis.com/customsearch/v1> 
Key Or API Key = YOUR_API_KEY
cx = YOUR_SEARCH_ENGINE_ID
q = SEARCH_QUERY&searchType=image

2a.Create and configure Power BI Workspace for this project
Prerequisite: Enable Microsoft Fabric in Power BI Account as an Admin or Tenant.

- Go to <app.powerbi.com>
- Navigate to <workspaces> tab on the left
- At the bottom, click< + New Workspace >
 - A drop down at the top right; Enter name of workspace < Global News Data Analytics >
 - Optional: In the description box, give detail description of project.
 - Scroll downward to "Advance" assign licensing to the workspace by clicking on "Trial" if you using trial version or " Premium Capacity" if you are using premium license.
 - Click Apply button

2b. Create and configure Storage in Fabric environment, i.e. Lakehouse Database.
Switch from Power BI environment to Data Engineering environment
- Click on the Power BI icon on the bottom left.
- Then, click on the <Data Engineering > Component
- Then, click on Lakehouse icon
- From the dropdown, "Name Lakehouse"- <Google_Custom_SearchDB>
- Click "create"

DATA INGESTION
- On the bottom left, click on the Power BI icon.
- From the list of icons, click the "Data Factory" icon to move into Data Factory environment
- Click on the "Data Pipeline" tab, to create a new pipeline for the Data Factory.
- Name Pipeline <US Election Data Pipeline >
- Then, click "Create" to create Data Factory Pipeline
- At the top, click on "Copy Data" tab, from the drop-down, choose "Add to Canvas" to copy data from Source(Google CSE JSON API) to Destination(Lakehouse Database)
- In Data Factory canvas --> "General" tab --> "Name" : Copy latest news-opinions
- Then Click on "Source" tab. To configure Source Connection
 - In "Connection" field, Click on the drop-down and select "more"(because our data source is outside of Fabric Environment)
 - New Sources--> click on "View more"-->Scroll down and select "REST" from variety of options. REST is the resource use for connecting to APIs
 - On "Connection Setting" heading-->Base URL, input Endpoint and Query Parameter(s) < https://www.googleapis.com/customsearch/v1?q=YOUR_QUERY&cx=YOUR_ENGINE_ID&key=YOUR_API_KEY&q=SEARCH_QUERY >
 - On "Connection Credentials" sub-heading-->, input connection name for ease of reference purpose, say "News_Opinions"
 - Then, click "Connect"
 - Test Data Factory connection to  API Data Source, by clicking on the " Test Connection" tab. Connection was successful, this prove that  Data Factory has establish connection to my Google CSE JSON API source.
 - Preview Data, by clicking on the "Preview Data" tab
 - ***IMAGE
- Click on "Destination" tab
- On "Connection" field drop-down, select previously created Lakehouse Database "Google_Custom_SearchDB"
- On " Root Folder" field, Choose "File".- File because I am copying the raw data in a JSON format.
- On "File Path" field, Leave the "Directory" field empty. Fill the "File Name" with a file name, say<latest-US-election-news-opinion.json>. This will be the file name in the of copy data in destination Lakehouse DB.
-On "File Format" field drop-down, choose "JSON"
- Then, click on the "save" tab at the top-left to save the pipeline
- Click "Run" tab at the top to run pipeline.
Data is Successfully copy from API source to Lakehouse DB

*** IMAGE




C.DATA TRANSFORMAION(Incremental Loading)




D.SENTIMENT ANALYSIS(Incremental Loading)





E.DATA REPORTING



F.BUILDING PIPELINES



G.SETTING UP ALERTS(Using Data Activator)



H.END TO END TESTING
