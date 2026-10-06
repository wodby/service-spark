# Apache Spark master on Wodby

What Wodby sets up for a Spark standalone master on this service. It runs the official `apache/spark` image with `org.apache.spark.deploy.master.Master`.

- The master accepts workers and applications on port 7077 (`spark://<master service name>:7077` from other services in the environment). This port is private.
- The web interface is on port 8080.
- `SPARK_PUBLIC_DNS`, the public DNS name Spark uses for the master, is the service's host.
- Ports and the listen address are fixed by the container arguments in the manifest. Other settings are environment variables on the service.
- The service has no volume and is not scalable.

Workers are a separate service, Spark worker, linked to this one.
