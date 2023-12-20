# Unveiling COVID-19 Realities: A Comprehensive MSSQL Subquery Analytics Portfolio on Global Deaths
Data Analytics Portfolio with Basic, Intermediate and advanced MSSQL Subqueries for 4 Large Data Sets
Data Analytics Portfolio with Basic, Intermediate and advanced MSSQL Subqueries

The Data Exploration involves the use of : 
WHERE Statement, 
GROUP BY, 
INNER AND OUTER JOINS, 
UNIONS, UNION OPERATORS,  
CASE STATEMENT, 
HAVING CLAUSE,  
UPDATING AND DELETING DATA, 
ALIASING, 
PARTITION BY, 
CTE (Common Table Expression), 
TEMP Table, 
STRING FUNCTIONS, 
STORED PROCEDURES, 
DATA CLEANING
And Others


SELECT TOP (1000) [EmployeeID]
      ,[JobTitle]
      ,[Salary]
  FROM [TutorialDB].[dbo].[EmployeeSalary]


Insert rows into table 'Customers'
INSERT INTO dbo.EmployeeSalary (
   [EmployeeID],
   [JobTitle],
   [salary]

)
VALUES
   (1001, 'Salesman', 45000),
(1002, 'Receptionist', 36000),
(1003, 'Salesman', 63000),
(1004, 'Accountant', 47000),
(1005, 'HR', 50000),
(1006, 'Regional Manager', 65000),
(1007, 'Supplier Relations', 41000),
(1008, 'Salesman', 48000),
(1009, 'Accountant', 42000)
GO


ALTER DATABASE TutorialDB COLLATE SQL_Latin1_General_CP1_CI_AS

SELECT *
FROM TutorialDB.dbo.EmployeeDemographics
 JOIN TutorialDB.dbo.EmployeeSalary

ON EmployeeDemographics.EmployeeID = EmployeeSalary.EmployeeID


SELECT *
FROM TutorialDB.dbo.EmployeeDemographics

SELECT *                                    
FROM TutorialDB.dbo.EmployeeSalary



SELECT a.*,
 b.* from TutorialDB.dbo.EmployeeDemographics a, 
 TutorialDB.dbo.EmployeeSalary b 
where a.EmployeeID = b.EmployeeID



SELECT *
FROM TutorialDB.dbo.EmployeeDemographics
 LEFT OUTER JOIN TutorialDB.dbo.EmployeeSalary

ON EmployeeDemographics.EmployeeID = EmployeeSalary.EmployeeID

SELECT EmployeeDemographics
.EmployeeID, FirstName,  LastName, Age, JobTitle, Salary
FROM EmployeeDemographics
LEFT OUTER JOIN EmployeeSalary
ON EmployeeDemographics.EmployeeID = EmployeeSalary.EmployeeID

SELECT TOP 5 EmployeeDemographics.EmployeeID, FirstName, LastName, Salary
FROM EmployeeDemographics
Inner JOIN EmployeeSalary
ON EmployeeDemographics.EmployeeID = EmployeeSalary.EmployeeID
WHERE FirstName <> 'Michael'
ORDER BY Salary DESC



SELECT JobTitle, AVG(Salary) AS 'Average Salary'
FROM EmployeeDemographics
INNER JOIN EmployeeSalary
ON EmployeeDemographics.EmployeeID = EmployeeSalary.EmployeeID
WHERE JobTitle = 'salesman'
GROUP BY JobTitle


SELECT *
FROM EmployeeSalary






CREATE TABLE [dbo].[WhareHouseEmployeeDemographics](
[EmployeeID] INT NOT NULL PRIMARY KEY,
[FirstName] VARCHAR(50) NOT NULL,
[LastName] VARCHAR(50) NOT NULL,
[Age] INT NOT NULL,
[Gender] VARCHAR(50) NOT NULL
)


SELECT *
FROM EmployeeDemographics


 Insert rows into table 'Customers'
