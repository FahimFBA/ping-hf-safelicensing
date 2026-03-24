# HF Space Keep-Alive (SafeLicensing)

This repository uses **GitHub Actions** to periodically ping a Hugging Face Space and prevent it from going idle due to inactivity.


## Target Space

-> [https://fahimfba-safelicensing.hf.space/](https://fahimfba-safelicensing.hf.space/)


## Status

![Keep Alive](https://github.com/FahimFBA/ping-hf-safelicensing/actions/workflows/keep-alive.yml/badge.svg)


## Why This Exists

Free-tier Spaces on **Hugging Face** automatically go to sleep after a period of inactivity (typically ~5–15 minutes).

This leads to:

*  Cold starts
*  Slow first response
*  Poor user experience


## Solution

A scheduled **GitHub Action** runs every 5 minutes and sends a request to the Space:

```yaml
on:
  schedule:
    - cron: "*/5 * * * *"
```


## How It Works

* GitHub Actions triggers a workflow every 5 minutes
* A `curl` request is sent to the Space URL
* This keeps the Space "active" and prevents it from sleeping


## Workflow File

Location:

```
.github/workflows/keep-alive.yml
```

Core step:

```bash
curl -L -s -o /dev/null -w "%{http_code}" https://fahimfba-safelicensing.hf.space/
```


## Features

*  Runs automatically every 5 minutes
*  Follows redirects (`-L`)
*  Silent execution (`-s`)
*  Minimal resource usage
*  Works on GitHub free tier


## Notes

* GitHub Actions scheduling is not exact (may vary by a few minutes)
* This prevents **idle sleep**, but not all types of shutdowns
* Hugging Face infrastructure behavior may vary


## Manual Trigger

You can manually run the workflow:

1. Go to **Actions tab**
2. Select **Keep HF Space Alive**
3. Click **Run workflow**


## Future Improvements

* Add `/health` endpoint for lightweight checks
* Add retry/backoff logic
* Monitor response latency


## Support

If you find this useful, consider giving the repo a star (⭐)!