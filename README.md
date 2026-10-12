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
