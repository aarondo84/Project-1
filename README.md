# Project-1


Problem set 1
-ID top 50 highest-paying data analyst positions that are available remotely
-focus on job postings with specific salaries(removing nulls)
SELECT 
	job_id,
    job_title, 
    job_location,
    job_schedule_type,
    salary_year_avg, 
    job_posted_date,
    name as company_name 
    
FROM job_postings_fact
left join company_dim on job_postings_fact.company_id=company_dim.company_id

where
	job_title_short= 'Data Analyst' and 
    job_location = 'Anywhere' and 
    salary_year_avg is not null
order by
	salary_year_avg DESC
limit 50


Problem set 2

Question: What are the top-paying data analyst jobs, and what skills are required?** 

- Identify the top 50 highest-paying Data Analyst jobs and the specific skills required for these roles.
- Filters for roles with specified salaries that are remote
- Why? It provides a detailed look at which high-paying jobs demand certain skills, helping job seekers understand which skills to develop that align with top salaries

with top_paying_jobs as(
SELECT 
	job_id,
    job_title, 
    job_location,
    job_schedule_type,
    salary_year_avg, 
    job_posted_date,
    name as company_name 
    
FROM job_postings_fact
left join company_dim on job_postings_fact.company_id=company_dim.company_id

where
	job_title_short= 'Data Analyst' and 
    job_location = 'Anywhere' and 
    salary_year_avg is not null
order by
	salary_year_avg DESC
limit 50
)

select
top_paying_jobs.*,
skills
from top_paying_jobs
inner join skills_job_dim on top_paying_jobs.job_id= skills_job_dim.job_id
inner join skills_dim on skills_job_dim.skill_id= skills_dim.skill_id
order by
	salary_year_avg DESC 

**problem 2 insights: sql is leading in skills needed for most data analyst roles followed by python and data visualization tools such as tableau.
SQL: Appears in 40 of 45 jobs (89%), 
Python: Appears in 19 jobs (42%).
Tableau: Appears in 17 jobs (38%).
Excel: Appears in 14 jobs (31%).
R: Appears in 13 jobs (29%).



<img width="2180" height="1574" alt="data_analyst_skills_visualization" src="https://github.com/user-attachments/assets/dbf7bdf5-937c-4f53-9cf1-d788e0be7f74" />


Problem set 3

Question: What are the top skills based on salary?

- Look at the average salary associated with each skill for Data Analyst positions.
- Focuses on roles with specified salaries, regardless of location.
- Why? It reveals how different skills impact salary levels for Data Analysts and helps identify the most financially rewarding skills to acquire or improve.

select
skills,
round(avg(salary_year_avg),0)as avg_salary
from job_postings_fact
join skills_job_dim on job_postings_fact.job_id = skills_job_dim.job_id
join skills_dim on skills_job_dim.skill_id = skills_dim.skill_id
where
	job_title_short = 'Data Analyst' and 
    salary_year_avg is not null
    -- and job_work_from_home = true
group by
	skills
order by 
	avg_salary desc
limit 25


**problem 3 insights:The data shows that specialized technical skills, such as Solidity, Couchbase, and Golang, are associated with higher average salaries. However, these results may reflect specialized or senior-level positions rather than typical data analyst jobs.

Rather than choosing skills based on salary alone, it is important to consider job demand, salary potential, and career goals. Based on the previous dataset, SQL, Python, Excel, and Tableau or Power BI are strong skills to prioritize.
