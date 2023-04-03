# VPC - Virtual Private Cloud
A VPC is a virtual network that closely resembles a traditional network that you'd operate in your own data centre, but with the benefits of using the scalable infrastructure of AWS. Amazon VPC enables you to launch AWS resources into a virtual network that you've defined.

AWS provides us with a default VPC, which we can view in the VPC console.

![](images/vpc-rss-map.png)

Here we can view details about our VPC such as ID, IPv4 CIDR, etc. AWS has added a new feature to the VPC console which is _Resource map_ which provides us a visualisation of our network inside our VPC.

## Subnets
A subnet is a range of IP addresses in your VPC. A subnet must reside in a single Availability Zone. After you add subnets, you can deploy AWS resources in your VPC. Simply put, subnets allows you to partition your network inside your VPC.

### Types
__Public__ - The subnet has a direct route to an internet gateway. Resources inside a public subnet can access the internet

__Private__ - The subnet does not have a direct route to an internet gateway. Resources in a private subnet requre a NAT device to access the internet.

## Routing
In AWS we can use route tables to determine where network traffic from your subnet or intenet gateway is directed.

## Internet Gateway
An Internet Gateway is a VPC component that allows communication between your VPC and the internet, it supports IPv4 and IPv6 traffic.

## Peering connections
A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses. This allows resources to in either VPC to communicate with each other as if they are within the same network.