INSERT INTO TutorialDB.dbo.WhareHouseEmployeeDemographics (
   [EmployeeID],
   [FirstName],
    [LastName],
     [Age],
   [Gender]

)
VALUES

(1013, 'Darryl', 'Philbin', 24, 'Male'),
(1050, 'Roy', 'Anderson', 31, 'Male'),
(1051, 'Hidetoshi', 'Hasagawa', 40, 'Male'),
(1052, 'Val', 'Johnson', 31, 'Female')

GO






INSERT INTO TutorialDB.dbo.EmployeeDemographics (
   [EmployeeID],
    [LastName],
   [FirstName],
    [Age],
   [Gender]

)
VALUES
(1011, 'Ryan', 'Howard', 26, 'Male'),
(1012, 'Holly', 'Flax', 30, 'Female'),
(1013, 'Darryl', 'Philbin', 25, 'Female')
GO


SELECT *
 FROM TutorialDB.dbo.EmployeeDemographics
UNION ALL

 SELECT *
 FROM TutorialDB.DBO.WhareHouseEmployeeDemographics



-- CASE STATEMENT -----
SELECT FirstName, LastName, Age,
CASE
WHEN Age > 30 THEN 'Old'
WHEN AGE BETWEEN 27 AND 30 THEN 'Young'
WHEN AGE = 25 THEN 'Child'
    ELSE 'Baby'
END

FROM TutorialDB.dbo.EmployeeDemographics
WHERE Age IS NOT NULL
ORDER BY AGE





- NEW NOTES STARTS FROM HERE ---

REAL LIFE SCENERIO: WHAT WILL THERE SALARY BE, AFTER WE CALCULATE THERE RAISE (SALARY INCREAMENT)

SELECT  FirstName, LastName, JobTitle, Salary,
CASE
WHEN JobTitle = 'salesman' THEN Salary + (Salary * 0.10)
WHEN JobTitle = 'Accountant' THEN salary + (salary * 05)
WHEN JobTitle = 'Regional Manager' THEN salary + (Salary * 0.03)
ELSE Salary + (salary * 0.02)

END AS 'Salary - Increament'
FROM TutorialDB.dbo.EmployeeDemographics
JOIN TutorialDB.dbo.EmployeeSalary
ON EmployeeDemographics.EmployeeID = EmployeeSalary.EmployeeID








- HAVING CLAUSE ----
SELECT JobTitle, COUNT(JobTitle) AS COUNT
FROM TutorialDB.DBO.EmployeeDemographics
JOIN TutorialDB.dbo.EmployeeSalary
ON EmployeeDemographics.EmployeeID =EmployeeSalary.EmployeeID
GROUP BY JobTitle 
HAVING COUNT(JobTitle) > 1



--- HAVING CLAUSE EXAMPLE 2 ----
SELECT JobTitle, AVG(salary) AS COUNT
FROM TutorialDB.DBO.EmployeeDemographics
JOIN TutorialDB.dbo.EmployeeSalary
ON EmployeeDemographics.EmployeeID =EmployeeSalary.EmployeeID
GROUP BY JobTitle 
HAVING AVG(Salary) > 45000
ORDER BY AVG(Salary)




-------- UPDATING AND DELETING DATA -----
SELECT *
FROM TutorialDB.dbo.EmployeeDemographics

UPDATE TutorialDB.dbo.EmployeeDemographics
SET Age = 45
WHERE  EmployeeID = 1001 AND LastName ='Halpert'


------- UPDATING AND DELETING DATA EXAMPLE 2-----

UPDATE TutorialDB.dbo.EmployeeDemographics
SET FirstName = 'Alex', LastName = 'Fatogun'
WHERE EmployeeID =1005 AND Gender = 'Male' 






-- DELETE STATEMENT ---


    DELETE FROM TutorialDB.dbo.EmployeeDemographics
    WHERE EmployeeID = 1009


    --- OR USE SAFE MODE ----



    SELECT *
    FROM TutorialDB.dbo.EmployeeDemographics
    WHERE EmployeeID = 1008







