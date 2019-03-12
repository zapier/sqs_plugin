# sqs_plugin

## Background

A lot of ETL work is done in other systems. Many of those other systems' schedulers/orchestration is inferior to that of Airflow. This plugin allows Airflow to use [AWS SQS](https://aws.amazon.com/sqs/) to communicate between Airflow and these other systems.

## Requirements

### Sensor

The primary requirement is a sensor. The sensor would await in a `running` state for an SQS message. Once an SQS message for that `dag`, `task`, and `execution_date` was received, it would change to a `success` state.

#### Timeout

The sensor would have a timeout parameter after which it would fail. Whether it went into `failed` or `up_for_retry` would depend on how `num_retries` was set for the sensor.
