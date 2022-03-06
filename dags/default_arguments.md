# Default Arguments

```python
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'start_date': datetime(2022, 1, 1),
    'email': ['airflow@example.com'],
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
    'end_date': datetime(2022, 6, 1),
}

with DAG('tutorial',
          schedule_interval='@daily',  # Cron expression, here it is a preset of Airflow, @daily means once every day.
          default_args=args 
            ) as dag:
```

## Task Owner 
    
    The owner of the task.
    
## Execution & Retries

   **depends_on_past (bool)** - when set to true, task instance will run sequentially and only if the previous instance has succeeded or has been skipped.  
   **retries (int)** - the number of retries that should be performed before failing the task.  
   **retry_delay (timedelta)** - time gap between the retries.
    
## Email

   **email (string or list[str])**  
   **email_on_retry (bool)** - Indicated whether email alerts should be sent when a task is retried.  
   **email_on_failure (bool)** - Indicates whether emails alerts shoould be sent when a atask is failed.  
       
## Scheduling 

  **Schedule_interval**  
|preset	    |meaning	                                                     |  cron     |
| ----------|:------------------------------------------------------------:| ---------:|
|None	    |Don’t schedule, use for exclusively “externally triggered” DAGs |	         |
|@once	    |Schedule once and only once	                                 |           |
|@hourly	|Run once an hour at the beginning of the hour	                 | 0 * * * * |
|@daily	    |Run once a day at midnight	                                   | 0 0 * * * |
|@weekly	|Run once a week at midnight on Sunday morning	                 | 0 0 * * 0 |
|@monthly   |Run once a month at midnight of the first day of the month	   | 0 0 1 * * |
|@yearly	|Run once a year at midnight of January 1	                       | 0 0 1 1 * |
    
  **start_date (datetime)**  
            
    start_date: datetime(2019, 1, 1)
    schedule_interval: '@daily'
             
The first run will kick in at 2019-01-02 at 00:00, this run execution_date will be: 2022-01-01 00:00  
The next run will kick in at 2019-01-03 at 00:00, this run execution_date of 2022-01-02 00:00.  
So on.

![alt text](https://github.com/AnandDedha/airflow/blob/main/images/Airflow%20Start%20date.png "Start Date and Execution date")

  **end_date (datetime)**  
  
