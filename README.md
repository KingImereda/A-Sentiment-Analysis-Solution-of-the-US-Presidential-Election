# Voter Sentiment and News Analytics for US Presidential Race using Microsoft Fabric.

## Project Overview.

A Sentiment Analysis Report on US Presidential Election, 2024. This project is executed using Microsoft Fabric as a collaborative platform which require Data Engineering, Data Science and Data Analytic skill.

### Statement of Problem.

- Lack of real-time insights: The inability to monitor and analyze global news trends and public sentiment in real-time limits our ability to respond quickly to emerging issues and opportunities.

- Overwhelming data: The vast amount of news and opinion data available online makes manual analysis time-consuming and inefficient.

- Poor decision-making: Lack of data-driven insights leads to suboptimal decision-making, potentially impacting our business operations, reputation, and competitive position.

### Project Goal.

- Develop a data-driven solution to analyze global News and opinions data from the web to generate actionable insights.

- Improve decision-making processes and gain a competitive advantage.

### Project Scope.

1. Create and configure a Google Custom Search Engine JSON API to extract US Presidential Election related data globally

2. Use  Data Factory in Fabric environment to ingest data(in Jason format) from  Google Custom Search Engine API into Lake Database (Subset of One-Lake Storage in Microsoft Fabric).

3. Transform the data(Jason Format) in One Lake Storage into proper table structure that has pre-defined Schema and this table will be stored as a Delta tables through using Synapse Data Engineering Microsoft 
   Fabric tool. A Spark Notebook is use to clean and transform the Jason file into cleaned data store in  delta tables.
  
4. Use the Synapse Data Science Tool to predict the sentiment of the ingested News data, using the Text Analysis model and load the final data to the Lake database.

5. Importing curated sentiment analysis data into Power BI. This is used to create a News dashboard to monitor the latest News for the day.

6. Data Activator to configure alerts in Power BI visuals to predict the sentiment of the News-Positive, Negative or Neutral.

7. Orchestrate the whole process as an End-to-End Pipeline using Fabric Data Factory.

## Tools Used.
- ##### Pyspark.
- ##### SQL.
- ##### Data Factory(Microsoft Fabric)-For Data Injestion.
  - Google Custom Search Engine JSON API- Source.
  - Lakehouse Database- For data storage- Target.
- ##### Synapse Data Engineering(Microsoft fabric).
  - Spark Notebook-- For data transformation.
  - Lakehouse Database.
- #### Synapse Data Science(Microsoft Fabric).
- Spark Notebook-- For pre-trained Machine Learning Model.
- Lakehouse Database.

***SOLUTION ARCHITECTURE

STEPS


## ENVIRONMENT SETUP
### 1.DATA SOURCE 
Create and configure a Google Custom Search Engine API as real-time data source.
#### Prerequisite: A Gmail account.
-Steps:
 - Log on to Google Cloud Platform: https://console.cloud.google.com/welcome?project=genial-reporter-434522-j4
 - On the top-left, Click on "My Google Search API"
 - From the dropdown, on the top-right, click "New Project"
 - Under "Project Name" to the left, Input your project name <My Google Search API 2>
 - Then, click "Create" button.Then on Google Cloud Window, Under Quick Access
 - Click on "API Apis& Service" tab,--> Library-->
 - From the appear window, scroll down and choose "Custom Search API"
 - Click "Enable"
 - To the top-left, click on "Credentials" button.
 - At the top, click "+ Create Credentials"
 - From the drop-down, click "API Key"
 - Copy and save generated API key in a secure place, then  click close button
 - Then click on "Enable APIs & Service" to the left.
 - Then, click on "Custom Search API" below.
 - To your mid-right, under (Explore), click "TRY IN API EXPLORER". This take you to a new window.
 - Click on "Get A KEY"
 - An "Enable Custom Search API" title appears, click on the drop-down (Select or Create Project)
 - Pick the name of the project you created in step 4 above (My Google Search API 2)
 - Click NEXT
 - Click on "SHOW KEY"
 - Copy API Key  to secure place. The same API as the first API
 - Click DONE
