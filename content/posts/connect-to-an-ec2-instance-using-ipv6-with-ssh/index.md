---
id: "MtofmWm3TjewL5SBjmQr3Q"
status: "published"
createdAt: "2024-08-22T10:55:57+01:00"
firstPublishedAt: "2024-08-22T11:03:53+01:00"
publishedAt: "2024-08-22T11:03:53+01:00"
updatedAt: "2024-08-22T11:03:42+01:00"
author_id: "156386009"
category_id: "Z84lDne0Qvi9gJdIH3q5xA"
cover_image: "images/blogging_llms.webp"
date: "2024-08-22"
excerpt: "Connect to an EC2 Instance Using IPv6 (with SSH). Needed Commands an LLMs chat link"
slug: "connect-to-an-ec2-instance-using-ipv6-with-ssh"
title: "Connect to an EC2 Instance Using IPv6 (with SSH)"
---

# Connect to an EC2 Instance Using IPv6 (with SSH)

# Introduction

In this post, I’d like to explain an issue I encountered recently. When connecting to my AWS services, I experienced a problem after my current ISP switched to IPv6.

While it’s great that the ISP finally made this step forward, my SSH access to my EC2 instances stopped working.

Previously, I was using a command like this:

```bash
ssh -i ~/.ssh/id_rsa vicens@my-amazon-dns.eu-west-3.compute.amazonaws.com
```

But it suddenly stopped working, and I received a timeout error.

Below, you’ll find the steps I followed to get it working again. You can, of course, refer to an LLM model for a similar explanation. In my case, it took some trial and error to resolve the issue, and I’d like to share what I learned with you

> LLMs are great, but they can lead to significant time loss if you follow their instructions blindly without fully understanding what you're doing!
>
>

# What is the problem?

The problem is that if you have a public IPv6 address, you can only connect to machines that are also using IPv6. Therefore, you need to enable IPv6 on the EC2 instance, as this is not done by default.

In a typical EC2 setup, you need to check and configure the following:

- Check if the VPC has IPv6 enabled and configure it properly if it does not.

- Check if the subnet has an IPv6 block \(or more than one, as in my case\) and configure it properly if it does not.

- Ensure the EC2 instance has an IPv6 address and configure it properly if it does not.

- Configure the security group associated with your instance to accept SSH requests \(port 22\) from your local public IPv6 address.

- Verify that the VPC is linked to the correct routing tables, and add the necessary route table for IPv6.

You can see the steps outlined in this public chat:

[https://chatgpt.com/share/ad5070bc-c2b0-4c7c-a4c0-ea2218d3c29c](https://chatgpt.com/share/ad5070bc-c2b0-4c7c-a4c0-ea2218d3c29c)

Since the routing table setup can be a bit tricky, I’ve summarized the commands I had to run below:

```bash
# verify VPC ID
`aws ec2 describe-vpcs --query 'Vpcs[*].{VpcId:VpcId,IsDefault:IsDefault}' --output json`

# List All Route Tables Without Filtering (important!) I got empty list when I ran other commands with filtering
`aws ec2 describe-route-tables --query 'RouteTables[*].{RouteTableId:RouteTableId,Associations:Associations}' --output json`

# Create a new route table (I did not need to do that because I had one)
aws ec2 create-route-table --vpc-id <vpc-id>

# Create the new route table
aws ec2 create-route --route-table-id <route-table-id> --destination-ipv6-cidr-block ::/0 --gateway-id <internet-gateway-id>

# associate it to your subnet
aws ec2 associate-route-table --route-table-id <route-table-id> --subnet-id <subnet-id>

## and just for your convinience the command to retrieve the subnet ID
aws ec2 describe-subnets --query 'Subnets[*].[SubnetId, VpcId]' --output text
```
```

# Don't Use DNS with IPv6 \(out of the box\)

Since switching to IPv6, DNS resolution no longer works, as it is mapped to an IPv4 address such as \`my-amazon-dns.eu-west-3.compute.amazonaws.com\`.

```bash
# This does not work anymore
ssh -i ~/.ssh/id_rsa vicens@my-amazon-dns.eu-west-3.compute.amazonaws.com

# This work (IPv6 direcly)
ssh -i ~/.ssh/id_rsa vicens@1020:d013:7820:39e:9fc:440a:120e:66aa
```

> It is possible to map a DNS to your IPv6 address, although I haven’t explored this option yet. It shouldn’t be too difficult to set up.
>
>

# Additional Troubleshooting Steps

The setup I described worked for my \_standard\_ EC2 installation, given my local configuration. However, if you're still experiencing issues, you can try the following extra checks:

## Can Your Local Machine Ping IPv6 Public Addresses?

Open a terminal and run this command, which pings Google’s IPv6 address:

```
ping6 2001:4860:4860::8888
```

## Check the AWS NACL

NACL \(Network Access Control List\) is another layer of protection between the outside world and your EC2 instances. It acts as a subnet-level firewall. Normally, you don’t need to adjust anything here since it allows all inbound and outbound traffic by default. However, if you're still facing issues, double-check your NACL settings using your LLM.

> Typically, security rules are managed through AWS security groups \(the AWS logical layer\) and in the EC2 instance itself if it has a firewall \(as in my case\).
>
>

# Summary

I hope this post helps if you encounter the same issue. I’m experimenting with writing posts that truly provide value in our modern times, where LLMs often serve as a primary source of information. I’d love to hear your feedback!
