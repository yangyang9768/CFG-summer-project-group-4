# Code First Girls NanoDegree Data Group Project



                **Group members: Moureen Caroline Ochieng| Sophie Burroughs | Chiratidzo Matowe | Pelumi Oluboye | Chang Xu | Anna Lisowska**

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
>> - statistical data visualisation using Altair


>#### CSV and excel files
> - owid-covid-data.csv
> - clean_data.csv
> - covid-containment-and-health-index.csv
> -covid_19_clean_complete.csv


```
sns.heatmap(round(df.corr(), 1),annot=True,cmap='viridis')
sns.set(rc={'figure.figsize':(20,8)})
plt.title('Heatmap of co-relation',fontsize=15)
plt.show()
```

![Building heatmap to check correlations](/Image/Heatmap.png "Heatmap")

```
def show_seasonality(data,country):
  fig, axes = plt.subplots(1,2,figsize=(20,7), dpi= 80)
  sns.boxplot(x=data.month, y=data['new_cases'], data=data,ax=axes[0])
  sns.boxplot(x=data.month, y=data['new_deaths'], data=data)
  axes[0].set_title(f'{country} new_case seasonality', fontsize=18);
  axes[1].set_title(f'{country} new death_number seasonality', fontsize=18)
  plt.show()
show_seasonality(uk_data,'UK')
```
![UK new cases and new deaths seasonality](/Image/UKnew_cases.png "Boxplot")

#### Moving average analysis

###### Uk situation analysis

Moving average analysis please refer to:
[Wikipedia](https://en.wikipedia.org/wiki/Moving-average_model)
We want to use moving average analysis to determine the growth situation of covid.
Because covid identification was influenced by the window period and the number of people taking the test.
According to the COVID 19-SYMPTOM TIME LINES: The symptom normally appears 5 days after 10 days, and the window period is 14 days.
As a result, based on the above data, we would like to calculate the average moving of the new cases.
We create 5 day moving averages, 10 day moving averages, and 14 day moving averages to identify fluctuations.

```
from IPython.core.display import display_svg
def move_average_plot_test(data,country):

    df=data[['date','total_cases','new_cases']].copy()
    df.set_index('date', inplace=True)
    df['5 days Moving_Average new cases'] = 0
    df['5 days Moving_Average new cases'] = df['new_cases'].rolling(5).mean()
    df['10 days Moving_Average new cases'] = 0
    df['10 days Moving_Average new cases'] = df['new_cases'].rolling(10).mean()
    df['14 days Moving_Average new cases'] = 0
    df['14 days Moving_Average new cases'] = df['new_cases'].rolling(14).mean()
    df[['new_cases', '5 days Moving_Average new cases']].plot(figsize = (20, 5), alpha = 0.5)
    plt.title(f'5 days moving average in {country}')

    df[['new_cases', '10 days Moving_Average new cases']].plot(figsize = (20,5), alpha = 0.5)
    plt.title(f' 10 days moving average in {country}')

    df[['new_cases', '14 days Moving_Average new cases']].plot(figsize = (20, 5), alpha = 0.5)
    plt.title(f' 14 days moving average in {country}')
    return df
move_average_plot_test(uk_data,'UnitedKingdom')
```
![Moving average analysis](/Image/Timeseries.png "Timeseries")

```
fig,ax = plt.subplots()
ax.plot(df_final["restriction"],
        color="red",
        marker="o")
# set x-axis label
ax.set_xlabel("Date", fontsize = 14)
# set y-axis label
ax.set_ylabel("Restriction Levels",
              color="red",
              fontsize=14)
ax2=ax.twinx()
ax2.plot(df_final["total_deaths"],color="blue",marker="o")
ax2.set_ylabel("Total deaths",color="blue",fontsize=14)
plt.title('Restriction levels and total deaths in the United Kingdom')
plt.show()
```
![Restriction against total deaths](/Image/Restriction.png "Restriction")

```
data_three2 = pd.read_csv('final_COVID-19-clean-complete.csv', parse_dates=['Date'])
SE = data_three2[data_three2['Country/Region'] == 'Sweden']

base = alt.Chart(SE).mark_bar().encode(
    x='monthdate(Date):O',
).properties(
    width=500
)
yellow = alt.value('#ffce03')
base.encode(y = 'Confirmed').properties(title = 'Total Confirmed')|base.encode(y='Deaths', color = yellow).properties(title = 'Total Deaths')
yellow = alt.value('#ffce03')
base.encode(y = 'New cases').properties(title = 'Daily New Cases')|base.encode(y='New deaths', color = yellow).properties(title = 'Daily New Deaths')
```
![New cases vs new deaths in Sweden](/Image/visualization-2.png "New cases vs new deaths")

```
alt.Chart(selected_countries).mark_circle().encode(
    x='monthdate(Date):O',
    y='Country/Region',
    color='Country/Region',
    size=alt.Size('New deaths:Q',
        scale=alt.Scale(range=[0, 1000]),
        legend=alt.Legend(title='Daily new deaths')
    )
).properties(
    width=800,
    height=300
)
```
![Daily new deaths for the 3 countries](/Image/visualization-5.png "Daily new deaths")

## Data sources:


[Our World in Data](https://ourworldindata.org)

[COVID-19 Dataset](https://www.kaggle.com/datasets/imdevskp/corona-virus-report)

[UK Government Coronavirus lockdowns](https://www.instituteforgovernment.org.uk/charts/uk-government-coronavirus-lockdowns)

[COVID-19 in Australia](https://en.wikipedia.org/wiki/COVID-19_pandemic_in_Australia)

[Swedish Government response to COVID-19](https://en.wikipedia.org/wiki/Swedish_government_response_to_the_COVID-19_pandemic)

[Time from symptom onset until death](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/928729/S0803_CO-CIN_-_Time_from_symptom_onset_until_death.pdf)