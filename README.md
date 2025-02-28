1.  **`Select * From PortfolioProject..CovidDeaths Where continent is not null order by 3,4`**:
    * Retrieves all columns from the `CovidDeaths` table, excluding rows where the continent is null, and orders the results by the third and fourth columns.

2.  **`Select Location, date, total_cases, new_cases, total_deaths, population From PortfolioProject..CovidDeaths Where continent is not null order by 1,2`**:
    * Selects specific columns (location, date, cases, deaths, population) from `CovidDeaths`, excluding null continents, and orders by location and date.

3.  **`Select Location, date, total_cases, total_deaths, (total_deaths/total_cases)*100 as DeathPercentage From PortfolioProject..CovidDeaths Where location like '%states%' and continent is not null order by 1,2`**:
    * Calculates the death percentage (deaths/cases * 100) for locations containing "states", excluding null continents, and orders by location and date.

4.  **`Select Location, date, Population, total_cases, (total_cases/population)*100 as PercentPopulationInfected From PortfolioProject..CovidDeaths order by 1,2`**:
    * Calculates the percentage of the population infected with COVID-19 (cases/population * 100) and orders by location and date.

5.  **`Select Location, Population, MAX(total_cases) as HighestInfectionCount, Max((total_cases/population))*100 as PercentPopulationInfected From PortfolioProject..CovidDeaths Group by Location, Population order by PercentPopulationInfected desc`**:
    * Determines the highest infection count and the maximum percentage of the population infected for each country, ordered by the percentage in descending order.

6.  **`Select Location, MAX(cast(Total_deaths as int)) as TotalDeathCount From PortfolioProject..CovidDeaths Where continent is not null Group by Location order by TotalDeathCount desc`**:
    * Finds the highest total death count for each country, excluding null continents, and orders by death count in descending order.

7.  **`Select continent, MAX(cast(Total_deaths as int)) as TotalDeathCount From PortfolioProject..CovidDeaths Where continent is not null Group by continent order by TotalDeathCount desc`**:
    * Finds the highest total death count for each continent, and orders by death count in descending order.

8.  **`Select SUM(new_cases) as total_cases, SUM(cast(new_deaths as int)) as total_deaths, SUM(cast(new_deaths as int))/SUM(New_Cases)*100 as DeathPercentage From PortfolioProject..CovidDeaths where continent is not null order by 1,2`**:
    * Calculates global total cases, total deaths, and the overall death percentage, excluding null continents, and orders by total cases and total deaths.

9.  **`Select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations, SUM(CONVERT(int,vac.new_vaccinations)) OVER (Partition by dea.Location Order by dea.location, dea.Date) as RollingPeopleVaccinated From PortfolioProject..CovidDeaths dea Join PortfolioProject..CovidVaccinations vac On dea.location = vac.location and dea.date = vac.date where dea.continent is not null order by 2,3`**:
    * Joins `CovidDeaths` and `CovidVaccinations` tables to show rolling vaccination counts by location and date.

10. **`With PopvsVac (...) Select *, (RollingPeopleVaccinated/Population)*100 From PopvsVac`**:
    * Uses a CTE to calculate the rolling percentage of vaccinated people relative to the population.

11. **`DROP Table if exists #PercentPopulationVaccinated ... Select *, (RollingPeopleVaccinated/Population)*100 From #PercentPopulationVaccinated`**:
    * Uses a temporary table to calculate and display the rolling percentage of vaccinated people relative to the population.

12. **`Create View PercentPopulationVaccinated as ...`**:
    * Creates a view to store the results of the rolling percentage of vaccinated people relative to the population query for later use.
