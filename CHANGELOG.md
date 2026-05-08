# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

## [1.1.0] - 2026-05-09

### Changed

- Reduced ping frequency from every 5 minutes (`*/5 * * * *`) to every 40 hours (`0 */40 * * *`) to align with Hugging Face's 48-hour inactivity window — cuts monthly workflow runs from ~8,928 to ~18

## [1.0.0] - 2026-03-24

### Added

- Initial keep-alive workflow that pings the SafeLicensing HF Space on a schedule
- `curl` step with redirect follow, silent mode, and HTTP status output
- `workflow_dispatch` trigger for manual runs
- README documentation
