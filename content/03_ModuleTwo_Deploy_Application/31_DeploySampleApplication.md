---
title: "Deploy Sample Application"
chapter: true
weight: 1
---

# Deploy Sample Application

We'll be using a simple application that counts prime numbers, but does not print anything to the console until it finishes counting the numbers. This is a "clean-slate" example - in the sense that we'll go from an instrumentation-less application to one that is is instrumented **in real-time and on-demand** by a developer.

This sample Java application will allow us to demonstrate Lightrun's capabilities in a containerized setting, and show that the system is agnostic to the specific deployment pattern we're using - Lightrun works where you do.

## Deploy CloudFormation Stack

The application environment can be deployed as part of a CloudFormation Stack. 

This stack will create an EC2 instance with the relevant ports open, install the Docker engine which we'll later use to run PetClinic, and clone the repo we'll use in this project. The stack is [available from here]([/cloudformation/stack.yaml](https://github.com/lightrun-platform/lightrun-aws-workshop/blob/main/cf-stack.json)).

To deploy it, go to [CloudFormation Console](https://console.aws.amazon.com/cloudformation/) and create a new stack from existing resources, the upload the template above:

   ![Create Stack](/images/03_Deploy_Application/upload-stack.png)

In the next screen, name your stack `lightrun-aws-workshop` and pick the SSH Key Pair you'd like to use for authentication:

   ![Choose Name and Key Pair](/images/03_Deploy_Application/choose-name-keypair.png)

{{% notice tip %}}
Note that the stack expects you already have an EC2 key pair configured on your account and available on your local machine (as we'll soon use it to connect to the instance). If you don't yet have one, [create it now](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html#having-ec2-create-your-key-pair).
{{% /notice %}}

Do not modify any of the options in the next screen, then review your workshop and click "Submit" in the final screen.

After your stack is set up, we'll need to connect to the instance to perform the next steps.

### Connect to the instance

We can now connect to the instance in order to install the application - grab your instances Public IPv4 DNS address from the AWS EC2 console, and connect to the instance:

```
ssh -i your-private-key.pem ubuntu@<your-ec2-public-dns-address>
```

We can now proceed to get our application running with Lightrun.

## Build and run the application
### Examine repo structure

First, go into the folder of our workshop ([the repo](https://github.com/lightrun-platform/lightrun-aws-workshop) has been cloned for you as part of the CloudFormation Stack):

```
cd /lightrun-aws-workshop
```

This folder contains the following:

1. Our sample application, called `PrimeMainMR.java` 
2. A Dockerfile that containerizes it
3. A copy of our CloudFormation stack

Let's add Lightrun to the application and run it!
### Build & run the app (with Lightrun)

All that's missing now are your Lightrun credentials - proceed to the [Lightrun Web Console](https://app.lightrun.com) and click "Set Up An Agent", then use the following configuration, and copy the snippet from step 1:

   ![Setup Lightrun Agent](/images/03_Deploy_Application/setup-agent.png)

The code should look something like this:

```
LIGHTRUN_KEY=<YOUR-LIGHTRUN-KEY> bash -c "$(curl -L "https://app.lightrun.com/public/download/company/<YOUR-LIGHTRUN-ORGANISATION-ID>/install-agent.sh?platform=linux")"
```

We're going to need two parameters here - your Lightrun key and organisation ID: we'll need them in order to "bake" the Lightrun agent into the container. Replace the placholders in the following command with these parameters and build the app:

```
sudo docker build -t prime-counter . --build-arg COMPANY_ID=<YOUR-LIGHTRUN-ORGANISATION-ID> --build-arg LIGHTRUN_KEY=<YOUR-LIGHTRUN-KEY>
```

After the image finishes building, we'll need to run the application:

```
sudo docker run prime-counter
```

The application is now running! Note that it does not emit anything, which is fine - we'll instrument it using Lightrun in just a moment.
