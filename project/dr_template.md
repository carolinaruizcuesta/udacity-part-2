# Infrastructure

## AWS Zones

- zone1: us-east-2
- zone2: us-west-1

## Servers and Clusters

### Table 1.1 Summary

| Asset                   | Purpose                                                     | Size         | Qty                                 | DR                                                                                |
|-------------------------|-------------------------------------------------------------|--------------|-------------------------------------|-----------------------------------------------------------------------------------|
| VM server               | Server that will serve the application code to the internet | t3.micro     | 3 instances / service (in total 6)  | each 3 instances will be deployed in a region, each one in an availability zone.  |
| ALB                     | Distribute traffic to the VM nodes                          |              | 2                                   | Each ALB in a differnet region                                                    |
| Kubernetes cluster node | Host monitoring (prometheus and grafana) pods               | t3.small     | 4 nodes                             | each 2 nodes will be deployed in a different region                               |
| IPs                     | Internet Protocol address for the application instances     |              | 6                                   | Each IP will point to an application server                                       |
| Database cluster        | SQL engine that will host application data                  | db.t3.medium | 2                                   | Each database cluster will be deployed to each region                             |


### Descriptions

- VM server: an instance that has the application code. Each one will execute it redundantly.
- ALB: it distributes traffic among the vm servers.
- Kubernetes cluster node: an instance that will host monitoring pods. Each cluster will monitor its VM instances of the same region.
- Database cluster: each database cluster will have 2 nodes, each one in a different availability zone. The secondary cluster will be replicating from the primary one, which is in another region.

## DR Plan

### Pre-Steps

- The DR region has the same application code version deployed as in the productive region.
- The DR region has the same engine and family database version deployed as in the productive region.
- Deploy the infrastructure as IaC.

## Steps

- DNS is pointing to the IP of the productive Load Balancer.
- During the failover, the DNS A record is changed to the DR region IP.
- Manually or automantically make the database failover so that the secondary cluster is promoted to be the primary one.