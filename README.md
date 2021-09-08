# insights-results-aggregator-exporter

[![GoDoc](https://godoc.org/github.com/RedHatInsights/insights-results-aggregator-exporter?status.svg)](https://godoc.org/github.com/RedHatInsights/insights-results-aggregator-exporter)
[![GitHub Pages](https://img.shields.io/badge/%20-GitHub%20Pages-informational)](https://redhatinsights.github.io/insights-results-aggregator-exporter/)
[![Go Report Card](https://goreportcard.com/badge/github.com/RedHatInsights/insights-results-aggregator-exporter)](https://goreportcard.com/report/github.com/RedHatInsights/insights-results-aggregator-exporter)
[![Build Status](https://travis-ci.com/RedHatInsights/insights-results-aggregator-exporter.svg?branch=master)](https://travis-ci.com/RedHatInsights/insights-results-aggregator-exporter)
![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/RedHatInsights/insights-results-aggregator-exporter)
[![License](https://img.shields.io/badge/license-Apache-blue)](https://github.com/RedHatInsights/insights-results-aggregator-exporter/blob/master/LICENSE)

Exporter for Insights Results data stored by Insights Results Aggregator

<!-- vim-markdown-toc GFM -->

* [Description](#description)
* [Usage](#usage)
    * [Building](#building)
* [Makefile targets](#makefile-targets)
    * [Configuration](#configuration)

<!-- vim-markdown-toc -->

## Description

Simple service that is able to read data from selected database (PostgreSQL,
RDS etc.) and store the data as set of CSV files and into S3 bucket. That
service can be used to make a database snapshot, even for databases that are
not directly reachable by user.

## Usage

```
Usage of ./irae:
  -authors
        show authors
  -output string
        output to: CSV, S3
  -show-configuration
        show configuration
  -summary
        print summary table after export
  -version
        show version

```

### Building

Go version 1.14 or newer is required to build this tool.

```
make build
```

## Makefile targets

```
Usage: make <OPTIONS> ... <TARGETS>

Available targets are:

clean                Run go clean
build                Keep this rule for compatibility
fmt                  Run go fmt -w for all sources
lint                 Run golint
vet                  Run go vet. Report likely mistakes in source code
cyclo                Run gocyclo
ineffassign          Run ineffassign checker
shellcheck           Run shellcheck
errcheck             Run errcheck
goconst              Run goconst checker
gosec                Run gosec checker
abcgo                Run ABC metrics checker
style                Run all the formatting related commands (fmt, vet, lint, cyclo) + check shell scripts
run                  Build the project and executes the binary
test                 Run the unit tests
bdd_tests            Run BDD tests
before_commit        Checks done before commit
help                 Show this help screen
```

### Configuration

Default name of configuration file is `config.toml`.
It can be changed via environment variable `INSIGHTS_RESULTS_EXPORTER_CONFIG_FILE`.

An example of configuration file that can be used in devel environment:

```
[storage]
db_driver = "postgres"
pg_username = "postgres"
pg_password = "postgres"
pg_host = "localhost"
pg_port = 5432
pg_db_name = "aggregator"
pg_params = "sslmode=disable"

[s3]
type = "minio"
endpoint_url = "127.0.0.1"
endpoint_port = 9000
access_key_id = "foobar"
secret_access_key = "foobar"
use_ssl = false
bucket = "test"

[logging]
debug = true
log_level = ""
```

Environment variables that can be used to override configuration file settings:

```
INSIGHTS_RESULTS_AGGREGATOR_EXPORTER__STORAGE__DB_DRIVER
INSIGHTS_RESULTS_AGGREGATOR_EXPORTER__STORAGE__PG_USERNAME
INSIGHTS_RESULTS_AGGREGATOR_EXPORTER__STORAGE__PG_PASSWORD
INSIGHTS_RESULTS_AGGREGATOR_EXPORTER__STORAGE__PG_HOST
INSIGHTS_RESULTS_AGGREGATOR_EXPORTER__STORAGE__PG_PORT
INSIGHTS_RESULTS_AGGREGATOR_EXPORTER__STORAGE__PG_DB_NAME
INSIGHTS_RESULTS_AGGREGATOR_EXPORTER__STORAGE__PG_PARAMS
INSIGHTS_RESULTS_AGGREGATOR_EXPORTER__LOGGING__DEBUG
INSIGHTS_RESULTS_AGGREGATOR_EXPORTER__LOGGING__LOG_DEVEL
```
