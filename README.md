# Spark service for Kubernetes on Wodby

Run Spark as a reusable Kubernetes application service with Wodby.

This repository defines the Wodby service manifests and operational
configuration for Spark.

- [Browse Wodby services](https://wodby.com/services)
- [Wodby service documentation](https://wodby.com/docs/2.0/services/)
- [Service manifest reference](https://wodby.com/docs/2.0/services/template/)

## Wodby stacks using this service

- [Apache Spark application stack](https://github.com/wodby/stack-spark)

## Service entries

### Apache Spark master

| Property | Manifest configuration |
| --- | --- |
| Service name | `spark-master` |
| Type | Application service |
| Versions | `4.1` by default |
| Workloads | `main` (Deployment, primary) |
| Containers | `spark-master` using `apache/spark` |
| Endpoints | `spark`: TCP 7077 (main), HTTP 8080 |
| Service links | None |
| Application build | Not buildable from application source |
| Helm | chart `oci://registry-1.docker.io/wodby/stateless`; version `0.2.0` |

Manifest: [`master/service.yml`](master/service.yml)

### Apache Spark worker

| Property | Manifest configuration |
| --- | --- |
| Service name | `spark-worker` |
| Type | Application service |
| Versions | `4.1` by default |
| Workloads | `main` (Deployment, primary) |
| Containers | `spark-worker` using `apache/spark` |
| Endpoints | None |
| Service links | Apache Spark master (`master`), required |
| Application build | Not buildable from application source |
| Helm | chart `oci://registry-1.docker.io/wodby/stateless`; version `0.2.0` |
| Configuration and operations | 2 settings |

Manifest: [`worker/service.yml`](worker/service.yml)

## Use this service

Use this service through [Apache Spark application stack](https://github.com/wodby/stack-spark), or reference `spark-master`,
`spark-worker` from a custom Wodby stack.

A service is a reusable component and does not deploy by itself. The stack
defines its links, settings, versions, resources, and relationship to the rest
of the application.

## Maintain a custom version

1. Fork this repository.
2. Edit the service manifest and referenced files.
3. Import the repository as a [Git-backed service](https://wodby.com/docs/2.0/services/create/#create-a-git-backed-service).
4. Reference the service from a stack manifest.

Keep service, workload, container, endpoint, link, volume, config, and
derivative names stable unless dependent stacks and app-level overrides are
updated at the same time.

Validate the manifests with:

```bash
wodby service validate-manifest master/service.yml --org <org-id>
wodby service validate-manifest worker/service.yml --org <org-id>
```

See the [service manifest reference](https://wodby.com/docs/2.0/services/template/) and the [managed services index](https://github.com/wodby/services).
