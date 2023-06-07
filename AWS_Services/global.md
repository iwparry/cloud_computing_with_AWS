# AWS Global Applications
We are able to make global applications by leveraging AWS Global Infrastructure. Global applications are appllications thaare dployed in multiple geographies, i.e. in AWS they could be doployed in multiple regions and/or edge locations. The benefits of this includes, decreased latency, for services that have end users all over the globe we can deploy our applications closer to them to decrease latency, providing a better experience. Another benefit is disaster recovery, if an AWS region goes down you can fail-over to another region and have your application still working. A distributed global infrastructure is also harder to attack as it protects you against hackers for example, its difficult for them to attack your applciation if its deployed accross multiple regions.

AWS Global Infrastructure contains regions, for deploying applications and infrastructure, which have several availability zones that are made of multiple data centres, and edge locations (points of presence) for content delivery as close as possible to users.

## Route 53
A managed DNS (Domain Name System), a collection of rules and records which helps clients understand ho to reach a server through URLs.

Most common records in AWS:
- www.google.com -> 12.34.56.78 = A record (IPV4)
- www.google.com -> 2001:0db8:85a3:0000:8a2e:0370:7334 = AAAA IPv6
- search.google.com -> www.google.com = CNAME:hostname to hostname
- example.com -> AWS resource = Alias (ex: ELB, CloudFront, S3, RDS, etc.)

### Routing Policies
__Simple routing policy__ - Use for a single resource that performs a given function for your domain, for example, a web server that serves content for the example.com website. Does not have a health check.

__Weighted routing policy__ - Use to route traffic to multiple resources in proportions that you specify. It is basically a form of load balancing.

__Latency routing policy__ - Use when you have resources in multiple AWS regions and you want to route traffic to the region that provides the best latency. Essentially routes traffic from users to the nearest server.
 to minimize latency.

__Failover routing policy__ - Use when you want to configure active-passive failover. So our DNS will perform a health check on our primary instance and in the case the primary instance fails, traffic will be directed to a failover instance, this helps with disaster recovery.

## AWS CloudFront
CloudFront is a Content Delivery Network (CDN). It improves the read performance by caching the content of your website at different edge locations, this in turn improves user experience (reduced latency). Because content is distributed globally companies are getting DDoS protection, integration with Shield, AWS Web Application Firewall.

### CloudFront Origins
- S3 bucket
- Custom Origin (HTTP)

### S3 Transfer Acceleration
Increases the transfer sppeed of files by transferring them to an AWS edge location which will forward the data to the S3 bucket in the target region.

## AWS Global Accelerator
Improves the availability and performance of global applications by using the AWS global network. 2 Anycast IPs are created for your application and traffic is sent through edge locations. 

## AWS Outposts
AWS Outposts are "server racks" that offers the same AWS infrastructure services, APIs and tools to build your own applications on-premises just as in the cloud. AWS will setup and manage "Outposts Racks" within your on-premises infrastructure and you can satrt leveraging AWS services on-premises.

You are responsible for the Outposts Rack physical security since it is located in your own data centre.

## AWS WaveLength
WaveLength Zones are infrsatructure deployments embedded within the telecommunications providers' datacentres at the edge of the 5G networks. This enables you to deploy AWS services to the edge of the 5G networks.

## AWS Local Zones
Allows you to place compute, storage, database and other selected AWS services closer to your end users to run latency-sensitive applications. The idea is to extend your VPC to more locations, essentially an extension of an AWS Region.

Note not all Regions have Local Zones e.g. Ireland has no Local Zones, but N.Virginia has Local Zones such as Boston.