--- Aliasing -----

SELECT  FirstName + ' ' + LastName AS 'FULL-NAME'
FROM [TutorialDB].[dbo].[EmployeeDemographics]

- ALIAS FOR TABLE NAME EXAMPLE 2 --

SELECT Demo.EmployeeID, Sal.salary
FROM [TutorialDB].[dbo].[EmployeeDemographics] AS Demo
JOIN [TutorialDB].[dbo].[EmployeeSalary] AS Sal
ON Demo.EmployeeID = Sal.EmployeeID

 ---- OR, EXAMPLE 3 -------
 
SELECT Demo.EmployeeID, Sal.salary,
FROM [TutorialDB].[dbo].[EmployeeDemographics] AS Demo
JOIN [TutorialDB].[dbo].[EmployeeSalary] AS Sal
ON Demo.EmployeeID = Sal.EmployeeID

----- OR EXAMPLE 4 ----

SELECT a.EmployeeID, a.FirstName, a.LastName, b.JobTitle, b.salary
FROM [TutorialDB].[dbo].[EmployeeDemographics] a 
LEFT JOIN [TutorialDB].[dbo].[EmployeeSalary] b 
ON a.EmployeeID = b.EmployeeID
LEFT JOIN [TutorialDB].[dbo].[WhareHouseEmployeeDemographics] c 
ON a.EmployeeID = c.EmployeeID


SELECT *
FROM TutorialDB.DBO.WhareHouseEmployeeDemographics



---- INTERMEDIATE SQL (PARTITION BY) -----
SELECT FirstName, LastName, Gender, Salary,
COUNT(Gender) OVER (PARTITION BY Gender) AS TotalGender
from TutorialDB.dbo.EmployeeDemographics Dem
JOIN TutorialDB.dbo.EmployeeSalary AS Sal
ON Dem.EmployeeID = Sal.EmployeeID


---- INTERMEDIATE SQL (PARTITION BY) -----
SELECT FirstName, LastName, Gender, Salary,
COUNT(Gender) OVER (PARTITION BY Gender) AS TotalGender
from TutorialDB.dbo.EmployeeDemographics Dem
JOIN TutorialDB.dbo.EmployeeSalary AS Sal
ON Dem.EmployeeID = Sal.EmployeeID



-- ---- -- ADVANCED MSSQL TUTORIAL (COMMON TABLE EXPRESSION CTE) -- -- -- 


WITH CTE_Employee as 
(SELECT TOP 6 FirstName, LastName, Gender, Salary,
COUNT (Gender) OVER (PARTITION BY Gender) AS TotalGender,
AVG (Salary) OVER (PARTITION BY Gender) AS AVGSalary
FROM TutorialDB.dbo.EmployeeDemographics AS DEMO 
JOIN TutorialDB.dbo.EmployeeSalary AS SALARY 
ON DEMO.EmployeeID = SALARY.EmployeeID
WHERE Salary > '30000'
)
SELECT *
FROM CTE_Employee


   ----- TEMP TABLES ------
   
CREATE TABLE #TEMP_Employee (
    EmployeeID INT,
    JobTitle VARCHAR(100),
        Salary INT,
)


SELECT *
FROM #TEMP_Employee

INSERT INTO #TEMP_Employee
VALUES(
    '1001', 'Financial Manager', '60000'
)

INSERT INTO #TEMP_Employee
SELECT *
FROM TutorialDB.dbo.EmployeeSalary

SELECT *
FROM #TEMP_Employee

UPDATE TutorialDB.DBO.#TEMP_Employee
SET EmployeeID = 1000
WHERE JobTitle = 'Financial Manager' AND Salary = 60000



CREATE TABLE #TEMP_Employee (
    LastName VARCHAR(50),
    FirstName VARCHAR(50),
    Age INT,
    Gender VARCHAR(50),
    JobTitle VARCHAR(50),
    Salary int,
    EmployeeID INT
)

