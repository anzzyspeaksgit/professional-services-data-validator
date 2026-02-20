# Gemini CLI Agent Configuration

This project includes specialized workflows for the Gemini CLI to assist with installation and common tasks.

## Available Workflows

- **Installation**: Guide for installing DVT locally or via Docker, including driver selection.
  - Usage: Ask Gemini "How do I install DVT?" or "Run the installation workflow."
  - Location: `.agents/workflows/install_dvt.md`

## Project Context
DVT (Data Validation Tool) is an Ibis-based CLI for data comparison.
- Core: BigQuery, Spanner, Postgres, MySQL.
- Optional: Oracle, SQL Server, Teradata, Snowflake, etc.
