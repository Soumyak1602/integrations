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
[Getting started](https://www.elastic.co/guide/en/welcome-to-elastic/current/getting-started-observability.html) guide.

## Metrics reference

An example event for `kafka` looks as following:

```json
{
    "@timestamp": "2024-02-21T23:35:00.000Z",
    "agent": {
        "ephemeral_id": "0c8bf84c-f257-496d-a788-89af2b6959ae",
        "id": "0395c9d5-9ac1-4ecc-bfd5-fc5376847519",
        "name": "docker-fleet-agent",
        "type": "metricbeat",
        "version": "8.11.4"
    },
    "aws": {
        "cloudwatch": {
            "namespace": "AWS/Kafka"
        },
        "dimensions": {
            "ClusterName": "qa-awseuw1-cp-internal-app-2-usage-data",
            "ConsumerGroup": "usage-data-pipeline",
            "Topic": "usage-data-pipeline"
        },
        "kafka": {
            "metrics": {
                "EstimatedMaxTimeLag": {
                    "sum": 1
                },
                "MaxOffsetLag": {
                    "sum": 31
                },
                "SumOffsetLag": {
                    "sum": 31
                }
            }
        }
    },
    "cloud": {
        "account": {
            "id": "123456789012",
            "name": "MonitoringAccount"
        },
        "provider": "aws",
        "region": "eu-west-1"
    },
    "data_stream": {
        "dataset": "aws.kafka_metrics",
        "namespace": "default",
        "type": "metrics"
    },
    "ecs": {
        "version": "8.11.0"
    },
    "elastic_agent": {
        "id": "0395c9d5-9ac1-4ecc-bfd5-fc5376847519",
        "snapshot": false,
        "version": "8.11.4"
    },
    "event": {
        "agent_id_status": "verified",
        "dataset": "aws.kafka_metrics",
        "duration": 67075155989,
        "ingested": "2024-02-21T23:47:52Z",
        "module": "aws"
    },
    "host": {
        "architecture": "aarch64",
        "containerized": false,
        "hostname": "docker-fleet-agent",
        "id": "1b287af46f2942b3ba34c3ee5a5c6111",
        "ip": [
            "172.20.0.7"
        ],
        "mac": [
            "02-42-AC-14-00-07"
        ],
        "name": "docker-fleet-agent",
        "os": {
            "codename": "focal",
            "family": "debian",
            "kernel": "6.4.16-linuxkit",
            "name": "Ubuntu",
            "platform": "ubuntu",
            "type": "linux",
            "version": "20.04.6 LTS (Focal Fossa)"
        }
    },
    "metricset": {
        "name": "cloudwatch",
        "period": 60000
    },
    "service": {
        "type": "aws"
    }
}
```

**ECS Field Reference**

Please refer to the following [document](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for detailed information on ECS fields.

**Exported fields**

| Field | Description | Type | Metric Type |
|---|---|---|---|
| @timestamp | Event timestamp. | date |  |
| agent.id | Unique identifier of this agent (if one exists). Example: For Beats this would be beat.id. | keyword |  |
| aws.cloudwatch.namespace | The namespace specified when query cloudwatch api. | keyword |  |
| aws.dimensions.BrokerID | Filters the metric data by broker ID. | keyword |  |
| aws.dimensions.ClientAuthentication | Filters the metric data by client authentication. | keyword |  |
| aws.dimensions.ClusterName | Filters the metric data by cluster name. | keyword |  |
| aws.dimensions.ConsumerGroup | Filters the metric data by consumer group. | keyword |  |
| aws.dimensions.Topic | Filters the metric data by topic. | keyword |  |
| aws.kafka.metrics.ActiveControllerCount.sum | The total number of active controllers. Only one controller per cluster should be active at any given time. | long | gauge |
| aws.kafka.metrics.BurstBalance.avg | The average remaining balance of input-output burst credits for EBS volumes in the cluster. | long | gauge |
| aws.kafka.metrics.BytesInPerSec.sum | The total number of bytes per second received from clients in the given collection period. | long | gauge |
| aws.kafka.metrics.BytesOutPerSec.sum | The total number of bytes per second sent to clients in the given collection period. | long | gauge |
| aws.kafka.metrics.CPUCreditBalance.avg | The average number of earned CPU credits that a broker has accrued since it was launched. | long | gauge |
| aws.kafka.metrics.ClientConnectionCount.sum | The total number of active authenticated client connections. | long | gauge |
| aws.kafka.metrics.ConnectionCount.sum | The total number of active authenticated, unauthenticated, and inter-broker connections. | long | gauge |
| aws.kafka.metrics.CpuIdle.avg | The average percentage of CPU idle time. | long | gauge |
| aws.kafka.metrics.CpuIoWait.avg | The average percentage of CPU idle time during a pending disk operation. | long | gauge |
| aws.kafka.metrics.CpuSystem.avg | The average percentage of CPU in kernel space. | long | gauge |
| aws.kafka.metrics.CpuUser.avg | The average percentage of CPU in user space. | long | gauge |
| aws.kafka.metrics.EstimatedMaxTimeLag.sum | The total time estimate (in seconds) to drain MaxOffsetLag in the given collection period. | long | gauge |
| aws.kafka.metrics.FetchMessageConversionsPerSec.sum | The total number of fetch message conversions per second for the topic in the given collection period. | long | gauge |
| aws.kafka.metrics.GlobalPartitionCount.sum | The total number of partitions across all topics in the cluster, excluding replicas. | long | gauge |
| aws.kafka.metrics.GlobalTopicCount.sum | The total number of topics across all brokers in the cluster. | long | gauge |
| aws.kafka.metrics.HeapMemoryAfterGC.avg | The average percentage of total heap memory in use after garbage collection. | long | gauge |
| aws.kafka.metrics.KafkaAppLogsDiskUsed.avg | The average percentage of disk space used for application logs. | long | gauge |
| aws.kafka.metrics.KafkaDataLogsDiskUsed.avg | The average percentage of disk space used for data logs. | long | gauge |
| aws.kafka.metrics.LeaderCount.sum | The total number of leaders of partitions per broker, not including replicas. | long | gauge |
| aws.kafka.metrics.MaxOffsetLag.sum | The total maximum offset lag across all partitions in a topic in the given collection period. | long | gauge |
| aws.kafka.metrics.MemoryBuffered.avg | The average size in bytes of buffered memory for the broker. | long | gauge |
| aws.kafka.metrics.MemoryCached.avg | The average size in bytes of cached memory for the broker. | long | gauge |
| aws.kafka.metrics.MemoryFree.avg | The average size in bytes of memory that is free and available for the broker. | long | gauge |
| aws.kafka.metrics.MemoryUsed.avg | The average size in bytes of memory that is in use for the broker. | long | gauge |
| aws.kafka.metrics.MessagesInPerSec.sum | The total number of incoming messages per second for the broker in the given collection period. | long | gauge |
| aws.kafka.metrics.NetworkRxDropped.sum | The total number of dropped receive packages. | long | counter |
| aws.kafka.metrics.NetworkRxErrors.sum | The total number of network receive errors for the broker. | long | counter |
| aws.kafka.metrics.NetworkRxPackets.sum | The total number of packets received by the broker. | long | counter |
| aws.kafka.metrics.NetworkTxDropped.sum | The total number of dropped transmit packages. | long | counter |
| aws.kafka.metrics.NetworkTxErrors.sum | The total number of network transmit errors for the broker. | long | counter |
| aws.kafka.metrics.NetworkTxPackets.sum | The total number of packets transmitted by the broker. | long | counter |
| aws.kafka.metrics.OfflinePartitionsCount.avg | The average number of partitions that are offline in the cluster. | long | gauge |
| aws.kafka.metrics.PartitionCount.avg | The average number of topic partitions per broker, including replicas. | long | gauge |
| aws.kafka.metrics.ProduceMessageConversionsPerSec.sum | The total number of produce message conversions per second for the topic in the given collection period. | long | gauge |
| aws.kafka.metrics.ProduceTotalTimeMsMean.avg | The mean produce time in milliseconds. | long | gauge |
| aws.kafka.metrics.RequestBytesMean.avg | The mean number of request bytes for the broker. | long | gauge |
| aws.kafka.metrics.RequestTime.avg | The average time in milliseconds spent in broker network and I/O threads to process requests. | long | gauge |
| aws.kafka.metrics.RootDiskUsed.avg | The average percentage of the root disk used by the broker. | long | gauge |
| aws.kafka.metrics.SumOffsetLag.sum | The total aggregated offset lag for all the partitions in a topic. | long | gauge |
| aws.kafka.metrics.SwapFree.avg | The average size in bytes of swap memory that is available for the broker. | long | gauge |
| aws.kafka.metrics.SwapUsed.avg | The size in bytes of swap memory that is in use for the broker. | long | gauge |
| aws.kafka.metrics.TrafficShaping.avg | The average number of packets shaped (dropped or queued) due to exceeding network allocations. | long | gauge |
| aws.kafka.metrics.UnderMinIsrPartitionCount.avg | The average number of under minIsr partitions for the broker. | long | gauge |
| aws.kafka.metrics.UnderReplicatedPartitions.avg | The average number of under-replicated partitions for the broker. | long | gauge |
| aws.kafka.metrics.ZooKeeperRequestLatencyMsMean.avg | The mean latency in milliseconds for Apache ZooKeeper requests from broker. | long | gauge |
| aws.tags | Tag key value pairs from aws resources. | flattened |  |
| cloud.account.id | The cloud account or organization id used to identify different entities in a multi-tenant environment. Examples: AWS account id, Google Cloud ORG Id, or other unique identifier. | keyword |  |
| cloud.image.id | Image ID for the cloud instance. | keyword |  |
| cloud.region | Region in which this host, resource, or service is located. | keyword |  |
| data_stream.dataset | Data stream dataset. | constant_keyword |  |
| data_stream.namespace | Data stream namespace. | constant_keyword |  |
| data_stream.type | Data stream type. | constant_keyword |  |
| event.module | Event module | constant_keyword |  |
| host.containerized | If the host is a container. | boolean |  |
| host.os.build | OS build information. | keyword |  |
| host.os.codename | OS codename, if any. | keyword |  |
