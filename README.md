# Code First Girls NanoDegree Data Group Project



                **Group members: MoureenCaroline Ochieng| Sophie Burroughs | Chiratidzo Matowe | Pelumi Oluboye | Chang Xu | Anna Lisowska**

## This repository contains the report and script:


## Time Series Analysis of Covid Impact on the UK, SWEDEN and AUSTRALIA

Coronavirus disease (COVID-19) is a virus-borne infection caused by the SARS-CoV-2 virus.
A new coronavirus known as 2019-nCoV was discovered in Wuhan, China's Hubei province capital.
People got pneumonia for no apparent reason, and existing vaccines and treatments were ineffective.
The virus has been linked to human-to-human transmission.
In mid-January 2020, the transmission rate (rate of infection) appeared to be increasing.


> #### Jupyter Notebook
> CFGFinalProject.ipynb
>
> 1. Data cleaning and wrangling
>  focusing on removing erroneous data from your data set.
>  Data-wrangling focusing on changing the data format by translating "raw" data into a more usable form.
>> - fixing or removing incorrect data.
>> - duplicate, or incomplete data within a dataset.
>
> 2. Data exploration
> the first step of data analysis used to explore and visualise data to uncover insights from the start or identify areas or patterns to dig into more.
>> - Time series analysis
>> - Bi-variate Analysis also known as linear regression
>> - statistical data visualisation using Altair


>#### CSV and excel files
> - owid-covid-data.csv
> - clean_data.csv
> - covid-containment-and-health-index.csv
> -covid_19_clean_complete.csv


`sns.heatmap(round(df.corr(), 1),annot=True,cmap='viridis')
sns.set(rc={'figure.figsize':(20,8)})
plt.title('Heatmap of co-relation',fontsize=15)
plt.show()`

![Building heatmap to check correlations](/Image/Heatmap.png "Heatmap")

## Data sources:


[Our World in Data](https://ourworldindata.org)

[COVID-19 Dataset](https://www.kaggle.com/datasets/imdevskp/corona-virus-report)
