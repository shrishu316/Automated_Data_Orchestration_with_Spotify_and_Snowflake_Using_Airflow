# Automated Data Orchestration with Spotify and Snowflake Using Airflow

This project is an ETL (Extract, Transform, Load) pipeline built to fetch and analyze data from Spotify
using Apache Airflow, Docker, Amazon EC2, S3, Snowpipe, Snowflake, and Looker Studio.

## Table of Contents
1. [Project Overview](#project-overview)
2. [Architecture](#architecture)
3. [Technologies Used](#technologies-used)
4. [Setup and Prerequisites](#setup-and-prerequisites)
5. [Data Flow and Pipeline](#data-flow-and-pipeline)
6. [Running the ETL Pipeline](#running-the-etl-pipeline)
7. [Data Visualization](#data-visualization)
8. [Future Improvements](#future-improvements)
9. [Contributors](#contributors)
10. [License](#license)

---

## Project Overview
The goal of this ETL project is to extract data from Spotify, process and store it in Snowflake, and visualize it through Looker Studio. 
This setup provides insights into Spotify data for analysis, reporting, and dashboarding.

## Architecture

![Spotify_architecture(2) drawio](https://github.com/user-attachments/assets/6f1d904a-2f58-4d47-b8ad-4126b47328b3)

## Technologies Used

- **[Spotify API](https://developer.spotify.com/documentation/web-api/)** - Fetches Spotify data.
- **[Docker](https://www.docker.com/)** - Container management and deployment.
- **[Apache Airflow](https://airflow.apache.org/)** - Workflow orchestration and scheduling.
- **[Amazon EC2](https://aws.amazon.com/ec2/)** - Cloud-based VM for hosting the ETL environment.
- **[Amazon S3](https://aws.amazon.com/s3/)** - Storage for raw data files.
- **[Snowpipe](https://docs.snowflake.com/en/user-guide/data-load-snowpipe)** - Continuous data ingestion tool.
- **[Snowflake](https://www.snowflake.com/)** - Cloud-based data warehouse.
- **[Looker Studio](https://lookerstudio.google.com/)** - Data visualization platform.

## Setup and Prerequisites

### Prerequisites

- **Spotify API Credentials** - Create a Spotify Developer account to obtain `Client ID` and `Client Secret`.
- **AWS Account** - Required for EC2 and S3 access.
- **Snowflake Account** - Set up your Snowflake warehouse and database.
- **Looker Studio Account** - To create visualizations.

### Project Setup

1. **Clone the Repository**
    ```bash
    git clone https://github.com/shrishu316/Automated_Data_Orchestration_with_Spotify_and_Snowflake_Using_Airflow.git
    cd Automated_Data_Orchestration_with_Spotify_and_Snowflake_Using_Airflow
    ```

2. **Environment Variables**

    Create an `.env` file to store sensitive credentials:
    ```bash
    SPOTIFY_CLIENT_ID=your_spotify_client_id
    SPOTIFY_CLIENT_SECRET=your_spotify_client_secret
    AWS_ACCESS_KEY_ID=your_aws_access_key_id
    AWS_SECRET_ACCESS_KEY=your_aws_secret_access_key
    SNOWFLAKE_USER=your_snowflake_user
    SNOWFLAKE_PASSWORD=your_snowflake_password
    SNOWFLAKE_ACCOUNT=your_snowflake_account
    ```

3. **Docker Compose**

    Docker Compose is used to build the Docker containers for Airflow and other dependencies:
    ```bash
    docker-compose up -d
    ```

4. **Set Up Airflow DAGs**

    Place your ETL DAGs under the `dags/` directory. Airflow will automatically detect and register them.

5. **Configure Snowpipe**

    Use Snowflake's UI or CLI to set up Snowpipe to listen for new data on the specified S3 bucket.

## Data Flow and Pipeline

### ETL Pipeline Steps

1. **Extract** - Spotify data is fetched via the Spotify API using Airflow.
2. **Load & Transform S3** - The raw data is saved as JSON in S3 and transformed to CSV files in an Amazon S3 bucket.
3. **Load to Snowflake** - Snowpipe is configured to automatically ingest new data from S3 into Snowflake.
4. **Data Modeling** - Data is modeled in Snowflake tables for easier querying.
5. **Visualization in Looker Studio** - Connect Looker Studio to Snowflake and build visualizations and dashboards.

### Airflow DAG
![Screenshot From 2024-11-01 12-42-31](https://github.com/user-attachments/assets/efbcb46b-0438-4075-ab26-ac5019925460)

- The Airflow DAG orchestrates the ETL process, running tasks on a schedule.
- Key tasks in the DAG:
  - `extract_data`: Fetches data from Spotify.
  - `load_to_s3`: Saves data to S3.
  - `snowflake_load`: Triggers Snowpipe to load data from S3 to Snowflake.

## Running the ETL Pipeline

1. **Start the Docker Containers**

    Ensure Docker containers for Airflow and related services are running:
    ```bash
    docker-compose up
    ```

2. **Access Apache Airflow UI**

    Airflow UI can be accessed at `http://localhost:8080`. Here, you can trigger and monitor DAG runs.

3. **Monitor Snowpipe**

    Snowflake's `LOAD_HISTORY` table can be queried to monitor Snowpipe activity.

## Data Visualization
![Screenshot_20241101_094104](https://github.com/user-attachments/assets/8682d817-1dd9-4e42-8c16-3df10021a365)
### Looker Studio Setup

1. Connect Looker Studio to Snowflake by configuring a data source connection.
2. Build custom visualizations, reports, and dashboards to analyze Spotify data.

## Future Improvements

- **Enhanced Data Transformation** - More sophisticated transformations on Spotify data.
- **Real-Time Data Ingestion** - Explore Kafka or Kinesis for near real-time data ingestion.
- **Automated Alerts** - Add notifications for ETL pipeline failures via Slack or email.
- **Data Quality Checks** - Implement data validation checks within the Airflow DAG.

## Contributors

- **Shubham** - [GitHub](https://github.com/shrishu316)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
