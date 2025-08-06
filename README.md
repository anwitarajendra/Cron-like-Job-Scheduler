# Cron-like Job Scheduler (Mini Cron Daemon)

This is a system-level Python project that mimics the basic functionality of the Unix `cron` scheduler. It allows users to schedule Python commands either at fixed intervals or daily at specific times.

## Features

- Schedule jobs with either interval (in minutes) or specific daily time
- Persistent storage of jobs using SQLite
- Background daemon logic using Python's `threading` and `time` modules
- Supports dynamic addition and removal of jobs

## How It Works

1. Users add job commands into the SQLite database with scheduling details.
2. The Python script runs an infinite loop that:
   - Fetches jobs from the database
   - Executes them at the scheduled time
   - Updates their `last_run` timestamp
3. Supports both interval-based and time-based job execution.

## Database Schema (SQLite)

Table: `jobs`

| Column         | Type     | Description                             |
|----------------|----------|-----------------------------------------|
| id             | INTEGER  | Primary key, auto-incremented           |
| command        | TEXT     | Python code to execute                  |
| schedule_type  | TEXT     | Either 'interval' or 'daily'           |
| interval_minutes | INTEGER | Time interval in minutes (if interval)  |
| daily_time     | TEXT     | Time string in HH:MM format (if daily)  |
| last_run       | TEXT     | Timestamp of last execution             |

## How to Run

1. Open the notebook in Google Colab.
2. Define your jobs directly or through database insertion code.
3. Run the scheduler cell and keep the notebook running in the background.

## Example Usage

```python
# Insert a job that runs every 10 minutes
insert_job("print('Scheduled task executed')", "interval", interval_minutes=10)

# Insert a job that runs daily at 14:30
insert_job("print('Daily task running')", "daily", daily_time='14:30')
```

## Notes

- This version runs without a user interface.
- SQLite handles persistent job storage.
- Logging can be added to capture job outputs if needed.

