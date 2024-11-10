# Monitoring and Metrics Setup for Microsoft SQL On-Premise Using InfluxDB

## Introduction

This document provides detailed instructions on setting up a monitoring and metrics system for Microsoft SQL on-premise using InfluxDB. The setup includes steps for installing and configuring InfluxDB, collecting and visualizing metrics from Microsoft SQL, and troubleshooting tips and best practices.

## Steps for Installing and Configuring InfluxDB

1. **Install InfluxDB**: Follow the official InfluxDB installation guide for your operating system. You can find the installation instructions [here](https://docs.influxdata.com/influxdb/v2.0/get-started/).

2. **Configure InfluxDB**:
   - Create a new database for storing metrics:
     ```sh
     influx
     CREATE DATABASE sql_metrics
     exit
     ```

## Collecting Metrics from Microsoft SQL

1. **Install Telegraf**: Telegraf is an agent for collecting and reporting metrics. You can find the installation instructions [here](https://docs.influxdata.com/telegraf/v1.19/introduction/installation/).

2. **Configure Telegraf**:
   - Edit the Telegraf configuration file to collect metrics from Microsoft SQL Server and send them to InfluxDB. Below is an example configuration:
     ```toml
     [[inputs.sqlserver]]
       servers = ["Server=localhost;Port=1433;User Id=sa;Password=your_password;"]
       query_version = 2
       azuredb = false
       query_scheduled_jobs = false
       include_query = ["PerformanceCounters", "WaitStatsCategorized", "DatabaseIO", "ServerProperties", "MemoryClerk"]

     [[outputs.influxdb]]
       urls = ["http://localhost:8086"]
       database = "sql_metrics"
     ```

## Visualizing Metrics

1. **Install Grafana**: Grafana is a visualization tool for displaying metrics. You can find the installation instructions [here](https://grafana.com/docs/grafana/latest/installation/).

2. **Configure Grafana**:
   - Add InfluxDB as a data source in Grafana.
   - Create dashboards to visualize the metrics collected from Microsoft SQL Server.

## Troubleshooting Tips and Best Practices

- Ensure that InfluxDB, Telegraf, and Grafana services are running.
- Check the logs of InfluxDB, Telegraf, and Grafana for any errors.
- Verify the connection strings and credentials used in the configuration files.
- Regularly update InfluxDB, Telegraf, and Grafana to the latest versions to benefit from new features and bug fixes.
