# VPC & Networking
## VPC
Amazon Virtual Private Clud (VPC) is a commercial cloud computing service that provides users a virtual private cloud, by provisioning a logically isolated section of AWS Cloud. Amazon VPC enables you to build a virtual network in the AWS cloud.
### IP Addresses in AWS
There are two kinds of IPs in AWS:

__IPv4__ - _Internet Protocol version 4_:
- Public IPv4 can be used on the internet
- EC2 instances are assigned a new public IP address every time it starts (even if not terminated)
- Private IPv4 can be used on private networks (LAN) such as internal AWS networking
- Private IPv4 is fixed for EC2 instances once created

__Elastic IP__ - allows you to attach a fixed public IPv4 address to an EC2 instance

__IPv6__ - _Internet Protocol version 6_:
- Each IP address is public
- Example: 2001:db4:6666:9999:aaaa:mmmm:nnnn:iiii

## Subnets
A subnet is a range of IP addresses in your VPC. You can launch AWS resources, such as EC2 instances, into a specific subnet. Simply put, subnets allows you to partition your network inside your VPC. Whilst a VPC is a "regional resource" (bound by region), subnets are an AZ resource (bount by availability zones).

## Internet Gateway
An Internet Gateway helps communication between our VPC and the Internet. A **public subnet** has a direct route to an internet gateway. Resources in a public subnet can access the public internet. A **private subnet** does not have a direct route to an internet gateway. Resources in a private subnet require a NAT device to access the public internet.

## NAT Gateway
A NAT Gateway (AWS-managed) and NAT Instances (self-managed) allow instances in your private subnets to access the internet whilst remaining private.

## Peering connections
A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses. This allows resources to in either VPC to communicate with each other as if they are within the same network.

## Network Access Control List (NACL)
A firewall which controls traffic from and to subnets. With NACL you can have _ALLOW_ and _DENY_ rules, these only include IP addresses. NACL operates at the subnet level, thus applies to all instances inside the associated subnet.

## Security Groups
A firewall that controls traffic to and from and EC2 instance. Security groups only have _ALLOW_ rules that include IP addresses and other security groups.

## VPC Flow Logs
VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC, so we are able to get VPC flow logs, subnet flow logs, and Elastic Network Interface flow logs. By enabling Flow Logs we are able to monitor & troubleshoot connectivity issues.

## VPC Endpoints
VPC Endpoints allow you to connect to AWS services using a private network instead of the public internet network. This in turn gives you enhanced security and lower latency when accessing AWS services. The two types of VPC Endpoints are __Gateway__ which will connect to S3 and DynamoDB, and the other is __Interface__ which can be used to connect to the rest of AWS services.

## AWS PrivateLink (VPC Endpoint Services)
AWS PrivateLink provides private connectivity between VPCs, supported AWS services, and your own on-premises networks without exposing your traffic to the public internet.
It is the most secure and scalable way to expose a service to numerous VPCs and does not require VPC peering, internet gateway, NAT, etc. In order to do this the service VPC will require a Network Load Balancer, and the customer VPC will require an Elastic Network Interface (ENI).

## Site to Site VPN
A Site to Site VPN enables you to connect your on-prem VPN to AWS, the connection will be automatically encrypted and will go over the public internet. For a Site to Site VPN to be implemented between your on-prem datacentre and your VPC you will need to use a Customer Gateway (CGW) for on-prem, and a Virtual Private Gatweay (VGW) for your VPC.
## Direct Connect (DX)
AWS Direct Connect links your internal network to an AWS Direct Connect location over a standard Ethernet fiber-optic cable, in other words DX establishes a physical connection between your on-prem datacentre and AWS. The connection is private, secure, and fast and goes over a private network. Compared to a Site-to-Site VPN it takes much longer to set up and is more expensive.

## AWS Client VPN
Allows you to securely connect to your private network in AWS and on-prem using an OpenVPN.

## Transit Gateway
This is a network transit hub that you can use to interconnect your VPCs and on-prem networks. Transit Gateway enables a peering connection bewteen numerous VPCs and on-premises systems. 