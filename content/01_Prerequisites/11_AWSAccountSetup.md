---
title: "Setup AWS Account" 
chapter: true
weight: 1 
---

# Setting up your AWS account
<!-- TODO - can I get a way to ask for credits too? -->
{{% notice warning %}}
You are responsible for the cost of the AWS services used while running this workshop in your AWS account. We highly recommend you to go to the [request AWS credit page](/030_self_guided_setup/30_request_credit.html) so you can run this workshop without any charge to you.
{{% /notice %}}

1. If you don't already have an AWS account with Administrator access, [create
one now by clicking here](https://aws.amazon.com/getting-started/).

1. Once you have an AWS account, ensure you are following the remaining workshop steps
as an IAM user with administrator access to the AWS account. If you don't have one, 
[create a new IAM user to use for the workshop](https://console.aws.amazon.com/iam/home?#/users$new).

1. Enter the user details:
![Enter User Details](/images/01_Prerequisites/aws-1-create-user.png)

1. Attach the `AdministratorAccess` IAM Policy:
![Attach IAM Policy](/images/01_Prerequisites/aws-2-attach-policy.png)

1. Review the details, then click to create the new user:
![Review User](/images/01_Prerequisites/aws-3-review-user.png)

1. Take note of the login URL and save:
![Save URL](/images/01_Prerequisites/aws-4-save-url.png)
