---
description: How to install the Data Validation Tool (DVT) locally or via Docker
---

1.  **Select Installation Method and Connections**
    Ask the user the following questions:
    *   "Do you want to install DVT locally (using a virtual environment) or using Docker?"
    *   "Which additional connection types do you need? (Oracle, SQL Server, Teradata, Snowflake, DB2, Sybase)"
    *   *Note: BigQuery, Spanner, PostgreSQL, MySQL, Hive, and Impala are included by default.*

2.  **Local Installation Path**
    *If the user selected "Local":*
    1.  **Check Prerequisites**: Verify Python 3.9+ is installed by running `python3 --version` (or `python --version` on Windows).
    2.  **Create Virtual Environment**:
        *   Run: `python3 -m venv .venv`
    3.  **Determine Pip Path**:
        *   Linux/macOS: `.venv/bin/pip`
        *   Windows: `.venv\Scripts\pip`
    4.  **Install DVT**:
        *   Upgrade pip: `<PIP_PATH> install --upgrade pip`
        *   Install package: `<PIP_PATH> install google-pso-data-validator`
    5.  **Install Output Adapters**:
        *   *If Oracle is selected*: `<PIP_PATH> install oracledb`
        *   *If Teradata is selected*: `<PIP_PATH> install teradatasql`
        *   *If Snowflake is selected*: `<PIP_PATH> install snowflake-sqlalchemy snowflake-connector-python`
        *   *If DB2 is selected*: `<PIP_PATH> install ibm_db_sa`
        *   *If Sybase is selected*: `<PIP_PATH> install sqlalchemy-sybase`
        *   *If SQL Server is selected*:
            *   **Check System Deps**: Verify `unixodbc-dev` and `msodbcsql18` are installed. If not, ask the user to install them (or offer to install on Debian/Ubuntu).
            *   Install driver: `<PIP_PATH> install pyodbc`

3.  **Docker Installation Path**
    *If the user selected "Docker":*
    1.  **Check Prerequisites**: Verify Docker is running: `docker --version`.
    2.  **Download Dockerfile and Entrypoint**:
        *   *If SQL Server is selected*: Run `curl -L https://raw.githubusercontent.com/GoogleCloudPlatform/professional-services-data-validator/develop/samples/docker/Dockerfile_sql_server_debian -o Dockerfile`
        *   *Otherwise*: Run `curl -L https://raw.githubusercontent.com/GoogleCloudPlatform/professional-services-data-validator/develop/samples/docker/Dockerfile -o Dockerfile`
        *   Run `curl -L https://raw.githubusercontent.com/GoogleCloudPlatform/professional-services-data-validator/develop/samples/docker/entrypoint.sh -o entrypoint.sh`
        *   Run `chmod +x entrypoint.sh` (Linux/macOS only)
    3.  **Prepare Dockerfile**:
        *   Fix the entrypoint path in the Dockerfile: `sed -i 's|samples/docker/entrypoint.sh|entrypoint.sh|g' Dockerfile` (or manually update if sed is unavailable).
        *   *If additional drivers ARE needed*:
            *   Append `RUN pip install ...` lines to the `Dockerfile` for each required driver (e.g., `oracledb`, `teradatasql`, `snowflake-sqlalchemy`, `ibm_db_sa`, `sqlalchemy-sybase`).
    4.  **Build Image**:
        *   Run `docker build -t data-validation .`

4.  **Verify Installation**
    *   *If Local*: Run `.venv/bin/data-validation --help` (or `.venv\Scripts\data-validation --help` on Windows)
    *   *If Docker*: Run `docker run --rm data-validation --help`
    *   Confirm the help text is displayed.