INSERT INTO #TEMP_Employee3
VALUES( 'Fatogun', 'Alex', 15, 'Male', 'Data Scientist', 46000, 999)

DROP TABLE IF EXISTS TutorialDB.dbo.TEMP_Employee3;


SELECT *
from #TEMP_Employee3

INSERT INTO #TEMP_Employee3
SELECT JobTitle,
COUNT(JobTitle),   AVG(Age), AVG(Salary)
FROM TutorialDB.DBO.EmployeeDemographics AS emp
JOIN TutorialDB.DBO.EmployeeSalary AS sal
ON emp.EmployeeID = sal.EmployeeID
GROUP BY JobTitle

SELECT *
FROM #TEMP_Employee3

SELECT *
FROM EmployeeDemographics

DROP TABLE #TEMP_Employee3 RESTRICT


IF OBJECT_ID('dbo.#TEMP_Employee3 ','U') IS NOT NULL
DROP TABLE dbo.#TEMP_Employee3;




DROP TABLE IF EXISTS #TEMP_Employee4
CREATE TABLE #TEMP_Employee4 (
    JobTitle VARCHAR(50),
    EmployeePerJob int,
    AvgAge INT,
    AVGSalary INT,

)

INSERT INTO #TEMP_Employee4
SELECT JobTitle, COUNT(JobTitle), AVG(Age), AVG(Salary)
FROM TutorialDB.DBO.EmployeeDemographics AS emp
JOIN TutorialDB.DBO.EmployeeSalary AS sal
ON emp.EmployeeID = sal.EmployeeID
GROUP BY JobTitle


SELECT *
FROM #TEMP_Employee4





---- STRING FUNCTIONS ---TRIM, LTRIM, RTRIM, REPLACE, SUBSTRING, UPPER, LOWER ----

CREATE TABLE EmployeeErrors  
(EmployeeID VARCHAR(50),
FirstName VARCHAR(50),
LastName VARCHAR(50)
)

INSERT INTO EmployeeErrors
VALUES
('1001 ', 'Jimbo', 'Halbert' ),
('  1002', 'Pamela', 'Beasely'),
('1005', 'Toby', 'Flenderson - Fired')

SELECT *
FROM EmployeeErrors

--- Using Trim. LTrim, RTrim

SELECT EmployeeID, TRIM (EmployeeID) AS IDTRIM
FROM EmployeeErrors

SELECT EmployeeID, LTRIM (EmployeeID) AS IDTRIM
FROM EmployeeErrors

SELECT EmployeeID, RTRIM (EmployeeID) AS IDTRIM
FROM EmployeeErrors




----- using replace -----

SELECT LastName, REPLACE(LastName,'- Fired', '') AS LastNameFixed
FROM EmployeeErrors



---- Using Substring ----


SELECT Err.FirstName, SUBSTRING(ERR.FirstName, 1, 3), DEMO.FirstName, SUBSTRING(DEMO.FirstName, 1,3)
FROM EmployeeErrors AS Err
JOIN EmployeeDemographics as DEMO
ON SUBSTRING(ERR.FirstName, 1, 3) = SUBSTRING(DEMO.FirstName, 1,3)





---- Using UPPPER AND lower  CASE--

SELECT FirstName, LOWER(FirstName)
FROM EmployeeErrors


SELECT FirstName, UPPER(FirstName)
FROM EmployeeErrors



-- STORED PROCEDURES ----

CREATE PROCEDURE TEST
AS
SELECT *
FROM EmployeeDemographics

EXEC TEST




-- subqueries (in the Select, From, and Where Statement ) -----

SELECT *
FROM EmployeeSalary

--- SUBQUERY IN SELECT ---

SELECT EmployeeID,  Salary, (SELECT AVG(Salary) FROM EmployeeSalary) AS 'All-Average-Salary'
FROM EmployeeSalary



--- HOW TO DO IT WITH PARTITION BY ---

SELECT EmployeeID, Salary, AVG(Salary) OVER()  AS 'All-Average-Salary'

FROM EmployeeSalary


