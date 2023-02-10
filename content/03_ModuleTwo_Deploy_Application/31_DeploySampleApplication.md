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

This stack will create an EC2 instance with the relevant ports open, and install the Docker engine which we'll later use to run PetClinic. The stack is [available from here](/cloudformation/stack.yaml) (TODO: Get this link to work).

To deploy it, make sure you have the AWS CLI installed and configured in the region you'd like to run the workshop in. Then download the stack declaration and run the following command from the same folder you downloaded the stack to:

TODO: Add AWS CLI command that deploys stack using the following commands

{{% notice tip %}}
Note that the stack expects you already have an EC2 key pair configured on your account and available on your local machine (as we'll soon use it to connect to the instance). If you don't yet have one, [create it now](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html#having-ec2-create-your-key-pair).
{{% /notice %}}

## Install & Run Spring PetClinic
TODO: This is way too much work. Edit is so the only thing the user needs to configure are his Lightrun org ID and Lightrun secret
### Connect to the instance

We can now connect to the instance in order to install the application - grab your instances Public IPv4 DNS address from the AWS EC2 console, and connect to the instance:

```
ssh -i your-private-key.pem ubuntu@<your-ec2-public-dns-address>
```

{{% notice tip %}}
You might wonder why we're doing these steps using the CloudFormation stack instead of manually. The reasoning is simple - we want to show how Lightrun works like under the hood in a normal AWS-based application, and that includes "baking" the agent into the `Dockerfile` of the application. It requires a couple more steps, but 
{{% /notice %}}

Once the stack is deployed, we can proceed to get our application running.

### Update Dockerfile with Lightrun Agent

First, get the repo from Github:

TODO: make this happen as part of userData in the application instance


```
git clone https://github.com/dockersamples/spring-petclinic-docker.git spring-petclinic
cd spring-petclinic
sudo apt update
```

Proceed to the [Lightrun Web Console](https://app.lightrun.com) and click "Set Up An Agent" using the following configuration, and copy the snippet from step 1:

   ![Lightrun - Developer Observability Platform](/images/03_Deploy_Application/setup-agent.png)

The code should look something like this:

```
LIGHTRUN_KEY=<YOUR-LIGHTRUN-KEY> bash -c "$(curl -L "https://app.lightrun.com/public/download/company/<YOUR-LIGHTRUN-ORGANISATION-ID>/install-agent.sh?platform=linux")"
```

We're going to add this line as part of the Dockerfile, to ensure that the Lightrun agent is downloaded and added to the application at runtime. Edit the Dockerfile:

```
vim Dockerfile
```

And modify the Dockerfile as such:

```
FROM eclipse-temurin:17-jdk-jammy

WORKDIR /app

# Add these two lines to the Dockerfile, swap <YOUR-LIGHTRUN-KEY> for your actual Lightrun key
ENV LIGHTRUN_KEY=<LIGHTRUN_KEY>
RUN bash -c "$(curl -L "https://app.lightrun.com/public/download/company/<YOUR-LIGHTRUN-ORGANISATION-ID>/install-agent.sh?platform=linux")"


# Addition 1: set Lightrun key as an environment variable
ENV LIGHTRUN_KEY=812ab864-4e9a-4df0-8603-5eb2702972d8

# Addition 2: download and install lightrun JVM agent
RUN apt-get update && apt-get install unzip && bash -c "$(curl -L "https://app.lightrun.com/public/download/company/8f1987b4-53e3-4e20-ae47-91f824d5d011/install-agent.sh?platform=linux")"

COPY .mvn/ .mvn
COPY mvnw pom.xml ./
RUN ./mvnw dependency:resolve

COPY src ./src

# Addition 3: supply agent path to application
CMD ["MAVEN_OPTS=-agentpath:agent/lightrun_agent.so", "./mvnw", "spring-boot:run"]
```

Note that there are three changes to the Dockerfile:

1. We're adding your Lightrun key as an environment variable, to be used in step 2.
2. We're downloading the Lightrun Java agent file and configuring it with the aforementioned key.
3. We're supplying the agent path for the application, to allow it to spin up at boot.

## Update pom.xml with debug symbols

Lightrun's Java agent needs to find several symbols, including your project's variables, so that later it would be possible to add actions.

To enable debug symbols for the Lightrun agent, the `maven-compiler-plugin` needs to be installed and configured with the following Java compiler arguments: 

```-g:source,lines,vars
```

Which can be done by editing line 116 of the pom.xml file, right beneath the <build> plugins, in the following way:

```
      <plugin>
      <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>[...]</version>
        <configuration>
          <compilerArgs>
            <arg>-g:source,lines,vars</arg>
          </compilerArgs>
        </configuration>
      </plugin>
```

## Run Spring PetClinic with Lightrun

We'd like the container to now run in the background, while having access to the 






MAVEN_OPTS=-agentpath:/path/to/agent/lightrun_agent.so ./mvnw


### Build and run application

And copy it into the window where your SSH session with the EC2 instance is open. This will download and configure the Lightrun agent inside th 

