# Hourly Log File Workflow

This GitHub Actions workflow automates logging the current date, time, and day to a text file (`log.txt`) every hour and clearing the file at midnight (UTC). It runs based on a scheduled cron trigger and automatically commits changes to the repository.

## Workflow Overview

### Key Features:
- **Hourly Logging**: Logs the current date, time, and day every hour, at the start of each hour (UTC).
- **Daily Log Clear**: Clears the log file at midnight (UTC) each day.
- **Automated Commits**: Logs and file-clearing actions are automatically committed to the repository.

## Workflow Configuration

This workflow is configured using two cron schedules:
- **Hourly**: Runs every hour at the start of the hour (UTC).
- **Midnight**: Runs once at midnight (UTC) to clear the log file for the new day.

### Cron Schedule:
- `0 * * * *` — Runs every hour at the top of the hour.
- `0 0 * * *` — Runs once a day at midnight to clear the log file.

### Workflow Breakdown:
1. **Hourly Log**:
    - At the start of each hour, the current date, time, and day (in UTC) are appended to the `log.txt` file.
    - The log entry is committed and pushed to the repository.

2. **Clear Log at Midnight**:
    - At midnight UTC, the contents of `log.txt` are cleared to prepare for the new day's log entries.
    - The cleared log file is committed and pushed to the repository.

## Setup

1. **Repository Access Token**:
   - The workflow uses a personal access token (`secrets.ACCESS_TOKEN`) for authentication to push changes back to the repository. Ensure this token has the necessary permissions (at least `repo` scope).

2. **GitHub Actions**:
   - The workflow uses GitHub-hosted runners (`ubuntu-latest`) and requires that the repository is set up to run GitHub Actions.

## Files Affected
- **log.txt**: This file stores the hourly logs and is cleared daily at midnight.
  
## Example Log Entries

After each hourly run, the `log.txt` file will contain entries similar to:

```
2024-12-01 01:00:00 - Monday
2024-12-01 02:00:00 - Monday
2024-12-01 03:00:00 - Monday
...
```

At midnight, the log will be cleared, and a new log will start for the next day.

## Troubleshooting

- **No Changes Error**: If no changes are detected (e.g., no new log entry to commit), the workflow will print "No changes" instead of failing.
- **Access Token**: If there are issues with authentication or pushing commits, verify that the `ACCESS_TOKEN` is correctly set in your repository secrets.

## Workflow Files

- `.github/workflows/hourly_log.yml`: The YAML configuration file for the GitHub Actions workflow.