--- WHY GROUP BY DOESNT WORK ---

SELECT EmployeeID, Salary, AVG(Salary) OVER()  AS 'All-Average-Salary'

FROM EmployeeSalary
GROUP BY EmployeeID, Salary
ORDER BY 1,2



-- SUBQUERY IN FROM STATEMENT --

SELECT a.EmployeeID, a.JobTitle, AllAverageSalary
FROM (SELECT EmployeeID,JobTitle, Salary, AVG(Salary) OVER () AS AllAverageSalary
FROM EmployeeSalary) a




SUBQUERY IN WHERE STATEMENT --

SELECT EmployeeID, JobTitle, Salary
    FROM EmployeeSalary
    WHERE EmployeeID IN (
    SELECT EmployeeID
    FROM EmployeeDemographics 
    WHERE AGE > 30)





-----  HOW TO ALTER DATABASE NAME ---


USE master;  
GO  
ALTER DATABASE NMyPortfolioProject SET SINGLE_USER WITH ROLLBACK IMMEDIATE;
GO
ALTER DATABASE NMyPortfolioProject MODIFY NAME = MyPortfolioProject;
GO  
ALTER DATABASE MyPortfolioProject SET MULTI_USER;




   — —— HOW TO CREATE DATA BASE———


USE master;
GO

IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'MyPortfolioProject'
      )
   CREATE DATABASE [NMyPortfolioProject];
GO

IF SERVERPROPERTY('ProductVersion') > '12'
   ALTER DATABASE [MyPortfolioProject] SET QUERY_STORE = ON;
GO



ALTER TABLE 

EXEC sp_rename 'Covid-Vacinations (1) (1)', 'Covid-Vacination’;


-- IF YOU EXPERINCE LINES OR ERRORS LATTER THEN:
In azure data studio press "cmd+shift+p" and type
 "intellisense", then you will see an option to
 refresh intellisense cache.




———  COVID 19 PORTFOLIO ——

--  SELECT * 
--  FROM MyPortfolioProject.dbo.[CovidDeaths-1]




SELECT *
FROM [Covid19-Vacination] 
ORDER BY 3, 4


-- Select Data that we are goin to be using
SELECT location, date, total_cases, new_cases, total_deaths, population
FROM MyPortfolioProject.dbo.[CovidDeaths-1]
order by 1, 2

-- Looking at the Total Cases versus Total Deaths
-- SELECT location, date, total_cases, total_deaths, 
-- (total_cases/total_deaths) AS DeathPercentage
-- FROM MyPortfolioProject.dbo.[CovidDeaths-1]
-- ORDER BY  1, 2


-- SELECT location, date, total_cases,total_deaths, 
-- (CONVERT(float, total_deaths) / NULLIF(CONVERT(float, total_cases), 0)) * 100 AS Deathpercentage
-- FROM MyPortfolioProject.dbo.[CovidDeaths-1]
-- ORDER BY  1, 2

SELECT location, date, total_cases,total_deaths, 
(CONVERT(float, total_deaths) / NULLIF(CONVERT(float, total_cases), 0)) * 100 AS Deathpercentage
FROM MyPortfolioProject.dbo.[CovidDeaths-1]
ORDER BY  1, 2




SELECT *
FROM [Covid19-Vacination] 
ORDER BY 3, 4


-- Select Data that we are goin to be using
SELECT location, date, total_cases, new_cases, total_deaths, population
FROM MyPortfolioProject.dbo.[CovidDeaths-1]
order by 1, 2

Looking at the Total Cases versus Total Deaths
SELECT location, date, total_cases, total_deaths, 
(total_deaths/total_cases) * 100 AS DeathPercentage
FROM MyPortfolioProject.dbo.[CovidDeaths-1]
-- ORDER BY  1, 2

SELECT *
FROM [CovidDeaths-DateChange]


