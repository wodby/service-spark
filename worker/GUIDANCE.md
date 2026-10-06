# Apache Spark worker on Wodby

What Wodby sets up for a Spark standalone worker on this service. It runs the official `apache/spark` image with `org.apache.spark.deploy.worker.Worker`.

## Linked services

| Link | Variables |
| --- | --- |
| Apache Spark master (required) | `SPARK_MASTER_URL` |

The worker registers with the master at that address when it starts. Do not set the master address elsewhere.

## Settings

| Setting | Variable | Meaning |
| --- | --- | --- |
| Worker CPU cores | `SPARK_WORKER_CORES` | cores Spark applications may use on this worker |
| Worker memory | `SPARK_WORKER_MEMORY` | memory Spark applications may use on this worker |

These are what the worker offers to the master. They are separate from the container's CPU and memory resources: keep them within the container's limits.

## Other facts

- The service is scalable: each replica is one worker.
- It has no endpoint and no Kubernetes service. The worker's web interface (port 8081) is not reachable from other services.
- It has no volume: application work directories are lost when the pod is replaced.
