# dataanalysiscapstone

Analyzing two sources of data, CovidDeaths and CovidVaccinations by creating tables
and importing the .xlsx into Microsoft SSMS.

Using commands to view tables
Select* from Covid..CovidDeaths
Select* from Covid..CovidVaccinations 

--Selecting only the Data to be used--

Select Location, date, total_cases, new_cases, total_deaths
from Covid..CovidDeaths

--viewing death rate (total_deaths/total_cases)

Select Location, date, total_cases, total_deaths, (total_deaths/total_cases) as death_ratio

--Convert to percentage  (total_deaths/total_cases)*100

Select Location, date, total_cases, total_deaths, (total_deaths/total_cases)*100 
as death_percentage
from Covid..CovidDeaths

--Filtering for chosen location (say India)

Select Location, date, total_cases, total_deaths, (total_deaths/total_cases)

from Covid..CovidDeaths

Where location = 'India';

--total cases vs population (how many people were infected from Covid in India on each day)

Select Location, date, population, total_cases, (total_cases/population) as infected_percentage

from Covid..CovidDeaths

Where location = 'India';

--looking at countries with highest infection rate compared to population

Select location, population, MAX(total_cases) as Highest_infection_count, MAX((total_cases/population))*100 as PercentPopulationInfected

from Covid..CovidDeaths

Group by location, population

ORDER BY PercentPopulationInfected desc;

(Andorra	77265	13232	17.1254772536077)

--showing countries with Highest Death Count per Population

Select location, MAX(cast(total_deaths as int)) as TotalDeathCount

from Covid..CovidDeaths

where continent is not null

Group by location

ORDER BY TotalDeathCount desc;
(United States	576232)

-----LOOKING AT STATS CONTINENT-WISE-----

Select continent, MAX(cast(total_deaths as int)) as TotalDeathCount

from Covid..CovidDeaths

where continent is not null

Group by continent

ORDER BY TotalDeathCount desc;

North America	576232
South America	403781
Asia	211853
Europe	127775
Africa	54350
Oceania	910

-----LOOKING AT STATS LOCATION (COUNTRY) WISE-----

Select location, MAX(cast(total_deaths as int)) as TotalDeathCount

from Covid..CovidDeaths

where continent is not null

Group by location

ORDER BY TotalDeathCount desc;


-----LOOKING AT STATS CONTINENT-WISE-----  (change is not null to is null to view all continents)

Select location, MAX(cast(total_deaths as int)) as TotalDeathCount

from Covid..CovidDeaths

where continent is null

Group by location

ORDER BY TotalDeathCount desc;

-----Showing continents with the highest death count per population-----

Select continent, MAX(cast(total_deaths as int)) as TotalDeathCount

from Covid..CovidDeaths

where continent is not null

Group by continent

ORDER BY TotalDeathCount desc;

----Joining other table, CovidVaccinations to CovidDeaths