SELECT location, date, total_cases,total_deaths, 
(CONVERT(float, total_deaths) / NULLIF(CONVERT(float, total_cases), 0)) * 100 AS Deathpercentage
FROM MyPortfolioProject.dbo.[CovidDeaths-DateChange]
ORDER BY  1, 2


-- Looking at Total Cases vs Total Deaths
-- It Shows the Likelihood of dying if you contract covid 19 in your Country

SELECT location, date, total_cases,total_deaths, 
(CONVERT(float, total_deaths) / NULLIF(CONVERT(float, total_cases), 0)) * 100 AS Deathpercentage
FROM MyPortfolioProject.dbo.[CovidDeaths-DateChange]
WHERE location like '%states%'
ORDER BY  1, 2


--- Looking at the Total Cases vs Population
--- Shows what percentage of population got covid

SELECT location, date, total_cases, population, 
(CONVERT(float, total_cases) / NULLIF(CONVERT(float, population), 0)) * 100 AS PercentPopulationInfection
FROM MyPortfolioProject.dbo.[CovidDeaths-DateChange]
WHERE location like '%states%'
ORDER BY  1, 2

---- OR ----
SELECT location, date,population,  total_cases, 
(total_cases/CONVERT(float, population)) * 100 AS DeathPercentage
FROM MyPortfolioProject.dbo.[CovidDeaths-1]
WHERE continent is not null
WHERE location like '%states%'
ORDER BY  1, 2

- Looking at Countries with the Highest Infection Rate compared to Population --

SELECT top population, MAX(total_cases) AS HighestInfectionCount,     
MAX(CONVERT( FLOAT, total_cases)/NULLIF(CONVERT(FLOAT, population),0 ))*100 AS PercentPopulationInfection
FROM MyPortfolioProject.dbo.[CovidDeaths-DateChange]
WHERE continent is not null
GROUP BY location,population
ORDER BY PercentPopulationInfection desc


-- --- for TOP 3 COUNTRIES WITH High Percent Population infection --
SELECT top 3 location, population, MAX(total_cases) AS HighestInfectionCount,     
MAX(CONVERT( FLOAT, total_cases)/NULLIF(CONVERT(FLOAT, population),0 ))*100 AS PercentPopulationInfection
FROM MyPortfolioProject.dbo.[CovidDeaths-DateChange]
WHERE continent is not null
GROUP BY location,population
ORDER BY PercentPopulationInfection desc


SELECT top 3 location, population, MAX(total_cases) AS HighestInfectionCount,     
MAX(CONVERT( FLOAT, total_cases)/NULLIF(CONVERT(FLOAT, population),0 ))*100 AS PercentPopulationInfection
FROM MyPortfolioProject.dbo.[CovidDeaths-DateChange]
GROUP BY location,population
ORDER BY PercentPopulationInfection desc



--  Showing Countries with the Highest death Count (Total Number Of Covid 19 Deaths)

SELECT location, MAX(CAST(total_deaths AS INT)) AS TotalDeathCount
FROM MyPortfolioProject.dbo.[CovidDeaths-DateChange]
WHERE continent is not null
GROUP BY [location]
ORDER BY TotalDeathCount DESC


---- lets break things down by continent---

SELECT location, MAX(CAST(total_deaths AS INT)) AS TOTAL_DEATHS_IN_CONTINENTS
FROM MyPortfolioProject.dbo.[CovidDeaths-DateChange]
WHERE CONTINENT IS NULL
GROUP BY LOCATION
ORDER BY TOTAL_DEATHS_IN_CONTINENTS DESC


--- SHOWING Continent with the highest death count population ---

SELECT continent, MAX(CAST(total_deaths AS INT)) AS TOTAL_DEATHS_IN_CONTINENTS
FROM MyPortfolioProject.dbo.[CovidDeaths-DateChange]
WHERE CONTINENT IS NOT NULL
GROUP BY continent
ORDER BY TOTAL_DEATHS_IN_CONTINENTS DESC


——— USING #TEMP— TABLE ----—

WITH POPVSVAC (continent, location, Date, population, RollingPeopleVacinated, new_vaccinations)

