# Young Lives Database Project

## Overview
The purpose of this project is to design and implement a database system using the Young Lives dataset. This README file provides an overview of the SQL statements used to create the database and tables, along with various queries and stored procedures for data analysis.

## Table of Contents
- [Database Creation](#database-creation)
- [Table Creation](#table-creation)
- [Data Queries and Procedures](#data-queries-and-procedures)
- [Additional Tasks](#additional-tasks)

## Database Creation

### Create Database for Young Lives
```sql
USE master;
GO

CREATE DATABASE YoungLives;
```

## Table Creation

### Create Tables Using T-SQL

#### Vietnam Table
```sql
USE YoungLives;
GO

CREATE TABLE [dbo].[Vietnam] (
      NOT NULL,
    [round] [float] NOT NULL,
    [stunting] [float] NULL,
    [thinness] [float] NULL,
    [literate] [float] NULL,
    [underweight] [float] NULL,
      NULL,
      NULL,
    [yc] [float] NULL,
    [chdisability] [nvarchar] NULL,
    [entype] [float] NULL,
    [typesite] [float] NULL,
    [bmi] [decimal](5,2) NULL
);
```

#### Peru Table
```sql
USE YoungLives;
GO

CREATE TABLE [dbo].[Peru] (
      NOT NULL,
    [round] [float] NOT NULL,
    [stunting] [float] NULL,
    [thinness] [float] NULL,
    [literate] [float] NULL,
    [underweight] [float] NULL,
      NULL,
      NULL,
    [yc] [float] NULL,
    [chdisability] [nvarchar] NULL,
    [entype] [float] NULL,
    [typesite] [float] NULL
);
```

#### India Table
```sql
USE YoungLives;
GO

CREATE TABLE [dbo].[India] (
      NOT NULL,
    [round] [float] NOT NULL,
    [stunting] [float] NULL,
    [thinness] [float] NULL,
    [literate] [float] NULL,
    [underweight] [float] NULL,
      NULL,
      NULL,
    [yc] [float] NULL,
    [chdisability] [nvarchar] NULL,
    [entype] [float] NULL,
    [typesite] [float] NULL
);
```

#### Ethiopia Table
```sql
USE YoungLives;
GO

CREATE TABLE [dbo].[Ethiopia] (
      NOT NULL,
    [round] [float] NOT NULL,
    [stunting] [float] NULL,
    [thinness] [float] NULL,
    [literate] [float] NULL,
    [underweight] [float] NULL,
      NULL,
      NULL,
    [yc] [float] NULL,
    [chdisability] [nvarchar] NULL,
    [entype] [float] NULL,
    [typesite] [float] NULL
);
```

## Data Queries and Procedures

### Summarizing Data Reports of India

#### Measuring Children in India Underweight
```sql
USE YoungLives;
GO

SELECT round,
    COUNT(CASE WHEN underweight = 0 THEN 1 END) AS Not_Underweight,
    COUNT(CASE WHEN underweight = 1 THEN 1 END) AS Moderately_underweight,
    COUNT(CASE WHEN underweight = 2 THEN 1 END) AS Severely_underweight  
FROM [dbo].[India]
GROUP BY round
ORDER BY round;
```

#### Measuring Literacy in India
```sql
CREATE PROCEDURE literacy @yc FLOAT
AS 
BEGIN
    SELECT
        COUNT(CASE WHEN literate = 0 THEN 1 END) AS Illiterate,
        COUNT(CASE WHEN literate = 1 THEN 1 END) AS Literate,
        round
    FROM [dbo].[India]
    WHERE yc = @yc
    GROUP BY round;
END;

EXEC literacy @yc = 0;
EXEC literacy @yc = 1;
```

### Measuring Ethiopia Disability
```sql
CREATE PROCEDURE entype_disability @entype FLOAT
AS 
BEGIN
    SELECT
        round,
        COUNT(CASE WHEN chdisability = 0 THEN 1 END) AS nondisability,
        COUNT(CASE WHEN chdisability = 1 THEN 1 END) AS disability
    FROM [dbo].[Ethiopia]
    WHERE entype = @entype
    GROUP BY round
    ORDER BY round;
END;

EXEC entype_disability @entype = 1;
```

### Measuring Peru Smoking
```sql
CREATE PROCEDURE Chsmoking @chsmoke FLOAT
AS 
BEGIN
    SELECT
        round,
        COUNT(CASE WHEN typesite = 2 THEN 1 END) AS rural,
        COUNT(CASE WHEN typesite = 1 THEN 1 END) AS urban 
    FROM [dbo].[Peru]
    WHERE chsmoke = @chsmoke
    GROUP BY round
    ORDER BY round;
END;

EXEC Chsmoking @chsmoke = 1;
```

### Measuring Peru Child Drinking
```sql
CREATE PROCEDURE Chalcoholism @chalcohol FLOAT
AS 
BEGIN
    SELECT
        round,
        COUNT(CASE WHEN typesite = 2 THEN 1 END) AS rural,
        COUNT(CASE WHEN typesite = 1 THEN 1 END) AS urban 
    FROM [dbo].[Peru]
    WHERE chalcohol = @chalcohol
    GROUP BY round
    ORDER BY round;
END;

EXEC Chalcoholism @chalcohol = 0;  -- no
EXEC Chalcoholism @chalcohol = 1;  -- yes
```

### Measuring Vietnam Stunting
```sql
CREATE PROCEDURE Chstunt @yc FLOAT
AS 
BEGIN
    SELECT
        round,
        COUNT(CASE WHEN stunting = 0 THEN 1 END) AS not_stunted,
        COUNT(CASE WHEN stunting = 1 THEN 1 END) AS moderately_stunted,
        COUNT(CASE WHEN stunting = 2 THEN 1 END) AS severely_stunted
    FROM [dbo].[Vietnam]
    WHERE yc = @yc
    GROUP BY round
    ORDER BY round;
END;

EXEC Chstunt @yc = 0;  -- older
EXEC Chstunt @yc = 1;  -- younger
```

## Additional Tasks

### Create Database for Vietnam Survey 2016-17
```sql
USE master;
GO 

CREATE DATABASE VietnamSurvey_2016_17;
```

### Create Tables for Vietnam Wave 1 and Wave 2

#### Vietnam Wave 1 Table
```sql
USE VietnamSurvey_2016_17;
GO

CREATE TABLE [dbo].[Vietnam_W1] (
      NOT NULL,
    [SchoolID] [float] NOT NULL,
    [ClassID] [float] NOT NULL,
    [StudentId] [float] NOT NULL,
    [Province] [float] NOT NULL,
    [DistrictCode] [float] NOT NULL,
    [Locality] [float] NOT NULL,
    [Gender] [float] NULL,
    [Age] [float] NULL,
    [Ethnicity] [float] NULL,
    [Absent_days] [float] NOT NULL,
    [STDDINT] [datetime2] NULL, 
    [STDLNGHM] [float] NULL,
    [STRPTCL1] [float] NULL,
    [STRPTCL6] [float] NULL,
    [STRPTCL10] [float] NULL,
      NULL,
    [ENG_RAWSCORE] [float] NULL,
      NULL,
    [MATH_RAWSCORE] [float] NULL,
    [GRLENRL] [float] NULL,
    [BOYENRL] [float] NULL,
    [TGRLENRL] [float] NULL,
    [TBOYENRL] [float] NULL,
    [HTDINT] [date] NULL,
    [HTSEX] [float] NULL,
    [HTEXCTCH] [float] NULL
);
```

#### Vietnam Wave 2 Table
```sql
CREATE TABLE [dbo].[Vietnam_W2] (
      NOT NULL,
    [SchoolID] [float] NOT NULL,
    [ClassID] [float] NOT NULL,
    [StudentId] [float] NOT NULL,
    [Province] [float] NOT NULL,
    [DistrictCode] [float] NOT NULL,
    [Locality] [float] NOT NULL,
    [Gender] [float] NULL,
    [Age] [float] NULL,
    [Ethnicity] [float] NULL,
    [Absent_days] [float] NOT NULL,
    [STDDINT] [datetime2] NULL, 
    [STDLNGHM] [float] NULL,
    [STRPTCL1]

 [float] NULL,
    [STRPTCL6] [float] NULL,
    [STRPTCL10] [float] NULL,
      NULL,
    [ENG_RAWSCORE] [float] NULL,
      NULL,
    [MATH_RAWSCORE] [float] NULL,
    [GRLENRL] [float] NULL,
    [BOYENRL] [float] NULL,
    [TGRLENRL] [float] NULL,
    [TBOYENRL] [float] NULL,
    [HTDINT] [date] NULL,
    [HTSEX] [float] NULL,
    [HTEXCTCH] [float] NULL
);
```

## Data Analysis and Visualization

### Tasks
1. **Vietnam Analysis of Absenteeism**:
   - Analyze the absenteeism rates in the Vietnam 2016-17 survey.
2. **Vietnam Analysis of Student Performance**:
   - Compare student performance in English and Math across different provinces.
3. **Additional Analysis**:
   - Further data analysis as per the project requirements, focusing on various child development metrics.

### Visualization Tools
Use tools like Power BI, Tableau, or Python libraries (e.g., Matplotlib, Seaborn) to visualize the data.

## Conclusion
This database system provides a comprehensive structure for storing and analyzing the Young Lives dataset. The SQL procedures and queries enable in-depth analysis of various child development metrics across different countries and waves of the survey.
