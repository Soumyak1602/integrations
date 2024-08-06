# Amazon Managed Streaming for Apache Kafka (MSK)

The Amazon Kafka integration allows you to monitor [Amazon MSK](https://aws.amazon.com/msk/) — it's a fully managed 
service that makes it easy for you to build and run applications that use Apache Kafka to process streaming data

Use the Amazon Kafka integration to collect metrics related to your MSK clusters from CloudWatch. This integration only
supports collecting DEFAULT level monitoring metrics for now. Once these metrics are sent to Elastic, you can visualize 
them in Kibana, create alerts to notify you if something goes wrong, and reference the metrics when troubleshooting 
an issue.

**IMPORTANT: Extra AWS charges on AWS API requests will be generated by this integration. Please refer to the AWS 
integration for more details.**

## Data streams

The Amazon Kafka integration collects one type of data: metrics.

**Metrics** give you insight into the state of Amazon MSK.
The metrics collected by the Amazon Kafka integration include bytes received from clients, bytes sent to clients, number
of incoming messages and more. See more details in the [Metrics reference](#metrics-reference)

## Requirements

You need Elasticsearch for storing and searching your data and Kibana for visualizing and managing it.
You can use our hosted Elasticsearch Service on Elastic Cloud, which is recommended, or self-manage the Elastic Stack on your own hardware.

Before using any AWS integration you will need:

* **AWS Credentials** to connect with your AWS account.
* **AWS Permissions** to make sure the user you're using to connect has permission to share the relevant data.

For more details about these requirements, see the **AWS** integration documentation.

## Setup

Use this integration if you only need to collect data from the Amazon MSK service.

If you want to collect data from two or more AWS services, consider using the **AWS** integration.
When you configure the AWS integration, you can collect data from as many AWS services as you'd like.

For step-by-step instructions on how to set up an integration, see the
{{ url "getting-started-observability" "Getting started" }} guide.

## Metrics reference

{{event "kafka_metrics"}}

**ECS Field Reference**

Please refer to the following [document](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for detailed information on ECS fields.

{{fields "kafka_metrics"}}