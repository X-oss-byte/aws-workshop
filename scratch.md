


Stuff:

Choose instance in template originally (t3.small should do it )

Make sure you have a key, if not one needs to be created for this workshop

Keep LatestAMIId as is

Keep SSHLocation as is

Don't change anything on configure stack options

submit as is

Call it lightrun-aws-workshop

This is an amazon instance, and as such should be access with Amazon AMI creds

Add name to machine (in ClouDFormation template)



Base64:
#!/bin/bash
sudo snap install docker
sudo addgroup --system docker
sudo adduser ubuntu docker
newgrp docker
sudo snap disable docker
sudo snap enable docker
docker run -d -p 8080:8080 springcommunity/spring-framework-petclinic


https://www.docker.com/blog/containerizing-a-legendary-petclinic-app-built-with-spring-boot/


[test]({{< ref "/04_ModuleThree_Deploy_Application" >}})
