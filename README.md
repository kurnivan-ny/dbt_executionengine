# dbt_executionengine

This repo a comprehensive data engineering environment setup using Docker Compose, featuring multiple services including Apache Spark, Trino, DuckDB, PostgreSQL, and dbt integrations.

## Project Overview
```
├── dbt/                              # Data transformation layer
│   ├── dbt_spark/                    # Spark-specific DBT configuration
│   │   └── logs/                     # Spark DBT execution logs
│   │   └── models/                   # Spark-specific data models
│   │   └── dbt_project.yml          # DBT project settings for Spark
│   │   └── profiles.yml             # Connection profiles for Spark
│   ├── duckdb/                      # DuckDB-specific DBT configuration
│   │   └── logs/                    # DuckDB DBT execution logs
│   │   └── models/                  # DuckDB-specific data models
│   │   └── tmp/                     # Temporary files for DuckDB
│   │   └── dbt_project.yml         # DBT project settings for DuckDB
│   │   └── profiles.yml            # Connection profiles for DuckDB
│   └── trino/                       # Trino-specific DBT configuration
│       └── logs/                    # Trino DBT execution logs
│       └── models/                  # Trino-specific data models
│       └── dbt_project.yml         # DBT project settings for Trino
│       └── profiles.yml            # Connection profiles for Trino
├── engine/                          # Data processing engines
│   ├── trino/                      # Trino engine configuration
│   │   └── etc/                    # Trino server configuration files
│   ├── postgres/                   # PostgreSQL engine configuration
│   │   └── data/                   # PostgreSQL data directory
│   └── duckdb/                     # DuckDB engine configuration
│       └── data/                   # DuckDB data directory
│       └── Dockerfile              # DuckDB container configuration
└── docker-compose.yml              # Service orchestration configuration
```

## Directory Structure Explanation

### DBT Layer (`/dbt`)
The DBT directory contains all data transformation logic and configurations for different data warehouses:

- **dbt_spark/**
  - Purpose: Manages Spark-specific data transformations
  - Key files:
    - `models/`: Contains SQL transformations for Spark
    - `dbt_project.yml`: Configures DBT project settings
    - `profiles.yml`: Defines connection settings

- **duckdb/**
  - Purpose: Handles DuckDB-specific transformations
  - Key files:
    - `models/`: Contains SQL transformations for DuckDB
    - `tmp/`: Stores temporary processing files
    - Configuration files for project and connections

- **trino/**
  - Purpose: Manages Trino-specific transformations
  - Contains similar structure to other DBT projects
  - Specialized for Trino's SQL dialect

### Engine Layer (`/engine`)
Contains configurations and data storage for different processing engines:

- **trino/**
  - Purpose: Trino server configuration
  - `etc/`: Contains server-specific settings

- **postgres/**
  - Purpose: PostgreSQL database setup
  - `data/`: Stores PostgreSQL data files

- **duckdb/**
  - Purpose: DuckDB engine setup
  - `data/`: Stores DuckDB data files
  - `Dockerfile`: Defines DuckDB container configuration

### Root Level
- `docker-compose.yml`: Orchestrates all services and their interactions

## Usage Guidelines

1. **DBT Projects**
   - Each DBT project is isolated by engine type
   - Models should be placed in appropriate engine-specific directories
   - Logs are automatically generated in respective `/logs` directories

2. **Engine Configuration**
   - Engine-specific settings should be maintained in respective directories
   - Data persistence is managed through mounted volumes in `data/` directories

3. **Development Workflow**
   - Use docker-compose for managing the entire stack
   - Each engine can be developed and tested independently
   - DBT models can be developed in isolation for each target platform

## Getting Started

1. Clone the repository
2. Navigate to the project root
3. Run `docker-compose up` to start all services
4. Access different engines through their respective ports
5. Execute DBT models using appropriate project directories

## Notes

- Each engine maintains its own data directory for persistence
- DBT models are separated by engine to handle syntax differences
- Logs are maintained separately for each DBT project
- Configuration files are isolated to prevent conflicts
