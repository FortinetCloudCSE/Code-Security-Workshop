---
title: "AWS Fundamentals"
linkTitle: "AWS Fundamentals"
weight: 2
---

### Lab 1 Overview

**Click this [Link](https://fortinet.qwiklabs.com/authoring/labs/29) to access the lab!**

The goal of this lab is to, as quickly as possible, get a simple web site running and exposed to the internet.  This website will require some compute resources to run on, exposed to the Internet (inbound/outbound) and permissions to access a centrally managed database.

Application Diagram

![](img/app-diagram.png)

To achieve your goal you will use the public cloud to create resources, download code, grant permissions and finally expose your website to the entire world.  All this will be achieved using the Amazon Web Services (AWS) web console,a web browser and a few simple commands.

Good luck!

### Log into AWS Console

Before we can do anything you will need to get access AWS web console in your browser. The log in details for your lab provided AWS account are on the left hand of the lab.  Each field has a copy link you can use.

Click on the `Open Console` link.

![](img/qwiklabs-lab-details4.png)

Copy/paste the `Username`, `Password` and click `Sign In`.

![](img/aws-login.png)

### Create an Virtual Server

Now that you have access to the AWS Console let's get working!

To get your website working you will need a server where you can run the code.  In a traditional on premise data center you would request a server from your operations team.  In the public cloud you can create your own resources, include servers, without having to ask anyone.

In AWS servers can be created using their `EC2` service. Use the search box and type `EC2` and click on the top returned result. 

![](img/aws-console-us-east-1.png)

In EC2 you can create virtual servers in many different regions around the world. By default, you will be dropped into `us-east-1` region which is located in the United States, North Virginia.  Find `Instances` in the left hand navigation (Below the Heading of "Instance") and click on it to view your currently running virtual server.

Click on `Launch Instance`

![](img/ec2-1(4).png)

Give you new virtual server a name you will remember, keep it safe for work!
Next choose Ubuntu as the operating system you want running in your new virtual server.

![](img/ec2-2.png)

Now we need configure what credentials we will use to access this virtual server once it is up and running.
Select `FortiDevKey` from the drop-down.  This key was created by Qwiklabs and can be used within AWS or from you local machine to access your virtual server.

![](img/ec2-3(4).png)

Finally click on `Launch Instance` to create you brand new virtual server.

![](img/launch.png)

Phew! You now have a brand new virtual server up and running in EC2.  Click on the ID for you new virtual server to view more details.

![](img/aws-ec2-new-server2.png)

### Access your Virtual Server

Next you need to gain access to your new virtual server so you can make it actually do something useful.  Developers often connect to servers using a secure shell (SSH).  AWS offers a simple way to do this called `Instance Connect`.  Instance Connect will allow you to gain a connection to your new virtual server using your browser.  After gaining access you will be able to run commands on the server.

Right-click on the instance name of your new instance and choose `Connect`.

![](img/ec2-4.png)

On the Connect to instance window, keep the default option of `EC2 Instance Connect` and click on `Connect`

![](img/aws-5(2).png)

If successful, you should see a terminal like interface within your AWS Console. Now you are ready to run some commands.

![](img/aws-6.png)

### Download the website code

The code for your new website is stored in git repository hosted on GitHub. Git/GitHub allow developers to collaborate together and share code.  Almost no modern company develops all of their own code. Developers rely on using many other projects to save time and effort while delivering business value.

The command below will download the code to your virtual server

```bash
git clone https://github.com/lacework-community/hello-world.git
```

You can confirm that code is on your server by listing all the file us the `ls` command.

```bash
ls hello-world
```

### Make the site your own

Before you start up your new website let's make a simple change. The default message is `Hello World!`.  The is kind of boring.  Let's update that message to something a bit more fun.

You will be using a program called `nano` to make this change. Below is the command to start `nano` opening the index.js file that runs your website.

```bash
nano ~/hello-world/index.js
```

![](img/aws-ec2-nano-hello-world.png)

Nano tries to be as user friendly as it can be.  You can use your arrow keys to move around, use delete to remove the `Hello World!` text.  You can type your new message as normal. Once you are done making changes use the control key and `o` key, followed by enter to confirm the change.  Finally control 'x' to exit `nano`.

### Install node runtime

Before we can even start up your website you will need to get the Node runtime setup.  Node is a more modern version of the browse language JavaScript.  Many modern websites and services use Node.

The command below will use the Ubuntu built in package management application (apt) to download NodeJs (the Node runtime) and npm (Node's own package manager).

```bash
sudo apt update && sudo apt install -y nodejs npm
```

Notice how many files are installed running just these few commands. Hopefully there aren't any negative side effects of making all these changes.

### Install your website dependencies 

As we mentioned all modern software is built on top of other software.  Your simple website is no exception.  In Node these dependencies are list in a file call `package.json`.  

To see your dependencies run this command. The `cat` command will output the content of a file.

```bash
cat hello-world/package.json
```

![](img/aws-ec2-cat-package.png)

Before you can start your website you will need to install these dependencies.  Luckily you already installed Node package manager `npm`. Run the command below to change directory and install the needed Node packages.

```bash
cd ~/hello-world
npm install
```

![](img/aws-ec2-npm-install.png)

Notice that we only had 3 direct dependencies in our `package.json` file, but we actually added 72 packages. This is because our direct dependencies have their own dependencies, which in turn might yet more dependencies.  Software is built on top of software. Turtles all the way down.

Even more concerning is the warning that there are 8 vulnerabilities found, including 4 of high severity.

Well no time to worry about all of that, you have a website to get up and running!

### Start up your website

To keep your website up and running you will use the `pm2` binary installed in the step above using npm.  The job of `pm2` is to ensure that node binaries are running even if the virtual server gets restarted or your website crashes.

```bash
./node_modules/pm2/bin/pm2 start index.js
```

![](img/ec2-node-started.png)

### Access your brand-new website

Go back to the AWS EC2 Service, click on your instance. You will find the public IP address of that instance and copy it.

![](img/ec2-get-public-ip2.png)

Note: use the copy link and not the 'open address' link

You will need to add the port the website is running on `3000`.

`http://<Your-IP>:3000`

### Hello, is anyone listening?

You might have noticed that when you visited the URL of your newly launched website nothing happened, your browser tab just spun and spun. AWS EC2 be default only allows inbound network connections on port 22, the default port of SSH.  Since your website is not running on port 22 all other inbound traffic was blocked. Next task is to open up some ports to allow inbound traffic to reach your virtual server.

AWS EC2 manages network access via `Security Groups`. Return to AWS EC2, find you EC2 instance, switch to the `security group` tab and click on your security group name.

![](img/aws-ec2-open-security-group2.png)

Ensure you are on the Inbound Rules tab and click on `Edit inbound rules`.

![](img/aws-ec2-lauch-inbound-rules2.png)

You will need click `Add rule` to create a new inbound rule. Then specify the `Protocol` as `TCP`, `Port range` of `1000-6000` and ensure anyone on the internet can access by specifying a `Source` of `0.0.0.0/0`. 

Notice that we opened up way more ports than we need and AWS warns us about allowing all inbound IP addresses. These are just the type of decisions that are now entrusted to anyone with a cloud account.

Anyway... click `Save rules`, let's get this web site up!

![](img/aws-ec2-edit-inbound-rules2.png)

Refresh the URl of your website to see if we can get traffic flowing.

### Wait, that doesn't look right...

Your new website isn't showing your fancy message. Rather it is complaining about an IAM role not being attached.  

![](img/website-no-iam-role.png)

As you might recall from the very beginning we mentioned that the website would need access to a centrally managed database. Access to cloud resources, like databases, is allowed through Identity and Access Management (IAM) IAM has concepts like roles, policies and permissions that control what can and can't be accessed by users and cloud resources.

By default when you create a new EC2 instance there is no IAM role attached.  This means that your virtual machine can not access any other cloud resources at the moment.

![](img/aws-ec2-no-role-defined2.png)

### Attach a new IAM role

To attach a new IAM role to your virtual server click on `Action`, then `Security` and finally `Modify IAM role`.

![](img/aws-ec2-modify-role2.png)

Before you can attach a role you will have to create a new on.  Click on `Create new IAM role` to open a new window in the IAM service page.

![](img/aws-attach-role-before-new-role2.png)

On the IAM Role page you will find a list of all the current roles.  You want a new role that can be attached to your virtual machine so click on `Create role`.

![](img/aws-iam-role-page.png)

There are a few type of roles you can create select `AWS service` and then in the `Service or use case` drop down select `EC2`.  This will allow your to attach this new role to an EC2 virtual server.

![](img/aws-iam-create-ec2-role.png)

Now comes the time to choose which permissions to grant.  Notice that there are over a thousand possible permissions policies you could grant.  Rather than go over all of these trying to find the right one, we will take the simple path and grant `AdministratorAccess`. Choosing the admin role grants more permissions than you need, but ensures that the database access will work. Once again these are just the types of decisions that anyone with a cloud account face everyday.

![](img/aws-iam-grant-admin.png)

Finally the hardest choice you have made all day. What do you name this new role? Pick something easy to remember and click `Create role`.

![](img/aws-iam-create-role.png)

Return to the previous page where you where trying to attache a role.  Click the circle icon, select your new role from the drop down and click `Update IAM role`.

![](img/ec2-attach-new-role2.png)

Finally check your website again. Fingers crossed it all worked.


### Take moment and recap

Here are the high level step you took
* create a new virtual machine
* cloned website code from github
* updated the website code
* installed the Node runtime
* installed node packages via npm
* started the website
* configured the network access
* create a new role and attached it to your virtual machine
* access your wonderful new website

All of this happened without involving IT, development, security, management, operations. 

What could go wrong?

### Take a break already

Once you complete this section of the lab, please take a break and talk amongst your peers about what you learned, we’ll come together once everyone has finished

![](img/break-time-7298ce200c.jpg)