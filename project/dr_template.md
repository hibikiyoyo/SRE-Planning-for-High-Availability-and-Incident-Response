# Infrastructure

## AWS Zones
Identify your zones here
us-east-2: "us-east-2a","us-east-2b"
us-west-1: "us-west-1a","us-west-1c"
## Servers and Clusters

### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EC2 | Multiple availability zones and have redundancy | AWS size eg. t3.micro (if applicable, not all assets will have a size) | 2 | In AWS availability zones should be used to ensure zone availability. That way if a zone fails, you have backups |
| Kubernetes | have a voting majority |  | 2 nodes | Kubernetes can spin up more pods, there is again the problem of quorum and just general node failure |
| Azs | Multiple Azs |  | 2 | more HA |
| DB | there are no data center failures |  | 3 | quorum and HA |


### Descriptions
- Assets should run in multiple regions. It is not good practice to run everything in one region. The regions should be geographically dispersed
- 1 database node is not HA. Adding 3 nodes is ideal. There needs to be an odd number of voters in case of a failure so an election can take place and have a winner.
- While Kubernetes can spin up more pods, there is again the problem of quorum and just general node failure. Ideally 3 to have a voting majority. More if the load calls for it.
- The EC2 node should have IP space in multiple availability zones and have redundancy. In AWS availability zones should be used to ensure zone availability. That way if a zone fails, you have backups. The application architecture will dictate the appropriate number but 1 is a failure point that should be addressed.

## DR Plan
### Pre-Steps:
Ensure the infrastructure is set up and working in the DR site.

## Steps:
- Create a cloud load balancer and point DNS to the load balancer
    - multiple instances behind 1 IP in a region
- Point your DNS to your secondary region
    - This can be done with a name provider like Amazon route 53
- Failover your database replication instances to another region
    - Manually force the secondary region to become primary at the database level
    - Automatically failover the database by health checks