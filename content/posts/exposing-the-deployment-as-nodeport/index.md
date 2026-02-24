---
id: "HoiSVIbcSD2KJgTfAQ6gxQ"
status: "published"
createdAt: "2024-09-06T10:31:26+01:00"
firstPublishedAt: "2024-09-06T10:31:30+01:00"
publishedAt: "2024-09-06T10:37:00+01:00"
updatedAt: "2024-09-06T10:36:55+01:00"
author_id: "156386009"
category_id: "Z84lDne0Qvi9gJdIH3q5xA"
cover_image: "images/wheel-helm-container-computer-developer-app-concept-business-digital-open-source-program-data-cod_115739-1959.avif"
date: "2024-09-06"
excerpt: "Step by Step Guide How To Expose Your K8S Deployment As NodePort"
slug: "exposing-the-deployment-as-nodeport"
title: "Exposing Your K8S Deployment as NodePort"
---

# Exposing Your K8S Deployment as NodePort

Let's say we have a running deployment in your Kubernetes Cluster. Your shiny app is ready to be shown to the world. 

How do you achieve this? 

In a Kubernetes \(K8s\) cluster, you have three ways to access your deployment:

- Exposing your deployment as \*\*ClusterIP\*\*: The deployment will only be accessible within your cluster.
- Exposing your deployment as \*\*NodePort\*\*: The deployment will be accessible using a port that is mapped to your deployment. 
- Exposing your deployment as \*\*LoadBalancer\*\*: An external load balancer will handle the traffic to your deployment.

> Please note that internally when you are exposing a deployment, you are actually creating a service. A service is a K8s resource.
>
>

We will go for the second option \(as the main title suggests\)!

The reason for this is that \*\*ClusterIP\*\* only exposes your deployment within the cluster, which is not what we want. The third option, \*\*LoadBalancer\*\*, requires additional configuration, as you need to properly set up the cloud provider hosting your Kubernetes cluster—in our case, AWS.

## Let's Start

Here is the link with all the necessary commands to make it happen. If you'd like a more detailed explanation, keep reading. \[ChatGPT\]\(https://chatgpt.com/share/2017611e-ac3e-49ca-9b7c-ce07fd6027cd\)

We need to:

- Expose the deployment as \*\*NodePort\*\*. This will assign a port and map it to your deployment.
- Open the \*\*Security Group\*\* and firewall \(if applicable\) to allow access to this port.

> To open the security port, we will use the aws-cli  you will need the `Security Group ID` and the `Instance ID`.
>
>

**Expose the deployment as NodeType**

```bash
kubectl expose deployment hello-world \
  --type=NodePort \
  --port=80 \
  --target-port=8080
```

Check the service created by running the following command: \`kubectl get svc hello-world\`. You should see a line similar to this: 

```bash
NAME          TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
hello-world   NodePort   10.106.116.139   <none>        80:31869/TCP   6s
```

Here we are using the port `31869` to map it internally.

> By default, these are ports ranging NodePort offers: 30000-32767
>
>

**Open the security rule in the EC2 security group**

```bash
aws ec2 authorize-security-group-ingress \
    --group-id <your_security_group_id> \
    --protocol tcp \
    --port 31869 \
    --cidr 0.0.0.0/0
```

> Note that in this case, we are using port `31869`, but it can be any port within the designated range.
>
>

You will need the \*\*Security Group ID\*\*, which can be found using the following commands:

```bash
aws ec2 describe-instances \
    --instance-ids <instance_id> \
    --query "Reservations[*].Instances[*].SecurityGroups[*].GroupId" \
    --output text
```

And for this you need the \`instance\_id\` with `aws ec2 describe-instances`

**Second open Internal Firewall Port**

In my case I have \`UFW\` firewall installed in my instance.

`sudo ufw allow 31869/tcp`

## That's all. 

Now the content is accessible through the internet using your public IP and the port we get as example: `http://\<your\_public\_ip\>:31869/`

As you can see, this setup is quite unstable because the port changes every time you expose the application, forcing you to repeatedly open the Security Group \(SG\) and Firewall \(FW\).

To avoid this, you could make the port static, but that’s not an ideal solution. It’s not elegant to access a web service on the internet using a port other than 80.

NodePort has also several security issues that disallow to use it beyond that for testing goals. 

Therefore, the best solution is to expose the deployment as a \*\*LoadBalancer\*\*, but we will cover that in another post.
