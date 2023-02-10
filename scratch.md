


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
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release
git clone https://github.com/lightrun-platform/lightrun-aws-workshop.git
cd /lightrun-aws-workshop
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
cd /lightrun-aws-workshop
sudo docker pull openjdk:11


export LIGHTRUN_KEY=812ab864-4e9a-4df0-8603-5eb2702972d8 
export COMPANY=8f1987b4-53e3-4e20-ae47-91f824d5d011

cd /lightrun-aws-workshop && docker build . -t prime-counter

https://www.docker.com/blog/containerizing-a-legendary-petclinic-app-built-with-spring-boot/

AMI with ubuntu "ImageId": "ami-0b0ea68c435eb488d",

[test]({{< ref "/04_ModuleThree_Deploy_Application" >}})


sudo docker build -t prime-counter . --build-arg COMPANY_ID=8f1987b4-53e3-4e20-ae47-91f824d5d011 --build-arg LIGHTRUN_KEY=812ab864-4e9a-4df0-8603-5eb2702972d8
sudo docker run prime-counter