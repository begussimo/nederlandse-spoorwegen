<div align="center">
<img src="assets/ns_nl_train.png" alt="drawing" width="400"/> <br />


# Dutch Train Stations and Disruptions Analysis 


![Badge](https://img.shields.io/badge/Jupyter-F37626.svg?&style=for-the-badge&logo=Jupyter&logoColor=white)
![Badge](https://img.shields.io/badge/JSON-43B02A?&style=for-the-badge&logo=json&logoColor=white)
![Badge](https://img.shields.io/badge/Request-%23D3FB52?&style=for-the-badge&logoColor=white)
![Badge](https://img.shields.io/badge/Snowflake-%2329B5E8?&style=for-the-badge&logo=Snowflake&logoColor=white)
![Badge](https://img.shields.io/badge/Looker_Studio-8A2TK2?style=for-the-badge&logo=Looker&logoColor=white&color=%23DE3163&cacheSeconds=%234285F4)

</div>

## :bookmark_tabs: Menu

- [Business Problem](#Business-Problem)
- [API Connection](#API-Connection)
- [Snowflake](#Snowflake)
- [Looker Studio](#Looker-Studio)
- [Folder Structure](#closedbook-results)
- [Author](#smiley_cat-author)

## Business problem


The Netherlands, celebrated for its efficient public transportation system, boasts a network of train stations connecting cities and regions seamlessly. Despite the commendable infrastructure, navigating through potential disruptions remains a significant concern for commuters. To shed light on this aspect, a comprehensive analysis has been meticulously conducted, offering insights into the operational dynamics of train stations and the impact of disruptions on the Dutch rail network.

The inception of this project faced challenges related to the acquisition of accurate datasets and the development of robust data pipelines. A strategic decision was made to gather data from authoritative sources, including the official Dutch railway portal and other relevant platforms. Employing an API integration, the data was collected to ensure a comprehensive and up-to-date dataset. Subsequently, data cleaning and transformation in Snowflake were carried out to prepare the dataset for thorough analysis and visualization in Looker Studio.

Study Overview:
This study provides a detailed examination of train stations across the Netherlands, delving into key operational aspects and disruptions that may impact commuter experiences. The analysis encompasses factors such as station facilities, and the disrupted stations and nature of disruptions. The datasets utilized in this study were procured from official railway sources, ensuring reliability and accuracy.

The architectural framework of the project is thoughtfully segmented into three main components, as follows:




- #### Data Procurement <font color='gray'> (by API connection using Python) </font>
- #### Data Preperation and Processing <font color='gray'>(by using Snowflake) </font>
- #### Data Visualization <font color='gray'>(by using Looker Studio) </font>



Here is the overall architecture flow:


![img](assets/arch.png)

# API Connection 
In this notebook, we will create a dataset of train stations and disruptions found from [NS API Portal](https://apiportal.ns.nl/) (Dutch transportation website). In order to do this, I have created some requests by using python and I have used different libraries like JSON,request and pandas in python.  

This notebook is part of my train stations data series in which I have created a dataset by using requests.

For more details on the scraping code and libraries please refer to [script.ipynb](script.ipynb)

![img](assets/ns_nl_api1.png)

# Snowflake

#### Data Warehouse and ETL with SQL

In this part, data is loaded into Snowflake and null handling and transformation steps are performed by using SQL queries. Data exploration, data preperation and data modelling and validation has been completed.

Two main tables in Snowflake Stations and Disruptions has been created as a result of the API response and these tables are :

![img](assets/stations1.png)

![img](assets/stations2.png)

![img](assets/disruptions1.png)

![img](assets/disruptions2.png)

This is created as the final table and all the data type transformations done in snowflake:


```console
CREATE OR REPLACE TABLE NL.HJ.Stations_Disruptions_NL AS
SELECT 
    ID,
    station.uiccode,
    type,
    stationcode,
    name,
    namen_lang,
    stationtype,
    registrationtime,
    releasetime,
    local,
    title,
    topic,
    isactive,
    start_time,
    end_time,
    phase_id,
    phase_label,
    impact_value,
    expectedduration_endtime,
    period,
    summaryadditionaltraveltime_maximumdurationinminutes as max_duration,
    summaryadditionaltraveltime_minimumdurationinminutes as min_duration,
    sectiontype,
    section_direction,
    consequence_section_direction,
    consequence_description,
    coordinate_lat,
    coordinate_lng
FROM dist
LEFT JOIN station
ON dist.uiccode=station.uiccode
```


Here is the final table that has been used in the final analysis:

![img](assets/join1.png)

![img](assets/join2.png)


# Looker Studio 

#### Visualizations

And as a final step Snowflake is connected with Looker Studio then the visualizations are performed.

To view the dashboard please use the [Dashboard](https://lookerstudio.google.com/u/0/reporting/26122bc4-607d-41fc-a635-94927f7d36b6/page/UuMjD) link here.

And for a quick overview please refer to the below:

![img](assets/llk1.png)
![img](assets/llk2.png)
![img](assets/llk3.png)
![img](assets/llk4.png)





## :open_file_folder: Folder Structure

```
.
├── assets                                   # Images for notebook
├── scraping.ipynb                           # Main notebook                       
└── README.md
```


## :smiley_cat: Author

- [@begussimo](https://github.com/begussimo)