-- How many people use python, SQL, Excel, and Power BI in thei current roles? 
SELECT count(ID) AS number_of_python_sql_excel_BI_users
FROM data_challenge_for_newbies
WHERE Tools like '%Python%'
AND Tools like '%SQL%'
AND Tools like '%Excel%'
AND Tools like '%PowerBI%';

-- IDENIFTY THE MOST POPULAR TOOLS BY EXPERIENCE LEVEL
SELECT 
	Experience,
    SUM(CASE WHEN Tools LIKE '%Excel%' THEN 1 ELSE 0 END) AS Excel_users,
    SUM(CASE WHEN Tools LIKE '%SQL%' THEN 1 ELSE 0 END) AS SQL_users,
    SUM(CASE WHEN Tools LIKE '%PowerBI%' THEN 1 ELSE 0 END) AS PowerBI_users,
    SUM(CASE WHEN Tools LIKE '%Python%' THEN 1 ELSE 0 END) AS Python_users,
    SUM(CASE WHEN Tools LIKE '%R%' THEN 1 ELSE 0 END) AS R_users
-- used conditional logic to count the number of users for each tool and found the total for each time the tool appeared
FROM data_challenge_for_newbies
GROUP BY Experience;

-- RETRIEVE ROWS WHERE RESPONDENTS REPORT "COMMUNICATION SKILLS" AS A CHALLENGE AND HAVE LESS THAN A YEAR EXPERIENCE
-- CREATE A COLUMN THAT CATEGORIZES RESPONDENTS BASED ON THEIR YEARS OF EXPERIENCE -- 
SELECT 
	ID,
    Challenge,
    Experience
FROM data_challenge_for_newbies
WHERE Challenge like '%communication skills%'
AND Experience = 'Less than a year';

-- RETRIEVE ROWS WHERE RESPONDENTS REPORT "COMMUNICATION SKILLS" AS A CHALLENGE AND HAVE LESS THAN A YEAR EXPERIENCE

SELECT 
	ID,
    Valuable_skill,
    Experience
FROM data_challenge_for_newbies
WHERE Valuable_skill like '%communication% %Skills%'
AND Experience = 'Less than a year';

-- CREATE A COLUMN THAT CATEGORIZES RESPONDENTS BASED ON THEIR YEARS OF EXPERIENCE -- 
SELECT
  ID,
  Experience,
  Tools,
  CASE
    WHEN Experience = 'Less than a year' THEN 'Entry level'
    WHEN Experience = '1 - 3 years' THEN 'Junior'
    WHEN Experience = '3 - 5 years' THEN 'Mid-level'
    WHEN Experience = '5+ years' THEN 'Senior'
  END AS Level_of_experience
FROM data_challenge_for_newbies;

-- Find industries with at least 5 respondents who believe it offers the most opportunity --
WITH popular_industries AS (  -- utilizing CTE to create a temporary result set 
SELECT 
	ID,
	SUM(CASE WHEN Industry LIKE '%Finance%' THEN 1 ELSE 0 END) AS Finance,
	SUM(CASE WHEN Industry LIKE '%Technology%' THEN 1 ELSE 0 END) AS Technology,
	SUM(CASE WHEN Industry LIKE '%Healthcare%' THEN 1 ELSE 0 END) AS Healthcare,
	SUM(CASE WHEN Industry LIKE '%Retail%' THEN 1 ELSE 0 END) AS Retail,
	SUM(CASE WHEN Industry LIKE '%Government%' THEN 1 ELSE 0 END) AS Government
-- used conditional logic to know the perception of respondents about each industry
FROM data_challenge_for_newbies
GROUP BY ID
)
SELECT
	SUM(Finance) AS total_finance,
    SUM(Technology) AS total_technology,   -- calculating the total entry for each industry  
    SUM(Healthcare) AS total_Healthcare,
    SUM(Retail) AS total_Retail,
    SUM(Government) AS total_Government
FROM popular_industries;

-- Find the respondents who are very satisfied with there roles, the tools they use and their years of experience
SELECT 
	ID,
    Tools,
    Experience
FROM data_challenge_for_newbies
WHERE Satisfaction like '%Very satisfied%';   -- used the WHERE clause to filter for only respondents who 
											  -- are very satisfied

-- Find the key challenges impacting job struggles across education levels and industry preferences 
SELECT
	Challenge,
    Education,
    Industry     -- relevant columns to know the challenges, education level
FROM 
	data_challenge_for_newbies
WHERE Job_struggle <> 'NO'  -- filter for respondents with job struggles 
ORDER BY Education, Industry;  -- to sort the result set in ascending order, considering Education level first



-- Determine if there's a significant correlation between education level and job struggle
SELECT
	Job_struggle,
	SUM(CASE WHEN Education LIKE '%Bachelor%' THEN 1 ELSE 0 END) AS Bachelors,
    SUM(CASE WHEN Education LIKE '%Self%' THEN 1 ELSE 0 END) AS Self_taught, 
    SUM(CASE WHEN Education LIKE '%Masters%' THEN 1 ELSE 0 END) AS Masters,
    SUM(CASE WHEN Education LIKE '%Boot%' THEN 1 ELSE 0 END) AS Bootcamp,
    SUM(CASE WHEN Education LIKE '%High%' THEN 1 ELSE 0 END) AS High_school -- Conditional logic to get the sum --
    -- of number of entries for each educational level 
FROM data_challenge_for_newbies
GROUP BY Job_struggle;   -- grouping the result set by the Job_struggle to know how the level of education affects job_struggle