AS (

SELECT DEA.continent, DEA.location, DEA.date, DEA.population, VAC.new_vaccinations,
SUM(CONVERT(INT, VAC.new_vaccinations)) OVER (PARTITION BY DEA.location ORDER BY DEA.location, DEA.date) AS RollingPeopleVacinated
FROM MyPortfolioProject.dbo.[CovidDeaths-1] AS DEA

JOIN MyPortfolioProject.dbo.[Covid19-Vacination] AS VAC
ON  DEA.[location] = VAC.[location]
AND DEA.date = VAC.date

WHERE DEA.location IS NOT NULL

-- ORDER BY 2,3
)

SELECT * 
FROM POPVSVAC

—  ——— CURRENTLY VACINATED IN REGARDS TO POPULATION OF A COUNTRY —


WITH POPVSVAC (continent, location, Date, population, RollingPeopleVacinated, new_vaccinations)

AS (

SELECT DEA.continent, DEA.location, DEA.date, DEA.population, VAC.new_vaccinations,
SUM(CONVERT(INT, VAC.new_vaccinations)) OVER (PARTITION BY DEA.location ORDER BY DEA.location, DEA.date) AS RollingPeopleVacinated
FROM MyPortfolioProject.dbo.[CovidDeaths-1] AS DEA

JOIN MyPortfolioProject.dbo.[Covid19-Vacination] AS VAC
ON  DEA.[location] = VAC.[location]
AND DEA.date = VAC.date

WHERE DEA.location IS NOT NULL

)
SELECT *, (CONVERT(FLOAT, RollingPeopleVacinated)/CONVERT(FLOAT, population )) * 100 

FROM POPVSVAC







---- TEMP TABLE ----

DROP TABLE IF EXISTS #PercentPopulationVacinated
CREATE TABLE #PercentPopulationVacinated
(
    continent NVARCHAR(255),
    location NVARCHAR(255),
    Date DATETIME,
    population numeric,
    new_vacinations numeric,
    RollingPeopleVacinated numeric
)
INSERT INTO #PercentPopulationVacinated
SELECT DEA.continent, DEA.location, DEA.date, DEA.population, VAC.new_vaccinations,
SUM(CONVERT(INT, VAC.new_vaccinations)) OVER (PARTITION BY DEA.location ORDER BY DEA.location, DEA.date) AS RollingPeopleVacinated
FROM MyPortfolioProject.dbo.[CovidDeaths-1] AS DEA

JOIN MyPortfolioProject.dbo.[Covid19-Vacination] AS VAC
ON  DEA.[location] = VAC.[location]
AND DEA.date = VAC.date

WHERE DEA.location IS NOT NULL

SELECT *, (CONVERT(FLOAT, RollingPeopleVacinated)/CONVERT(FLOAT, population )) * 100 

FROM #PercentPopulationVacinated



----------- CREATING VIEW TO STORE DATA FOR LATER VISUALIZATION -----------

CREATE VIEW  PercentPopulationVacinated AS
SELECT DEA.continent, DEA.location, DEA.date, DEA.population, VAC.new_vaccinations,
SUM(CONVERT(INT, VAC.new_vaccinations)) OVER (PARTITION BY DEA.location ORDER BY DEA.location, DEA.date) AS RollingPeopleVacinated
FROM MyPortfolioProject.dbo.[CovidDeaths-1] AS DEA

JOIN MyPortfolioProject.dbo.[Covid19-Vacination] AS VAC
ON  DEA.[location] = VAC.[location]
AND DEA.date = VAC.date

WHERE DEA.location IS NOT NULL

-- SELECT *, (CONVERT(FLOAT, RollingPeopleVacinated)/CONVERT(FLOAT, population )) * 100 

-- FROM #PercentPopulationVacinated


-----  WE CAN NOW QUERRY FROM THIS  ----

SELECT *
FROM PercentPopulationVacinated

———————  ——— MICROSOFT SQL (LEVEL 2)---------------
