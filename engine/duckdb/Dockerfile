FROM python:3.9-slim

# Install DuckDB
RUN pip install duckdb

# Create directory for DuckDB files
WORKDIR /duckdb

# Keep container running
CMD ["tail", "-f", "/dev/null"]