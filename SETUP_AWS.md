# AWS SETUP

When we login to AWS we ensure that we set our region to "Ireland", AWS may set to another region my default.

What we then do is search for EC2 in the search bar, following which we launch an instance. 

When on Launch and Instance we input a name and tags for the instance. The naming convention we use here is *name-tech201-app*.

After this we need to choose the AMI for our instance, the one we are after is ubuntu, specifically 18.04.

We need to have a public IP set for our instance.

You will then be asked for a key pair to access the security group, these keys should be provided to you (best practice to move these to your .ssh folder for security).

Leave instance type as "t2.micro"

Then in Networking change the subnet to "DevOpsStudent default 1a"

Under security group rules for our specific group we want 3 rules, one for ssh, one for https...(tbc)

Once all that is done we click Launch Instance, anf this should create our instance in our security group. If everything has been done alright we should see the status of our instance set to "running".