Back on The Programmable Search Engine
 - Click on the highlighted "Control Panel". A new window appears< Create a new search engine>
 - Field (Name Your Search Engine) : "Business Insight"
 - Field (What to search) : "Search the entire web"
 - Field (Search Setting) : Check "Image Search" and "Safe Search"
 - Click "Create"
##### Your New Search Engine has been created . Copy the Search Engine ID

##### Use this Code Snippet as your Google CSE JSON API call

- https://www.googleapis.com/customsearch/v1?key=YOUR_API_KEY&cx=YOUR_SEARCH_ENGINE_ID&q=SEARCH_QUERY&searchType=image

##### Where
- Customize Google URL for your CSE = (https://www.googleapis.com/customsearch/v1) 
- Key Or API Key = YOUR_API_KEY
- cx = YOUR_SEARCH_ENGINE_ID
- q = SEARCH_QUERY&searchType=image

### Fabric Workspace.
Create and configure Power BI Workspace for this project
##### Prerequisite: Enable Microsoft Fabric in Power BI Account as an Admin or Tenant.
- Go to www.app.powerbi.com
- Navigate to "workspaces" tab on the left
 - At the bottom, click " + New Workspace "
 - A drop down at the top right; Enter name of workspace ( Global News Data Analytics )
 - Optional: In the description box, give detail description of project.
 - Scroll downward to "Advance" assign licensing to the workspace by clicking on "Trial" if you using trial version or " Premium Capacity" if you are using premium license.
 - Click Apply button

### Data Storage.
##### Create and configure Storage in Fabric environment, i.e. Lakehouse Database.
Switch from Power BI environment to Data Engineering environment
- Click on the Power BI icon on the bottom left.
- Then, click on the "Data Engineering" Component.
- Then, click on Lakehouse icon.
- From the dropdown, "Name Lakehouse"- (Google_Custom_SearchDB).
- Click "create".

## DATA INGESTION.
This is done using the Data Factory Component of Fabric.
- On the bottom left, click on the Power BI icon.
- From the list of icons, click the "Data Factory" icon to move into Data Factory environment
- Click on the "Data Pipeline" tab, to create a new pipeline for the Data Factory.
- Name Pipeline (US Election Data Pipeline).
- Then, click "Create" to create Data Factory Pipeline.
- At the top, click on "Copy Data" tab, from the drop-down, choose "Add to Canvas" to copy data from Source(Google CSE JSON API) to Destination(Lakehouse Database)
- In Data Factory canvas --> "General" tab --> "Name" : Copy latest news-opinions.
- ##### Click on Source tab.
- Then Click on "Source" tab. To configure Source Connection.
  - In "Connection" field, Click on the drop-down and select "more"(because our data source is outside of Fabric Environment)
  - New Sources--> click on "View more"-->Scroll down and select "REST" from variety of options. REST is the resource use for connecting to APIs
  - On "Connection Setting" heading-->Base URL, input Endpoint and Query Parameter(s) " https://www.googleapis.com/customsearch/v1?key=AIzaSyDiEhYXncP-RJf-tJ- 
    J5jrt73246yWTUww&cx=06d6d810465d04d97&q=US+presidential+election&hq=latest+news+opinions "
  - On "Connection Credentials" sub-heading-->, input connection name for ease of reference purpose, say "News_Opinions"
  - Then, click "Connect"
  - Test Data Factory connection to  API Data Source, by clicking on the " Test Connection" tab. Connection was successful, this prove that  Data Factory has establish connection to my Google CSE JSON API 
    source.
  - Preview Data, by clicking on the "Preview Data" tab
##### Screen Shot.

![Screenshot 2024-09-04 173434](https://github.com/user-attachments/assets/4bbf27f7-b75c-4768-9870-e84f874f0b7d)

- ##### Click on "Destination" tab
   - On "Connection" field drop-down, select previously created Lakehouse Database "Google_Custom_SearchDB"
   - On " Root Folder" field, Choose "File".- File because I am copying the raw data in a JSON format.
   - On "File Path" field, Leave the "Directory" field empty. Fill the "File Name" with a file name, say<latest-US-election-news-opinion.json>. This will be the file name in the of copy data in destination 
     Lakehouse DB.
   - On "File Format" field drop-down, choose "JSON"
   - Then, click on the "save" tab at the top-left to save the pipeline
   - Click "Run" tab at the top, to run pipeline.
##### Data is Successfully copy from API source to Lakehouse DB

![Screenshot 2024-09-04 183123](https://github.com/user-attachments/assets/1754a1ed-27c6-4e8f-9fd4-e829911b5907)


## DATA TRANSFORMAION(INCREMENTAL LOADING).
This is done using Synapse Data Engineering Component of Fabric.
- On the bottom left, click on the Power BI icon or whatever icon present there.
- From the list of icons, choose Synapse Data Engineering. 
- In Synapse Data Engineering environment, click on "Notebook" tab,-To create a Spark Notebook to "transform" the raw json file into a clean data table.
- On the top-left, click on the Notebook name and rename appropriately foe ease referencing.
##### Steps:
Use the created Notebook to import and read the raw json file that exist in stored Lakehouse Database.
- On the Left, click on "Lakehouse" button.
- On the left, click "Add Lakehouse" button.- This help in accessing the different tables and files that reside in the Lakehouse Database directly from the Notebook.
- Choose "Existing Lakehouse".
- Click "Add".
- Check or choose the Lakehouse where the raw json data resides.
- Click "Add".
- From the imported Lakehouse Database to the left, choose DB where needed data or "File " (-This shows all files that reside in the Lakehouse Database),then "..." , then "Load Data" 
- There are two options (Spark or Pandas), Choose "Spark". 
A code is automatically generated to read the raw json file as a Pyspark DataFrame.
```
df = spark.read.option("multiline", "true").json("Files/latest-news-US-presidential-election.json")
# df now is a Spark DataFrame containing JSON data from "Files/latest-news-US-presidential-election.json".
display(df)

```
- Then, "run" the cell.

```
#Select the items column where the nested data is and ignore the other columns.

df = df.select(["items"])

```
```
from pyspark.sql.functions import explode

# Explode json object(items) as an alias(json_object)

df_explode = df.select(explode(df["items"]).alias("json_object"))

```
```
display(df_explode)
```
```
# Converting the Exploded Json Dataframe to a single Json string list,i.e. "json_list" variable

json_list = df_explode.toJSON().collect()

```
```
#Testing the JSON string list with the first news article

print(json_list[0])


```
```
import json
# Convert the JSON String to a JSON dictionary

news_json =json.loads(json_list[7])

```
```
# Testing the JSON Dictionary.

display(news_json["json_object"]["snippet"])

```
```
print(news_json["json_object"]["displayLink"])
print(news_json["json_object"]["link"])
print(news_json["json_object"]["kind"])
print(news_json["json_object"]["pagemap"]["cse_image"])
print(news_json["json_object"]["pagemap"]["cse_thumbnail"])
print(news_json["json_object"]["pagemap"]["metatags"])
print(news_json["json_object"]["title"])
print(news_json["json_object"]["snippet"])

```

```
# Processing all the json items from list[0-9].These columns capture  all the different information I want to extract fron the News/Articles c 
# using for loop function to iterate all the News/Articles one after the other.

import datetime
# Needed to add a date column to the list, because not all news and opinion content has published date
displayLink = []
link = []
kind = []
pagemap = []
title = []
snippet = []
date_fetched = []

# Process each JSON object in the list
for json_str in json_list:
    try:
        # Parse the JSON string into a dictionary
        article = json.loads(json_str)

        # Extract information from the dictionary
        displayLink.append(article["json_object"]["displayLink"])
        link.append(article["json_object"]["link"])
        kind.append(article["json_object"]["kind"])
        pagemap.append(article["json_object"]["pagemap"]["cse_image"])
        pagemap.append(article["json_object"]["pagemap"]["cse_thumbnail"])
        pagemap.append(article["json_object"]["pagemap"]["metatags"])
        title.append(article["json_object"]["title"])
        snippet.append(article["json_object"]["snippet"])

        # Append the current date to the date list
        date_fetched.append(datetime.datetime.now().strftime("%Y-%m-%d"))
    except Exception as e:
        print(f"Error processing JSON object {e}")

```
```
# Create a new Dataframe with the Custom Schema defined

from pyspark.sql.types import StructType, StructField, StringType

# combine the list using the zip function to create the data.

data = list(zip(displayLink,link,kind,pagemap,title,snippet,date_fetched))

# Define schema for the Dataframe with the proper data type for all the columns in the Dataframe
schema = StructType([
    StructField("displayLink", StringType(), True),
    StructField("link", StringType(), True),
    StructField("kind", StringType(), True),
    StructField("pagemap", StringType(), True),
    StructField("title", StringType(), True),
    StructField("snippet", StringType(), True),
    StructField("date_fetched", StringType(), True),
])

#create Dataframe
df_cleaned = spark.createDataFrame(data, schema=schema)

```
```
display(df_cleaned)
```

![Screenshot 2024-09-06 110507](https://github.com/user-attachments/assets/cc82f1c4-3307-424f-8b01-0e1de665724a)

```
from pyspark.sql.functions import col
# Renamed col [displayLink] to [provider] and col[link] to url

df_cleaned_final = df_cleaned.withColumnRenamed("displayLink", "provider").withColumnRenamed("link","url")

```
##### Screenshot.

![Screenshot 2024-09-06 111240](https://github.com/user-attachments/assets/ec34edb5-6a25-4140-bd2f-3c29a8a9f347)



```
#The code effectively handles the scenario where the target table already exists by performing a MERGE operation to update existing rows and insert new ones based on specified conditions. This ensures that the #data in the Delta table remains up-to-date and consistent with the df_cleaned_final DataFrame. i.eSave the table in delta format and perform an incremental loading SCD_1

from pyspark.sql.utils import AnalysisException
from pyspark.sql.functions import col, max

table_name = "Election.tbl_latest_news"

def handle_table_exists():
    # Create a unique version of the DataFrame to avoid conflicts during the MERGE operation
    # Adjust the grouping and aggregation according to your specific key columns
    df_cleaned_final_unique = df_cleaned_final.groupBy("provider").agg(
        max("url").alias("url"),
        max("kind").alias("kind"),
        max("pagemap").alias("pagemap"),
        max("title").alias("title"),
        max("snippet").alias("snippet"),
        max("date_fetched").alias("date_fetched")
    )

    # Register the cleaned DataFrame as a temp view
    df_cleaned_final_unique.createOrReplaceTempView("vw_df_cleaned_final")

    # Perform the MERGE operation
    spark.sql(f"""
        MERGE INTO {table_name} target_table
        USING vw_df_cleaned_final source_view
        ON source_view.provider = target_table.provider
        WHEN MATCHED AND
            (source_view.url <> target_table.url OR
            source_view.kind <> target_table.kind OR
            source_view.pagemap <> target_table.pagemap OR
            source_view.title <> target_table.title OR
            source_view.snippet <> target_table.snippet OR
            source_view.date_fetched <> target_table.date_fetched)
        THEN UPDATE SET *
        WHEN NOT MATCHED THEN INSERT *
    """)

# Check if the table exists
table_exists = spark.catalog.tableExists(table_name)

if not table_exists:
    # If the table doesn't exist, create it
    df_cleaned_final.write.format("delta").saveAsTable(table_name)
    print("Table created successfully")
else:
    print("Table Already Exists")
    handle_table_exists()
```

## SENTIMENT ANALYSIS USING SYNAPSE MACHINE LEARNING(Incremental Loading).
This is done using Synapse Data Science Component of Fabric.
- On the bottom left, click on the Power BI icon or whatever icon present there.
- From the list of icons, choose Synapse Data Science option. 
- In Synapse Data science environment, click on "Notebook" tab,-To use pre-trained Machine Learning Model.
- On the top-left, click on the Notebook name and rename appropriately for ease referencing.
##### Steps:
Use the created Notebook to import and read the cleaned data stored in a delta table in Lakehouse Database.
- On the Left, click on "Lakehouse" button.
- On the left, click "Add Lakehouse" button.- This help in accessing the different tables and files that reside in the Lakehouse Database directly from the Notebook.
- Choose "Existing Lakehouse".
- Click "Add".
- Check or choose the Lakehouse where the data resides.
- Click "Add".
- From the imported Lakehouse Database to the left, click on "Tables " (-This shows tables that reside in the Lakehouse Database),then "..." , then "Load Data" 
- Then, Choose "Spark".
A code is automatically generated to read the raw delta table as a Pyspark DataFrame.
```
# please remove the "Limit 1000"
df = spark.sql("SELECT * FROM Election.tbl_latest_news ")
display(df)
```
```
# import the synapse ML library (Importing a pre-trained model called AnalyzeText)

import synapse.ml.core
from synapse.ml.services import AnalyzeText

```

```
# CONFIGURING PRE-TRAINED MODEL
```

```
# import the model and configure the input and output columns
model = (AnalyzeText()
        .setTextCol("snippet")
        .setKind("SentimentAnalysis")
        .setOutputCol("response")
        .setErrorCol("error"))
```

```
#Apply the model to our Dataframe
result = model.transform(df)

```

```
display(result)

```

![Screenshot 2024-09-07 150935](https://github.com/user-attachments/assets/ddd4ff02-9ea1-4d7d-8677-faa05adb8cf2)

##### Save result as delta table.

```
# Create sentiment column
from pyspark.sql.functions import col

sentiment_df = result.withColumn("sentiment", col("response.documents.sentiment"))

```

```
# Show result
display(sentiment_df)

```


![Screenshot 2024-09-07 151947](https://github.com/user-attachments/assets/f509a391-b172-4b13-9a8d-288d52ff3f1e)

```
#drop unwanted columns (error and response) after they are have serve their purpose.

sentiment_df_final = sentiment_df.drop("error","response")

```

```
display(sentiment_df_final)
```

![Screenshot 2024-09-07 152148](https://github.com/user-attachments/assets/8ced405a-9a80-4a47-9914-111d61f6da1b)

#### Save final result and perform incremental loading of Type 1 for new and updated records.

```
from pyspark.sql.utils import AnalysisException
from pyspark.sql import functions as F

table_name = "Election.tbl_sentiment_analysis"

# Check if t# Save result into delta table.
he table exists
def check_table_exists(spark, table_name):
    try:
        return spark.catalog.tableExists(table_name)
    except AnalysisException:
        return False

try:
    if not check_table_exists(spark, table_name):
        # Save the DataFrame as a new Delta table if it doesn't exist
        sentiment_df_final.write.format("delta").saveAsTable(table_name)
        print(f"Table {table_name} created successfully.")
    else:
        print("Table Already Exists")

        # Preprocess the source DataFrame to remove duplicates
        sentiment_df_dedup = sentiment_df_final.dropDuplicates(subset=["provider"])

        # Create or replace a temporary view for the deduplicated DataFrame
        sentiment_df_dedup.createOrReplaceTempView("vw_sentiment_df_final")

        # Perform the MERGE operation
        merge_query = f"""
            MERGE INTO {table_name} target_table
            USING vw_sentiment_df_final source_view
            ON source_view.provider = target_table.provider
            WHEN MATCHED AND (
                source_view.url <> target_table.url OR
                source_view.kind <> target_table.kind OR
                source_view.pagemap <> target_table.pagemap OR
                source_view.title <> target_table.title OR
                source_view.snippet <> target_table.snippet OR
                source_view.date_fetched <> target_table.date_fetched
            )
            THEN UPDATE SET *
            WHEN NOT MATCHED THEN INSERT *
        """
        # Execute the MERGE statement
        spark.sql(merge_query)
        print("Table merged successfully with new data.")

except Exception as e:
    print(f"An error occurred: {str(e)}")


```




E.DATA REPORTING



F.BUILDING PIPELINES



G.SETTING UP ALERTS(Using Data Activator)



H.END TO END TESTING
