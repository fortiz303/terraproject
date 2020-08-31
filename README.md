	This terraform project will launch a web server, create load balancer (ELB) and install nginx and create security groups for both the load balancer and the EC2 instance. This assumes you have created a key pair.




	A more detailed explanation as to how the terraform project is running:
	
	(1)Defines version of terraform
	(5) Defines provider and defines specific region that we have stored in our variables file.
	(9) Defines resource “aws_vpc” and set it as default
	(10)Defines the ip range of the vpc.
	(11) Resolves DNS within the network
	(14) Provides a name tag to identify. We can use more than one tag for more than one property.
	(18) Defining what subnet the vpc will be using
	(28) Defining the internet gateway
	(29) Defines the internet gateway for the specific id that is defined above
	(36) Defines the routing table for the internet gateway defined above
	(39)Allows open internet access
	(44) Provides a name tag to route table
	(49-52) Defines route table and subnet association to connect both the route table ad subnet
	(56-84) Defines our security groups and amongst other things, defines the security access for specific ports, and from specific IP addresses. Ingress are incoming and egress are outbound/outgoing traffic
	(88) Defining the security group for ELB
	(94-108) Defines our security groups and amongst other things, defines the security access for	specific ports, and from specific IP addresses
	(111) Defines a dependency that internet gateway must be present for defining the ELB
	(114) Define the elb and gives it the name 
	(118) Defines which subnet we can connect to (same availability zone)
	(120) Defines our security group on line 88
	(122-135) Defines the listeners for load balancing and health checks for the connected machines. Does health checks at specific intervals on a defined URL/path.
	(139-144) Defines the instance and distributes the load across different AZ zones. The instance will get registered automatically in the ELB.
	(146) Defining our ec2 instance which will be our web server.
	(151) Defines our ami from the variables defined already in the variables file
	(158) Defines the key pair name of the private key that is used to access this EC2
	(161-163) Assigning the security groups and subnets and user data while booting the EC2.Also installs the nginx from a separate file (userdata.sh)

	NOTE: Defining variables in another file is a precaution/security 
