---
title: "Lightrun Account Setup" 
chapter: true
weight: 3
---

# Setting up your Lightrun account

TODO: Remove all mention of EKS from workshop, make sure to note we converted it to Docker

Lightrun's developer observability platform offers a fully-manged SaaS solution, which we will use during this workshop.

{{% notice tip %}}
Note that if your topology requires single-tenant, private cloud or on-prem deployments (whether airgapped or not), this workshop still applies to you!
[Contact us](https://lightrun.com/request-a-demo) for more information on how to setup Lightrun in your own environment.
{{% /notice %}}

## Getting Started with Lightrun

1. From your browser, navigate to [Lightrun Cloud](https://app.lightrun.com) and fill the registration form:
{{% notice info %}}
Please make sure to input  "AWS Workshop" as your company name, to ensure your account is configured correctly for this workshop in our backend servers.
{{% /notice %}}

   ![Welcome Screen](/images/01_Prerequisites/lightrun-1-welcome-screen.png)

2. Choose **IntelliJ IDEA** and **Java** as your IDE and language, respectively, then click Next.
Fill in your details, choose a company name and click **Sign Up**, or click **Register with Google** to use your Google account.

   ![Choose IDE & Language](/images/01_Prerequisites/lightrun-2-choose-ide-language.png)

3. Install the Lightrun IntelliJ Plugin by following the on-screen instructions, then click the (now enabled) Next button.
{{% notice tip %}}
Note that there are two installation options - using the [JetBrains Marketplace](https://plugins.jetbrains.com/plugin/16477-lightrun) or via a manual installation. Both will yield the same result, choose whichever you're more comfortable with.
{{% /notice %}}

   ![Install IDE Plugin](/images/01_Prerequisites/lightrun-3-install-IDE-plugin.png)

4. In the next screen, download the **Linux** version of the Lightrun SDK (formerly known as the Lightrun agent) that will be added to our EKS pods later. There is **no need to run the application with the agent** - we'll take care of this later on. 
{{% notice info %}}
Regardless of which operating system you're working on, this workshop focuses on running our Java application on Linux containers inside of EKS pods. Please make sure to only use the Linux version of the SDK to avoid any incompatibilities. 
{{% /notice %}}
   ![Download SDK](/images/01_Prerequisites/lightrun-4-download-sdk.png)

<!-- TODO: Maybe have users who input "AWS Workshop" as the company name have a flag enabling them to go into the console? -->
5. Note that the Next button will be greyed out, requesting that you run your app with the Lightrun SDK in order to continue. This is fine, and we'll take care of it later on.

