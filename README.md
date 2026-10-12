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

- Identify the top 10 highest-paying Data Analyst jobs and the specific skills required for these roles.
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
