---
title: "Deploy Sample Application"
chapter: true
weight: 1
---

# Deploy Sample Application

We'll be using the [Spring PetClinic](https://spring-petclinic.github.io/) sample Java application, and specifically [this containerized version](https://github.com/dockersamples/spring-petclinic-docker) of it. 

This is a sample application designed to show how the Spring stack can be used to build simple, but powerful database-oriented applications - and will allow us to demonstrate Lightrun's capabilities in the JVM world using a containerized application. Please refer to (TODO: Add link) the "Getting Familiar with Our Sample Application" section to learn more about Spring PetClinic.

## Deploy CloudFormation Stack

The application environment can be deployed as part of a CloudFormation Stack. 

This stack will create an EC2 instance with the relevant ports open, and install the Docker engine which we'll later use to run PetClinic. The stack is [available from here](/cloudformation/stack.yaml).

To deploy it, make sure you have the AWS CLI installed and configured in the region you'd like to run the workshop in.
Then download the stack declaration and run the following command from the same folder you downloaded the stack to:

TODO: Add AWS CLI command that deploys stack using the following commands

{{% notice tip %}}
Note that the stack expects you already have an EC2 key pair configured on your account and available on your local machine (as we'll soon use it to connect to the instance). If you don't yet have one, [create it now](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html#having-ec2-create-your-key-pair).
{{% /notice %}}

## Install & Run Spring PetClinic

We can now connect to the instance in order to install the application - grab your `<AWS-EC2-Public-IPv4-DNS>` address from the AWS EC2 console, and connect to the instance:

{{% notice tip %}}
You might wonder why we're doing these steps using the CloudFormation stack instead of manually. The reasoning is simple - we want to show how Lightrun works like under the hood in a normal AWS-based application, and that includes "baking" the agent into the `Dockerfile` of the application. It requires a couple more steps, but 
{{% /notice %}}

Once the steack is deployed, we can proceed 

