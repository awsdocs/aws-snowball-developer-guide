# Using the Large Data Migration Plan<a name="understanding-data-migration-plan"></a>

After you create your large data migration plan, you can use the resulting schedule and dashboard to guide you through the rest of the migration process\. 

## Jobs ordered list<a name="job-ordered-list"></a>

Each plan displays a job ordered list\. This is empty at first\. When you start to order jobs, you can add jobs to your plan by selecting **Add job** from the **Actions** menu\. Jobs that you add here are tracked on the monitoring dashboard\. 

Similarly, you may remove the job from the job ordered list by selecting **Remove job** from the **Actions** menu\.

We recommend using the job ordering schedule provided in the plan for a smooth data migration\.

## Recommended job ordering schedule<a name="job-ordering-schedule"></a>

After you create an AWS Snow Family large migration plan, you'll see a recommended job ordering schedule for creating new jobs\. This schedule automatically adjusts based on the average data ingested per job and the average duration for completing an end\-to\-end job\. Follow this recommended schedule to simplify the decision making process for placing new job orders\.

## Monitoring dashboard<a name="monitoring-dashboard"></a>

After you add jobs to your plan, you can see metrics on the dashboard as the jobs return to AWS for ingestion\. These metrics can help you to track your progress:
+ **Data migrated to AWS** – The amount of data that's been migrated to AWS so far\.\.
+ **Average data migrated per job** – The average amount of data per job in terabytes\.
+ **Total Snow Jobs** – The number of Snowball Edge jobs ordered compared to the remaining jobs to be ordered\.
+ **Average duration for a migration job** – The average duration of a job in days\.
+ **Snow Job Status** – The number of jobs in each status\.