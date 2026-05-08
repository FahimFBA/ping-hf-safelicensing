# HF Space Keep-Alive (SafeLicensing)

This repository uses **GitHub Actions** to periodically ping a Hugging Face Space and prevent it from going idle due to inactivity.


## Target Space

-> [https://fahimfba-safelicensing.hf.space/](https://fahimfba-safelicensing.hf.space/)


## Status

![Keep Alive](https://github.com/FahimFBA/ping-hf-safelicensing/actions/workflows/keep-alive.yml/badge.svg)


## Why This Exists

Free-tier Spaces on **Hugging Face** automatically pause after **48 hours** of inactivity.

This leads to:

* Cold starts
* Slow first response
* Poor user experience


## Solution

A scheduled **GitHub Action** runs every **40 hours** and sends a request to the Space — safely within the 48-hour inactivity window:

```yaml
on:
  schedule:
    - cron: "0 */40 * * *"
```


## How It Works

* GitHub Actions triggers a workflow every 40 hours
* A `curl` request is sent to the Space URL
* This resets the inactivity timer and prevents the Space from pausing


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

* Runs automatically every 40 hours
* Follows redirects (`-L`)
* Silent execution (`-s`)
* Minimal resource usage — ~18 runs/month vs ~8,928 runs/month at 5-min interval
* Works on GitHub free tier


## Notes

* GitHub Actions scheduling is not exact (may vary by a few minutes)
* This prevents **idle pause**, but not all types of shutdowns
* Hugging Face infrastructure behavior may vary


## Manual Trigger

You can manually run the workflow:

1. Go to **Actions tab**
2. Select **Keep HF Space Alive**
3. Click **Run workflow**


## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.


## Support

If you find this useful, consider giving the repo a star ⭐!
