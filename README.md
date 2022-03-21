# Covid-Project-Dashboard
Data Visualization project on covid-19 worldwide.
Prepare a dashboard to show the covid-19 situation worldwide, and comparing it with other countries

## Tool used
- SQL
- Tableau

## Process
### SQL
1) Found the gobal numbers of total cases, total deaths and death percentage
```sql
Select
    sum(new_cases) as total_cases,
    sum(new_deaths) as total_deaths,
    sum(new_deaths)/sum(new_cases)*100 as death_percentage
from
    `project-for-portfolio.covid_project.covid_deaths`
where
    continent is not null
order by
    1, 2;
```
2) I took some data out as they were not needed and wanted to stay consistent
```sql
select
    location,
    sum(new_deaths) as total_death_count
from
    `project-for-portfolio.covid_project.covid_deaths`
where
    continent is null
    and
    location not in('World', 'European Union', 'International', 'Upper middle income', 'High income', 'Lower middle income', 'Low income')
group by
    location
order by
    total_death_count desc;
```
3) looking at countries with hightest infection rate compared to population
```sql
select
    location, 
    population,
    max(total_cases) as highest_infection_count,
    max((total_cases/population))*100 as percent_of_population_infected
from
    `project-for-portfolio.covid_project.covid_deaths`
group by
    location,
    population
order by
    4 desc;
```
4) Looked for total cases vs population and show what percentage of population got infected.
```sql
select
    location,
    population,
    date,
    max(total_cases) as highest_infection_count,
    max(total_cases/population)*100 as percent_of_population_infected
from
    `project-for-portfolio.covid_project.covid_deaths`
where
    location = "India"
group by
    location,
    population,
    date
order by
    5 desc;
```
- After running queries I export these data into excel and saved files separately
- Imported those excel files into tableau
### Tableau

1) Created a table of global data which shows total cases, total deaths and death percentage

![Global Numbers](https://user-images.githubusercontent.com/92750711/159223965-ad4291c4-300e-4568-95b8-94fecaf8e94d.png)


2) Created a bar graph for different continent which shows the total deaths per continent

![Bar Graph](https://user-images.githubusercontent.com/92750711/159221044-b2d71b91-d390-4d5d-8a26-b28686280f31.png)

3) Created a map visualization which shows us the percentage of population got infected in each country

![Map Visualization](https://user-images.githubusercontent.com/92750711/159221019-310fc58c-4093-4709-ae00-833712ce7bc1.png)

4) created line graph visualization which shows the percentage of population infected very month

![Line graph](https://user-images.githubusercontent.com/92750711/159221035-6e4fcde8-208f-4952-9aec-0cdd352e83fd.png)

5) created a dashboard to represent the whole.

![Covid-Dashboard](https://user-images.githubusercontent.com/92750711/159222956-16c169d0-b0eb-46ea-8be3-ac6f3bda8ca4.png)
