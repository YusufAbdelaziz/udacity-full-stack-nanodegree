# Deployment Process

## Lesson 1 : Foundations of Deployment Process.

- Why deployment process is important ?
    - Knowing how to code is not enough to get your application in the hand of users. Understanding the deployment process is important in order to:
        - Make your portfolio of projects available online to recruiters and users.
        - Avoid overpaying for services you don't need.
        - Secure the private keys of APIs. Often these APIs might be paid services and you need to ensure you are not sharing these keys in public.
    - The great thing about learning deployment tools is that the knowledge transfers well to different cloud providers.
- What does deployment process involve ?
    - The deployment process involves the following :
        - Determining what cloud resources are needed.
        - Preparing the code for production and deploying it for the first time.
        - Creating a deployment process that we’ll automate using a CI/CD pipeline.
        - Documenting your process and iterating on it.
    - The main goal of creating a pipeline is to automate the deployment process such that we can launch our web sites so users are cable of using them.
    - To create a pipeline, we need a set of skills like knowing how to deploy, command-line interface and scripts. All of these skills are discussed throughout the course.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled.png)
        
    - Some new terms :
        - **Pipeline:** A series of automated steps (Command-Line Interface commands) that simplify the testing, building, and deployment of code. While this might seem abstract for the moment, it will make more sense as we progress in this course.
        - **Cloud Provider:** Companies that offer servers for rent and hosting services that provide flexible computing.
        - **AWS:** Amazon Web Services is the dominant player in the Cloud Provider industry.
- What is the difference Continuous Integration, Continuous delivery and Continuous Deployment ?
    - Click [here](https://semaphoreci.com/blog/2017/07/27/what-is-the-difference-between-continuous-integration-continuous-deployment-and-continuous-delivery.html).
- Course outline.
    1. Configuring a Production Environment:
        1. Database.
        2. Web server
        3. Web Hosting
    2. Interacting with Cloud Services
        1. AWS CLI
        2. Elastic Beanstalk CLI.
    3. Writing Scripts for Web Apps
        1. Build Scripts
        2. Test scripts
        3. Shell Scripts
    4. Configure and Document a Pipeline
        1. CircleCI CI/CD
        2. Runbooks
        3. Architecture Diagrams
    5. Hosting a Full a Full Stack App
        1. Automated Pipeline.
        2. Typical Full Stack Application
- How benefits from deployment ?
    - Everybody ! The product managers, designers, developers and customers.
    - **Product managers and designers** benefit from a faster feedback loop with customers.
    - **Developers** benefit from a more streamlined workflow with fewer manual interventions on their part.
    - **Customers** benefit from receiving features faster and getting up-to-date software.
- When to automate deployment?
    - When automating deployments, almost anything can be done. However, we should take careful considerations in order to avoid potential errors. Think about the following questions:
        - **Are you confident that the application is well tested?** If your test does not cover properly the core features of your application maybe you want to remediate that issue before moving to automated deployments.
        - **Do you need to comply with regulatory procedures that could be impacted by a deployment?** Generally, it would be advisable to avoid automated deployments until you have a process in place to audit whether you comply with regulations in your industry.
        - **Does everything need to be automated?** Automation is great at saving time. However, like other pieces of software, an automated deployment needs maintenance. It's good to slow down and automate where you need it instead of trying to automate at all costs.
- What tools we need for the course ?
    - Git
    - Terminal
    - Browser
    - AWS CLI
    - Elastic Beanstalk CLI
- New terms
    - **DevOps:** A collection of techniques trying to bridge the gap between development and operations.
    - **Pipeline**: A series of automated steps that to simplify the testing, building, and deployment of code.
    - **CI/CD**: Continuous Integration / Continuous Delivery (sometimes Deployments). Subparts of a pipeline dedicated to integrating code, delivering it, and deploying it.
    - **Cloud Provider**: Companies that offer rentable servers and hosting services that provide flexible computing.
    - **AWS**: Amazon Cloud Services is the dominant player in the Cloud Provider industry.
    - **DevSecOps**: Adding Security to the DevOps keyword aims at promoting the importance of taking an active approach to security.
    - **Cost Operations:** Taking an active approach to controlling cost saves a lot of money in the long run.
    - **Production**: The live applications our customers use to connect to our application.
    - **Feedback loop**: A generic reference to the time it takes to receive feedback on a new feature from customers.
    - **Manual Check**: A step in a pipeline that requires human approval before going to the next step.
    - **Regulations**: A series of rules that must be complied with.
    - **Agile**: a development methodology that prioritizes iteration over the heavy process.
    - **EC2**: Amazon Elastic Compute Cloud, is the service amazon provides for renting servers on its cloud platform.
    - **Jenkins**: One of the first CI/CD platforms and one of the most popular to this day.
    - **Terraform:** A programming language that provides infrastructure as code capacities.

## Lesson 2 : Setting up a Production Environment.

- Lesson outcomes.
    - In this lesson, we will learn about the different components of a production environment. We will cover the following topics:
        - How experts approach a new application that they are tasked with deploying.
        - Deploy a database using AWS RDS.
        - Deploy a web server using AWS Elastic Beanstalk.
        - Deploy a web UI using AWS S3.
- Why setting up a production environment ?
    - Production environment is a set of services that makes your application available to end user. This is where you customers are going to use your application and where new features will be made available on a regular basis.
- What are we looking at when we choose production environment ?
    - Balance features and flexibility :
        - Renting a server takes time in configuring it.
        - On the other hand, you might use cloud provider like Netlify or Vercel who configures and manages it for you but with less features and flexibility on the configurations.
    - Environment Variables :
        - Environment Variables need to be set easily.
        - Allows you to hide sensitive information like API keys or database connection strings.
    - Command Line Interface :
        - We need a CLI for configuration.
        - CLI allows you to use a CI/CD (continuous integration / continuous deployment) pipeline easily.
    - Easy to use Yet Configurable :
        - You need easy menus to navigate between to accomplish your deployment tasks.
        - However, you still need to have enough configuration options to satisfy your deployment needs.
- What are we going to use in this course ?
    - AWS Relational Database Service (RDS). It has many databases in many SQL variances and also provide easy management tools for you to use for production set-ups.
    - AWS Elastic Beanstalk (EB). Used to host a web server and it’s used as an orchestration service which supports running servers in multiple languages and different runtimes including Go, C# and NodeJS.
    - AWS Simple Storage Service (S3). It’s using for configuring the hosting in general and it’s great for hosting files.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%201.png)
        
- How to approach Production Environment configuration like an expert ?
    - First things first, you need to check the `package.json` file and understand which framework is used.
    - You should do a research to understand the high level ideas behind the framework. You can do so by reading the docs of the framework.
    - Try to explore the communication that the application your deploying is doing. It might be connected to an external API or a database.
- What do we need to configure a database on AWS RDS ?
    - You need to know that there’re many features in RDS and you might not use all of them, so a simple tutorial would be enough to get you on the track.
    - We need these components to make sure our configuration is good enough :
        - **Backups**: A copy of your database can be made on a regular interval to avoid losing data if something goes wrong.
        - **Public or private**: A database could be made available on the open web, or only within a private Internet network.
        - **Multiple Availability Zones:** You can configure a database to be physically in multiple data-centers.
        - **Server specs:** You can choose the size of the server.
- How to configure a database demo ?
    - You can visit your AWS console.
    - Search for the service you want to use, in this case it’s **RDS**.
    - Create a new database.
    - You’d find a bunch of features like database engine type, visibility (public or private), availability (in a single zone or multiple zones), instance configuration (memory size).
    - Click on **Create database →** You can use the standard create or easy create, we’d go for standard as we want to specific configuration. Please be careful for the PostgreSQL version you’re using and make sure it’s compatible with the Node version you’re running.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%202.png)
        
    - Next, use the **free tier** as we don’t need much resources for the course.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%203.png)
        
    - You can configure the DB instance identifier, master username and password in settings section. Make sure that you remember the credentials as we’d use them for connection.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%204.png)
        
    - Make sure you’re using **db.t3.mico** or the smallest instance configuration possible.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%205.png)
        
    - Now for the **Connectivity** section, make it public by selecting Yes in the **Public Access** part.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%206.png)
        
    - We’ll leave the remaining configurations and create the database. Wait a little bit and you’d see it available in the RDS list.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%207.png)
        
    - Unfortunately, you can’t connect your NodeJS app with the database up till this point, so we need to pay a visit to the **VPC Security Group (Thanks for the instructor May Hassan for point out this issue for us** 😊**).**
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%208.png)
        
    - You’ll need to select the security group and add an inbound rules by clicking on **Edit inbound rules.**
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%209.png)
        
    - Add a rule and set its type as **All Traffic** and at the source write **0.0.0.0/0** and save the rules. Note that the source type will be **Anywhere** initially but ignore it and it will turn into **Custom**
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2010.png)
        
    - And we’re done, let’s go to the Node app to connect our database.
- How to connect a Node app to the database we created ?
    - We’ll use **[Sequelize](https://sequelize.org/docs/v6/getting-started/)** package which is an ORM used for different types of database engines like Oracle, Postgres, MySQL, and more.
    - An [ORM](https://stackoverflow.com/questions/1279613/what-is-an-orm-how-does-it-work-and-how-should-i-use-one) stands for Object Relational Mapping which is a technique to let you query and manipulate data from database using an object-oriented paradigm.
    - So you’re creating models (which is the tables) and the columns of each table and their corresponding types.
    - You need to install it via →  `npm install --save pg pg-hstore`
    - It’s better to check the docs but we’d take a brief look on the code provided in the class
        
        ```tsx
        const express = require("express");
        const { Sequelize, DataTypes, Model } = require("sequelize");
        const bodyParser = require("body-parser");
        const cors = require("cors");
        const config = require("./config");
        const path = require("path");
        const contacts = require("./contacts");
        
        const app = express();
        
        app.use(express.static("public"));
        app.use(cors());
        
        const sequelize = new Sequelize(
        		"postgres://user:pass@example.com:5432/dbname"
        );
        
        class User extends Model {}
        
        User.init(
          {
            id: {
              type: DataTypes.STRING,
              primaryKey: true,
            },
            name: {
              type: DataTypes.STRING,
              allowNull: false,
            },
            email: {
              type: DataTypes.STRING,
            },
            avatarURL: {
              type: DataTypes.STRING,
            },
          },
          {
            sequelize,
            modelName: "User",
          }
        );
        
        app.get("/", (req, res) => {
          res.sendFile(path.join(__dirname + "/client/index.html"));
        });
        
        app.use((req, res, next) => {
          const token = req.get("Authorization");
        
          if (token) {
            req.token = token;
            next();
          } else {
            res.status(403).send({
              error:
                "Please provide an Authorization header to identify yourself (can be whatever you want)",
            });
          }
        });
        
        app.get("/contacts", async (req, res) => {
          const users = await User.findAll();
          res.send(
            users.map(({ dataValues }) => ({
              id: dataValues.id,
              name: dataValues.name,
              email: dataValues.email,
            }))
          );
        });
        
        app.delete("/contacts/:id", (req, res) => {
          res.send(contacts.remove(req.token, req.params.id));
        });
        
        app.post("/contacts", bodyParser.json(), (req, res) => {
          const { name, email } = req.body;
        
          if (name && email) {
            res.send(contacts.add(req.token, req.body));
          } else {
            res.status(403).send({
              error: "Please provide both a name and an email address",
            });
          }
        });
        
        app.listen(config.port, async () => {
          try {
            await sequelize.authenticate();
            console.log("Connection has been established successfully.");
            console.log("Server listening on port %s, Ctrl+C to stop", config.port);
            await User.sync();
            contacts.defaultData.contacts.forEach((contact) => {
              User.findOrCreate({ where: { id: contact.id }, defaults: contact });
            });
          } catch (error) {
            console.error("Unable to connect to the database:", error);
          }
        });
        ```
        
    - Things to note :
        - You can initialize the Sequelize object using three different ways, but we’d use one of them (the others are in the docs):
            
            `postgres://user:pass@example.com:5432/dbname`
            
            You may change `postgres` into `mysql` in case of using MySQL and same thing stands with other DB engines. Note that `dbname` is usually called `postgres`.
            
        - Our User model extends from Model class which is used to create CRUD methods out of the box for the model we’re identifying in the `init` method.
        - At `app.listen`, we call `squelize.authenticate` method to test the connection between the `Sequlize` object and the database.
    - And voilà ! you’re done 😃.
- What is Elastic Beanstalk ?
    - Elastic Beanstalk is a free service that lets you easily run applications on web servers. It offers the following advantages:
        - **Free**: You only pay for the servers that elastic beanstalk uses. The extra tools are free of charge.
        - **Pre-built Environments**: Most major programming languages are supported out of the box.
        - **Simple Server Management**: Security updates and system upgrades are done for you.
        - **Easy Scaling**: If you need to provision extra servers, you can quickly change your configuration.
- What does Elastic Beanstalk use ?
    - **Elastic Compute Cloud (EC2)**: Used for hosting servers. However, Elastic Beanstalk preconfigures the servers.
    - **Simple Storage Service (S3)**: Used for storing application code and sending it to other servers.
    - **Simple Notification Service (SNS)**: Provides a way to notify you of events inside the environment.
- How to configure Elastic Beanstalk environment?
    - Search for “Elastic Beanstalk” and go to the dashboard.
    - Press on “Create a new Environment”
    - Select the “Web Server Environment”
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2011.png)
        
    - After that you can define the app name and app tags. However, app tags are optional and used to distinguish each environment from the other in case you have environments with similar names.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2012.png)
        
    - Go to platform section and choose the platform you’re using and for our case it’s NodeJS.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2013.png)
        
    - Lastly, you can upload the application code directly or select a sample code for the sake of experimenting.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2014.png)
        
- How to configure environment variables in a Elastic Beanstalk environment ?
    - Go to the environment you’ve created and click on Configuration and Edit the software configurations.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2015.png)
        
    - Scroll down and add any environment variables you want
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2016.png)
        
- What is S3 ? What are the pros and cons of the S3 ?
    - While we could use a web server that we set up on Elastic Beanstalk to serve HTML files, there are other options like AWS S3 for this purpose. It is possible that you have already heard about S3 since it is a really popular service. Here are some of its strengths:
        - Inexpensive
        - Foundational service on AWS upon which many other services are built
        - Global and available in all regions
    - S3 Stands for Simple Storage Service. It is AWS's file storage service. S3 is different from a hard drive. It can be referred to as **object-based storage**.
    - By object-based, we mean that the file name is a key and the value of that key is the actual content of the file. Metadata, which includes information about the object, such as owner, date created, and other important information, is also stored.
    - S3 is a global service, which results in unique buckets or unique file names.
    - In this course, we’ll use S3 to upload/update **static websites**.
    
    ## **Limitations and Strengths of S3**
    
    - **S3 can't run a file system:** S3 is just meant to serve files and cannot act as an operating system. It cannot be a complete server.
    - **Fine-grained permission system:** We can control the access to the bucket with Access Control List (ACL) policy, which is a file written in JSON or yml.
    - **Configurable for web hosting:** We can serve static files like HTML and CSS on S3.
    
    ## **New Terms**
    
    - **Access Control List (ACL) policy.** This is a file written in JSON or yml that can be used to grant or restrict access to an S3 bucket. This is also used in other AWS services.
    - **Object Storage**: Storage that behaves differently than a file system organizing files as objects.
    - **Metadata**: Data about data. Includes information about files such as owner, date created, and other important information.
    - **S3 - Simple Storage Service**: AWS's file storage solution that drives many different connections between AWS services.
    
- How to deploy a static website with S3 ?
    - Go to AWS S3 and create a new Bucket. You should define a unique bucket name
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2017.png)
        
    - Disable ACL and allow public access
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2018.png)
        
    - You can safely allow public accesses in case of static website hosting and you can now create the bucket.
    - You can enable ACL (Access Control List) from the bucket setup or from the **Permissions** tab.
    - In this case, you need to add **-acl public-read** flag to your deploy command.
    - After that, go to **Properties** tab and scroll down to **Static website hosting.** Click on **edit** and enable the static website hosting and provide the index document (which is usually index.html).
    - Unfortunately, the bucket can be written by anyone and we want only to allow reading the bucket aka displaying the website. Head to **Permissions** and go to **Bucket policy** click on **edit** and add this JSON policy to prevent writes operations on your bucket. Remember to replace bucket name with your real bucket name.
        
        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Sid": "PublicReadGetObject",
                    "Effect": "Allow",
                    "Principal": "*",
                    "Action": [
                        "s3:GetObject"
                    ],
                    "Resource": [
                        "arn:aws:s3:::bucketname/*"
                    ]
                }
            ]
        }
        ```
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2019.png)
        
    - Click on the bucket and upload the static files (HTML, CSS, assets, etc.) which usually exist inside the `build` folder.
    - Go back to properties and scroll down to static website hosting and you’d see the url you’re going to access.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2020.png)
        
    - For more info on user guide of S3, click [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html).

## Lesson 3 : Interact with Cloud Services via CLI.

- Lesson outcomes.
    - We will learn the following things in this lesson:
        - How to use a CLI and read its documentation
        - How to use the AWS Beanstalk CLI
        - How to use the AWS CLI to update an S3 bucket
- Why would we bother ourselves with interacting with cloud services CLI ?
    - Using AWS console is not a normal way to deploy an app, and we need to interact with a CLI to make the process as easy as possible so we can prevent the overhead of navigating between consoles.
- What can we do with cloud service CLI ?
    - We can deploy code to Elastic Beanstalk or update an HTML file in S3.
    - Check the health of the app by checking if it responses properly or check the logs of the app.
    - We can also check general information of the app.
    
- When should we use AWS console or the CLI ?
    
    
    | Console | CLI |
    | --- | --- |
    | When learning a new service. | Inside CI/CD pipeline. |
    | Prefer a visual environment | Writing a script. |
    | Doing an action you don’t do often like using a DynamoDB that you’ve not used before. | Doing repetitive tasks like deploying an application |
- How experts approach interacting with cloud services ?
    - CLI expertise comes with lots of practice! There’s a lot of commands, but you can practice each by reading the docs.
    - All you need to do to get familiar with AWS CLI is :
        - Read the docs.
        - Practice with various CLI commands.
        - Find things to automate.
    - You can find AWS CLI reference from [here](https://docs.aws.amazon.com/cli/latest/index.html).
- Why does we have separate CLI for Elastic Beanstalk from AWS CLI.
    - The reason for that is EB CLI has easier commands to interact with EB.
- What is the difference between AWS CLI and EB CLI ?
    
    ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2021.png)
    
- What can we do with EB CLI ?
    - We can create environment.
    - Deploying new versions of the code.
    - Check the logs for each environments.
- EB CLI basics.
    - Click **[here](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-getting-started.html)** to see basic commands of CLI.
    - `eb create` allows you to create a new EB environment
    - `eb deploy` will deploy your application to Elastic Beanstalk
    - `eb use` will link a local repository to an existing EB project
    - `eb health` will give you information about the health of your application
    - `eb open` will open the EB console in your favorite browser
    - `eb status` **THIS IS A SUPER USEFUL** command. The reason for that is you can know all the info related to the environment.
        
        ```yaml
        (.ebcli-virtual-env) PS C:\Users\yusse\Documents\Study\reactnd-contacts-server> eb status
        Environment details for: test3-dev
          Application name: test3
          Region: us-east-2
          Deployed Version: app-19cc-220927_231810785788
          Environment ID: e-xkxw4xgqgm
          Platform: arn:aws:elasticbeanstalk:us-east-2::platform/Node.js 12 running on 64bit Amazon Linux 2/5.5.6
          Tier: WebServer-Standard-1.0
          CNAME: test3-dev222.us-east-2.elasticbeanstalk.com
          Updated: 2022-09-27 21:19:32.900000+00:00
          Status: Ready
          Health: Green
        Alert: Your environment is using a deprecated platform branch. It might not be supported in the future.
        ```
        
- What is Identity Access Management (IAM) keys and how to add a user?
    - Identity access management keys can identify you to the AWS CLI. These keys hold associated permissions to give access to your account.
    - Type IAM in the search bar.
    - Click on users and click on “Add User”.
    - Type the user name, and define whether the user is going to interact with CLI only or also with the AWS console.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2022.png)
        
    - After that you should define the set of permissions you can add to the newly created user. You might first create a group of permission to which you include your new user.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2023.png)
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2024.png)
        
    - We’ve created a user with admin permissions, this means a complete access to the AWS account so please be aware of what you’re doing.
    - You can create the group and add your user to that group and continue creating the user.
    - You can then use the access id key and secret key to configure **`eb`** with **`eb init`**
- What happens when we deploy code to EB via CLI ?
    1. The application is packaged into a zip file.
    2. The zip file is uploaded to an S3 bucket.
    3. The bundled zip is then downloaded onto EB servers.
    4. The servers are then updated with the new version of the code.
- How to deploy to EB via CLI ?
    - First things, you need to initialize `eb` using `eb init` (in case you haven’t).
    - You may use the access id key and secret key you got while creating a new IAM user.
    - Create an environment to deploy to using `eb create env-name` you should find the environment in Elastic Beanstalk dashboard.
    - Edit `config.yml` and include the environment you created.
        
        ```yaml
        branch-defaults:
          lesson-2-exercise-1:
            environment: my-env # Environment name
            group_suffix: null
        deploy:
          artifact: ./app.zip # The zipped file of the project.
        global:
          application_name: reactnd-contacts-server # app name
          branch: null
          default_ec2_keyname: vockey
          default_platform: Node.js 16 running on 64bit Amazon Linux 2
          default_region: us-east-1 # WATCH OUT THE REGION !!!!!!!
          include_git_submodules: true
          instance_profile: null
          platform_name: null
          platform_version: null
          profile: eb-cli
          repository: null
          sc: git
          workspace_type: Application
        ```
        
    - In case the environment already exists in the Elastic Beanstalk dashboard, you can just use this command `eb use env-name` to link the local CLI to the environment to which you’re deploying the code.
    - Try to zip the build folder you created with build script and deploy that zip file. Notice that we added a deploy key with an artifact of the zipped file location. Head down to know how to create a zip file.
    - Run `eb deploy` command and you can see your code deployed to the environment automatically. This would deploy the zip file which basically contains the build folder.
    - **IMPORTANT NOTE** : For some weird reason, you may not find the environment you created in the region from which you create the environment, so re-check the `config.yml`file.
- How to set environment variables with EB CLI ?
    - Use this command → `eb setenv VAR1=Banana VAR2=Apple`
    - Please be careful with the spaces, don’t add any spaces before or after the equal sign.
- How to terminate EB environment and application ?
    - You can run this command `eb ternminate --all` to terminate the app and its environment.
- What is blue/green deployments ?
    - Blue/green deployments enable us to send our new code to half of the servers in our environment and keep the other half for accepting users and traffic. When the first half is done deploying we then proceed to deploy the new code on the second half.
    - For more info, click [here](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.CNAMESwap.html).
- How to create a zip file with Linux or Windows ?
    
    ### Linux
    
    1. In case you’re using Linux, you can install zip utility using :
        
        `sudo apt install zip unzip`
        
    2. After that, run `zip -r {filename.zip} {foldername}`.
    
    ### Windows
    
    1. For windows, you need to install 7-Zip from [here](https://www.7-zip.org/).
    2. Add the installation folder to the path of environment variables of windows.
    3. Restart the terminal or VSCode and type `7z`. Try to explore the various options of the command.
    4. Use the following command to create a zip file
    `7z a -tzip {yourfile.zip} {yourfolder}`
    5. You can basically go to the project folder you want to zip, and run the following command to zip your project
        
        `7z a -tzip myproject.zip .` The `.` means that you want to archive the current folder.
        
- What is a runbook ?
    - A runbook is a set of ordered list of steps. It explains in simple terms how to take actions and what each action mean. You don’t have to understand perfectly how each action works internally, it’s just enough to know how it works.
    - An example of a runbook is the above toggle in which we clarify how to archive a folder.
    - You need to check the runbook you’ve created so you’re pretty sure that the steps are doing what they supposed to do.
- What can we do with S3 CLI ?
    1. **Create new buckets**: Creating a new bucket with the S3 CLI is quite fast!
    2. **Upload files to a bucket:** The S3 CLI lets us copy local files to a bucket.
    3. **Set permissions:** We can set access policies on a bucket via the CLI.
- What are the challenges we face when hosting a static website and updating its content ? What is Cache-Control ?
    - Some browsers will effectively cache files (save them locally to load them faster). This means that, in some situations, to update the content of our website we will need to specify with S3 some cache HTTP headers.
    - **Cache-Control:** HTTP headers telling the browser how long it needs to cache certain files. To ensure browsers take the new content of our HTML files, we will sometimes need to force the browser to revalidate the content of the files in S3.
    - For more info about cache headers and possible directives we can include to the response, click [here](https://www.imperva.com/learn/performance/cache-control/).
- How to configure AWS command line correctly ?
    - So I might be dumb or something because I made a mistake by setting the credentials (access key id and secret access key) globally so AWS CLI was always checking these credentials ignoring the ones in the local files.
    - So to check if you did what I did, try to type `echo $AWS_SECRET_ACCESS_KEY` and  `echo $AWS_ACCESS_KEY_ID`.
    - So if that is the case, you need to remove them in case you want to use `aws configure`
    - To remove the global credentials you have two options :
        - Go to Registry Editor and remove the global keys and you need to restart your device after that.
            
            ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2025.png)
            
        - Or you can use `REG delete HKCU\Environment /F /V key-name-in-registry` command in case you’re too lazy like me 🥲.
    - To see the credentials you added via running `aws configure` command, you can head to the home directory by writing `%UserProfile%` in the search bar of windows 10 and head to `.aws`.
    - You will find two files, `config` and `credentials`.
    - Useful links :
        - **[Configuration and credential file settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)**
        - [Configuration Quick Setup](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html).
- How to upload local files to a S3 bucket? How to download files from S3 bucket?
    - You first need to check if the bucket to which you want to upload your files exists using `aws s3 ls` .
    - Uploading or downloading using the same command, but you need to define the destination to which your forwarding the files.
    - So if we want to upload the local folder to its associated bucket, use this command
        
        `aws s3 cp ./build s3://bucket-name --recursive` You need the recursive flag in case you’re also uploading folders besides files.
        
    - You might need to add `--acl public-read` flag in case you’ve enabled ACL in your bucket.
        
        `aws s3 cp --recursive --acl public-read ./www s3://reactnd-contacts-complete` 
        
    - If you want to download files from the bucket, just flip the destination and source
        
        `aws s3 cp s3://reactnd-contacts-complete ./build --recursive`
        
    - Note that the dot `.` means the current path from which you’re writing the command. In this case we want the build folder of the current directory (we’re uploading the contents of the build folder to be precise). This would upload the contents
    - For more info and examples about `cp` command, click [here](https://www.middlewareinventory.com/blog/aws-s3-cp-examples-how-to-copy-files-with-s3-cli-devops-junction/).
    
- Edge Cases
    
    ## **`eb use` does says ERROR: NotFoundError - Environment "env-name" not Found.**
    
    If you are having issues having the EB CLI connect to your environment try running `eb init`. This will ask you a series of questions in order to connect the Elastic Beanstalk to the right application and AWS region. Read the **[documentation](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb3-init.html)** about the command if you are unsure what to answer
    
    ## **Connecting your AWS account to Elastic Beanstalk CLI**
    
    If you are having issues connecting your account to the Elastic Beanstalk CLI, try following **[this tutorial](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-configuration.html)** provided on the EB documentation site.
    
    If you need assistance in generating AWS keys, take a look at **[this tutorial](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console)** to generate a user with programmatic access.
    
    ## **An S3 hosted website does not display updated content after deploying new application code**
    
    In some cases, it is possible that your browser is trying to cache the content of a webpage in order to provide you with a better user experience. This can cause some issues with displaying the updated version of a website. You can try running the following command in order to force websites to uncache and revalidate the content on a website. Make sure to replace BUCKET_NAME with the name of your bucket.
    
    ```
    aws s3 cp --acl public-read --cache-control="max-age=0, no-cache, no-store,
    must-revalidate" ./build/index.html s3://BUCKET_NAME/
    ```
    

## Lesson 4 : Write Scripts for Web Apps.

- Lesson Outcomes
    
    ## **Why write scripts?**
    
    - Scripts are the foundation of automation. They enable you to **repeat actions** in a predictable way, **solve complicated problems** that would take multiple CLI commands to fix, and even **migrate data** from one database to another.
    - As an application grows and becomes more mature, you will gradually adapt your scripts and they will grow with the application. You will need to maintain them as you maintain your code in order to make your application well-organized and easy to work with.
    
    ## Lesson Outcomes
    
    - We’ll mainly learn :
        - How experts approach **writing scripts**
        - **Deployment scripts** in order to deploy the application
        - **Build Scripts** in order to package and build applications
        - **Test Scripts** in order to catch potential bugs in an application
- How experts approach writing scripts ?
    - Firsts things first you want to balance between customization and maintenance.
    - Your scripts should satisfy the needs of the project. It shouldn’t be overcomplicated so you can maintain it later.
- What should we do when creating a script ?
    1. Start from the commands they already know.
    2. Look for pre-built scripts (like Angular build).
    3. Add simple scripts directly in the `package.json`
    4. Add complicated scripts inside a script file (for ex: deploy.sh) that is called from the `package.json`. 
- How to know if my script is complex ?
    - It is hard to draw a line on what makes a script simple or complex, but here are some indications that **your script is getting complex**:
        - You are passing two or more options to the CLI commands
        - You are using multiple CLI tools in the same script (for example: calling both `eb` and `s3`)
        - You are using multiple subsequent commands
        - The commands are long and hard to read
    - Bash scripts are example of complex scripts. In case you have a long and complex command, then it’s a good idea to create a bash script. You can create a file with `.sh` extension like `example.sh` and include the commands you want to execute. It’s a convention that you create a `bin` folder and add the bash files to it.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2026.png)
        
    - This is out of the scope of the course, however you can check [this](https://cs.lmu.edu/~ray/notes/bash/) intro to bash, and [this](https://www.linode.com/docs/guides/intro-bash-shell-scripting/) to know more about the syntax of bash scripts.
- What are Shell, Bash, and PowerShell ?
    - **Shell** is a program that processes commands and returns the output. It is one of the most popular terminal programs out there.
    - **Bash (Born again shell)** is similar to Shell, with more advanced features. It is available by default on most Mac and Linux systems.
    - **PowerShell** is a terminal program available on Windows. It has similar features to Shell and Bash but the syntax is different.
- Why should we add our scripts to `package.json` file in JS Apps?
    - JavaScript developers mostly use **npm** or **yarn** as package managers. These two package managers also provide an easy way to execute scripts that are defined in the script section of the `package.json` file. This is why we will always add all our scripts directly into the script section of the `package.json`.
- What is a deployment script ?
    - It’s a command or a series of commands that will update your application.
- What should we consider when we create a deployment script ?
    1. Understand what you are deploying
    2. Read the documentation about the platform you are deploying to. This will help you identify which script commands you can call inside your script.
    3. Add your script to the `package.json` script section. THIS is really important step, so you can call the script via npm or yarn.
    
    ### **Further Reading**
    
    - [Scripts inside package.json](https://krishankantsinghal.medium.com/scripting-inside-package-json-4b06bea74c0e): This is a great small read to understand more in-depth how you can add scripts to your `package.json`.
    - [npm-run-all](https://www.npmjs.com/package/npm-run-all) and [concurrently](https://www.npmjs.com/package/concurrently) are simple npm packages that give you additional tooling when you want to run more complex scripts from your `package.json`.
- What is Vercel ?
    - [Vercel](https://vercel.com/) is a deployment platform centered around developers and easy deployments.
- What is Kubernetes or K8s ?
    - [K8s](https://kubernetes.io/) is an open source container orchestration platform that automates many of the manual processes involved in deploying, managing, and scaling containerized applications.
- How to create a shell script and call it from `package.json`?
    - You first need to create a bin folder, and inside that folder you can add your scripts, for example `deploy.sh`.
    - After that, you can include any set of commands like :
        
        ```bash
        aws s3 cp ./build s3://reactnd-contacts-complete --recursive
        ```
        
    - You can add the script which runs the shell script as follows :
        
        ```json
        // package.json
        
        "scripts" : {
        	"deploy" : "bash ./bin/deploy.sh"
        }
        ```
        
    - You can run `npm run deploy` and the build folder contents are uploaded to your S3 bucket.
    - In Unix-based OS (macOS or Linux) you might need to change the mode of access of the bash script file using **[chmod](https://www.computerhope.com/unix/uchmod.htm)** command. So you’d need to change the mode first and then run the command `chmod +x ./bin/deploy.sh && ./bin/deploy.sh` . Notice that `+x` makes our bash script executable, so we’re changing the access mode of the file as executable and then we execute the file by calling its path and name..
- What are build scripts ?
    - A **build script** is a command or a series of commands that package your application.
    - You have been using build scripts really often throughout this course. Some frameworks like React and Angular make them readily available, making your life easier. While these frameworks are great and provide good scripts, it's still important to understand a little bit what they are doing.
- What should I consider when creating my own build script ?
    - Here are some concepts that you would want to explore if you want to create your own build script:
        - **Bundlers like Webpack and Rollup** are able to package your application code and all its dependencies. They are responsible for packing your code in a format that is more compact while still understandable by browsers and servers.
        - **Compilers like Babel** let you use more advanced features of the latest JavaScript versions while maintaining compatibility with older browsers.
        - **Transpilers like TypeScript** extend the base capacities of JavaScript by adding extra features not present in the base language.
    - You can take the following steps in order to create your build scripts:
        1. Check if a framework script is available. Frameworks like Angular often offer pre-made build scripts.
        2. Understand the final format of what you are building.
        3. Make the build script available inside a `package.json`.
- Good book to know more about Webpack in depth.
    - Click [here](https://survivejs.com/webpack/).
- What is a test script ?
    - A **test script** is a command or series of commands that test application code against pre-defined scenarios.
- Define the different types of tests (test hierarchy) ?
    
    ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2027.png)
    
    - **Unit Test** : tests a functions or methods of a class or module.
    - **Integration Tests** :  tests a set of modules together and see if they interact with each other properly.
    - **End to End Tests or E2E :** It’s ****is a methodology used for ensuring that applications behave as expected and that the flow of data is maintained for all kinds of user tasks and processes. An example of E2E is a sign up flow. In this flow, we ensure that the user signs up correctly and we receive the correct credentials at our servers. We might also want to make sure that users don’t enter malicious data so this might be a scenario to cover.
    - **UI Tests : It’s** is a testing type that helps testers ensure that all the fields, labels, buttons, and other items on the screen function as desired.
- Why testing is important in deployment ?
    - Testing is a prevalent topic in software development. When we think about deploying our application, we use tests in order to have **confidence** that we are deploying solid code that will not crash or introduce bugs.
    - Bug-free software, however, does not exist, for this reason, we must do our best to test the application and build confidence in our automated process.
- What is Cypress ?
    - Cypress is a cool all-in-one testing framework that includes assertion library, with mocking and stubbing.
    - [Cypress in a nutshell](https://www.youtube.com/watch?v=LcGHiFnBh3Y) is a great introduction video to Cypress and UI testing.
- How to define the testing sequence in our script ?
    - We should first run Unit and Integration tests because they’re easier to run and there’re a cool frameworks that accelerate the testing process like Jest and Mocha.
    - E2E and UI tests are more complex. They need a setup script and they need a dedicated test server so we’d run them at the end.
- Is writing testing considered as something we can test ourselves manually instead of spending more time writing automated tests?
    - While manual tests are great, they are slower and more expensive! By using automated tests we gain two benefits:
        - **Catching errors earlier in the process.** By running tests before deployment, we are now more confident that we are catching simple errors! We can always plan for more error cases in automated tests than would be possible in manual tests.
        - **We will deploy our app faster and more often.** Automated tests allow us to test features more quickly and more often, making it less expensive to develop and update features.
- If you write good code, why do you need tests?
    - It is not possible to write bug-free software. Developers do their best to think of every possibility but there are just too many variables at play when developing a feature. One of the best ways to ensure there are no bugs is by having a good amount of tests.

## Lesson 5 : Configure and Document a Pipeline.

- Lesson outcomes.
    - **Basics of a pipeline**: We will learn how everything comes together and enables automation around deployments.
    - **Continuous Integration**: We will understand the different steps that a pipeline executes that form the CI portion of this.
    - **Continuous Delivery**: We will learn how deployments can be automated after an application is built and tested.
    - **Documentation**: We will learn to document a pipeline and the different operations around an application.
- What is a pipeline ? How does an efficient pipeline benefit developers ?
    - *A pipeline is a set of instructions that will be executed on a server with the goal of building and deploying your application.*
    - Those set of instructions really come together inside a pipeline in a way that allows us more flexibility! An efficient pipeline can benefit developers in the following ways:
        - Faster feedback about the code
        - Getting features deployed faster
- Why create a pipeline ?
    - Pipelines have really cool benefits which include :
        - **Speed**: Automatically performing all the steps of a pipeline is faster than doing it manually each time.
        - **Finding bugs:** By running tests each time we are trying to deploy, we are able to find bugs earlier.
        - **Building confidence in your release:** When you release software that has passed different quality steps, you can be more confident in its quality.
- What makes up a good pipeline ?
    - A good pipeline must be :
        - **Readable:** You should try to make your pipeline concise and easy to read. Having multiple long commands inside the pipeline code will make it hard to understand.
        - **Logic should be inside the scripts:** This allows for more portability to other pipeline providers if you ever need to move away from your current provider.
        - **Constantly evolving:** This means that a pipeline should fit the need of the project and evolve as your project gains maturity.
- Which pipeline provider we’ll be using ?
    - We’ll be using **CircleCI.**
    - There are many other pipeline-as-a-service companies that offer a similar set of services, but for the purpose of this course, **CircleCI** presents a **great set of features**
     and has the advantage of being **popular**
     in the industry.
- What is a pipeline file ?
    - It’s just a YAML file that contains instructions that will run the pipeline.
    - With **CircleCI**, it should exist in `.circleci/config.yml`.
- What are the sections of a pipeline file ?
    - It contains the following sections:
        - **CircleCI version**: This is simply indicating which version of the platform our pipeline should use.
        - **Orbs** are a set of instructions created by CircleCi that allow us to **configure the pipeline** on which we will run our actions. These instructions will instruct the server to setup specific software on the server executing our pipeline. We could use orbs to setup node.js or install the AWS CLI for example. Orbs are **not always present** in a pipeline.
        - **Jobs** are groups of commands that we want to run. This is where we will run commands to **install, build or deploy our application**.
        - **Workflows** are instructions about **the order of the jobs**. They allow us to create complex flows and specify manual approvals. Workflows are **not always present** in a pipeline.
- Summary of `config.yml` parts, new terms, and references to CircleCI docs.
    
    ### **Summary - Parts of a config.yml File**
    
    Each config.yml file will be unique depending on the project, but normally we can find some common sections:
    
    - The **orbs section** will be responsible for setting up some basic recipes
    - The **jobs section** will contain specific actions to take
    - The **workflows section** will specify how the jobs should be handled
    
    ### **New Terms**
    
    - **Pipeline:** A set of instructions that install, test, build and deploy applications.
    - **Orbs:** Pre-made recipes offered by CircleCi to speed up setting up servers.
    - **Jobs:** Commands that a CircleCI pipeline should run.
    - **Workflows:** Information about the flow of jobs in a CircleCI Pipeline.
    
    ### **Further Reading**
    
    - [CircleCi getting started](https://circleci.com/docs/2.0/getting-started/): This is the intro tutorial from CircleCI.
    - [CircleCi Orbs](https://circleci.com/developer/orbs): Search engine for all the orbs available on CircleCI.
    - [Understanding CI/CD in depth](https://www.infoworld.com/article/3271126/what-is-cicd-continuous-integration-and-continuous-delivery-explained.html): this is a great post that explains CI/CD in-depth if you want to push the topics we will learn this lesson.
- How to setup CircleCI in my project ?
    - You first need to create a config.yml file inside a .circleci folder. Note that this is just an example, you might need a more sophisticated config file that has multiple orbs, jobs, and steps.
        
        ```yaml
        version: 2.1
        orbs:
          # orgs contain basc recipes and reproducible actions (install node, aws, etc.)
          node: circleci/node@4.1.0
          # different jobs are calles later in the workflows sections
        jobs:
          build:
            docker:
              # the base image can run most needed actions with orbs
              - image: "cimg/base:stable"
            steps:
              - node/install
              - checkout
              # install dependencies in both apps
              - run:
                  name: hello
                  command: |
                    echo "hello-world"
        ```
        
    - Now go to the CircleCI website and login via GitHub, connect the repo you’re working on with the website. Select the option which uses the config file inside the project, or create a new one in case there’s no config file in your project.
    - Every time you push a new commit to the repo, the workflow inside the config.yml file is triggered. Notice that we’ve ignored the workflow section in our config.yml file.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2028.png)
        
    - You can click on **build** to see the specific execution of commands. You notice that the “hello world” step is executed properly.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2029.png)
        
- What is Continuous Integration (CI) ?
    - Continuous integration is a group of many steps in our pipeline. The goal of continuous integration is to verify if code is ready to be merged when a pull request is submitted or to see if code is ready and safe to be deployed. By installing dependencies and testing the code, we are building confidence that our application is ready to be deployed. To do so, we can include the following steps in our pipeline:
        - **Linting** refers to verifying if the code follows certain standards of quality. This is the step responsible for calling lint scripts such as ESLint or Prettier.
        - **Installing** is the step responsible for calling `npm install` to download node modules locally
        - **Testing** is the step responsible for calling the different test scripts in our application If the testing step fails, then the pipeline stops.
        - **Building** is the step responsible for calling the build script of our application
    
    ## For more information
    
    - **[What is Continuous Integration](https://www.atlassian.com/continuous-delivery/continuous-integration)**: Great post from Atlassian explaining the basics of Continuous Integration.
    - **[Benefits of Continuous Integration](https://www.katalon.com/resources-center/blog/benefits-continuous-integration-delivery/)**: This is a great list of benefits that come with continuous integration.
- What is the difference between a linter (like ESLint) and a formatter like (like Prettier) ?
    - Prettier is a core formatting tool that can only find stylistic errors in the code (ex: number of spaces after `if`), while linting can go further and also look at programmatic errors (ex: a defined variable is never used).
    - Quick comparison by Prettier [website](https://prettier.io/docs/en/comparison.html).
- How to create Continuous Integration step with CircleCI ?
    - You can do this via `config.yml` file.
        
        ```yaml
        version: 2.1
        orbs:
          # orgs contain basc recipes and reproducible actions (install node, aws, etc.)
          node: circleci/node@4.1.0
          # different jobs are calles later in the workflows sections
        jobs:
          build:
            docker:
              # the base image can run most needed actions with orbs
              - image: "cimg/base:stable"
            steps:
              - node/install
              - checkout
        				# Installs yarn on CircleCI environment. Needed as our scripts
        				# uses yarn.
              - run: |
                  curl -o- -L https://yarnpkg.com/install.sh | bash
                  echo 'export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"' >> $BASH_ENV
        
              # install dependencies in both apps
              - run:
                  name: Frontend install
                  command: |
                    npm run frontend:install
              - run:
                  name: Backend install
                  command: |
                    npm run backend:install
              - run:
                  name: Frontend built
                  command: |
                    npm run frontend:build
              - run:
                  name: Backend built
                  command: |
                    npm run backend:build
        ```
        
    - In case you have an monorepo (like in the exercise which has front and backend apps in a single repo), you can push a commit to the master branch and all the commands in the `config.yml` file will run sequentially.
    - This is the `package.json` file in the monorepo, it has commands that install frontend and backend packages as well as building both apps.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2030.png)
        
    - You’d notice in the dashboard that each command is executed.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2031.png)
        
- What Is Continuous Delivery and Continuous Deployment?
    - **Continuous delivery** or **continuous deployment** are both steps that we refer to when talking about the **D** of CI/CD. Both have as a goal to **get the application from the build stage** and **move it to its destination**. Let's explore a little bit the difference between each:
        - **Continuous Delivery** aims at getting your application delivered to its final step before it is deployed. In this approach, code is manually approved for deployment.
        - **Continuous Deployment** is similar to continuous delivery but goes one step further and makes the complete process automatic without human approval.
    - It is important to note also that some applications like NPM package or Docker images are meant to be **published** to a registry, while while applications like servers or websites are meant to be **deployed** to services like S3 or Elastic Beanstalk.
- How to deploy a frontend app with CircleCI ?
    - You might first need to add AWS credentials (IAM user) in the project environment on CircleCI website.
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2032.png)
        
    - You add AWS CLI orb to the config file as well as referencing the credentials.
        
        ```yaml
        version: 2.1
        orbs:
          # orgs contain basc recipes and reproducible actions (install node, aws, etc.)
          node: circleci/node@4.1.0
          aws-cli: circleci/aws-cli@3.1.3
          # different jobs are calles later in the workflows sections
        jobs:
          build:
            docker:
              # the base image can run most needed actions with orbs
              - image: "cimg/base:stable"
            steps:
              - node/install
              - checkout
        				# Aws setup, credentials are taken from the environment variables.
              - aws-cli/setup:
                  aws-access-key-id: AWS_ACCESS_KEY
                  aws-secret-access-key: AWS_ACCESS_SECRET
                  aws-region: AWS_REGION_NAME
        
              - run: |
                  curl -o- -L https://yarnpkg.com/install.sh | bash
                  echo 'export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"' >> $BASH_ENV
        
              # install dependencies in both apps
              - run:
                  name: Frontend install
                  command: |
                    npm run frontend:install
              - run:
                  name: Backend install
                  command: |
                    npm run backend:install
              - run:
                  name: Frontend built
                  command: |
                    npm run frontend:build
              - run:
                  name: Backend built
                  command: |
                    npm run backend:build
              - run:
                  name: Frontend Deployed
                  command: |
                    npm run frontend:deploy
        ```
        
    - You can now push a code commit and you’d see that the app is deployed successfully.
    - Notice that the app has a deploy script which is :
        
        ```json
        "deploy": "chmod +x ./bin/deploy.sh && ./bin/deploy.sh"
        ```
        
    - Which execute the shell script (you might need to remove `--acl public-read` in case you’ve not allowed ACL in your bucket) :
        
        ```bash
        aws s3 cp --recursive --acl public-read ./build s3://reactnd-contacts-complete
        ```
        
        ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2033.png)
        
- Why do we create documentation for our project ?
    - Documenting is important in order to properly communicate difficult parts of an application. Documentation also serves as a good reference when it comes to onboarding new developers on a project or diagnosing something that is going wrong.
- What types of documentations should we consider ?
    - There are multiple ways to document a project. Here are some forms of documentation that you might want to dive more into:
        - **Architecture diagrams** are great at giving an overhead view of your application or production environment. These diagrams come in multiple forms but they all have a similar goal: give a visual reference to one part of your project. You can use [diagrams.net](http://diagrams.net) which is a cool tool to define an architecture for your project.
        - **Runbooks** are step-by-step guides that let you quickly remember how to accomplish certain operations on your website.
        - **Markdown files** are great for giving a quick glimpse into the details of the project. The most common example is the README.md file that is present on most GitHub repo.
        - **Documentation sites** provide a complete solution to host all documentation surrounding a project or company. Some are offered as a service like [Confluence](https://www.atlassian.com/software/confluence) from Atlassian, while others are complete projects that live in a repo like **[Docusaurus](https://docusaurus.io/)**. This is the most complicated type to create but the most comprehensive and informative.
- What are the important sections of a README file ?
    - In your README, you are trying to include general information about the project:
        - How to set up the project.
        - A brief description of the project..
        - Any other useful information to communicate to new developers and give information at a quick glance.
    - You can check [makeareadme.com](http://makeareadme.com) website that explains how to create a good readme file and what sections should you readme file include.
- How to create an architecture diagram for an app that contains a web hosting service, non-relational database, web server, and a identity provider ?
    
    ![Untitled](Deployment%20Process%202e4a11106b0c4d3792d7436f9e8e7577/Untitled%2034.png)
    
    - This is a simple example of how you can represent an application's production environment. Architecture diagrams should aim at providing a representation of the different layers of your application.
    - No diagram will be the same but let's note some of the key points in the example above:
        - The AWS services are all inside the zone labeled as the "AWS cloud"
        - There are arrows explaining the flow of information with a brief description
        - Labels show the name of each service

## Windows Subsystem Linux (WSL).

- In case you got board of finding windows equivalent commands of Linux commands.
- WSL is a Linux terminal inside a windows operating system.
- Follow [these](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-10#1-overview) instructions to install WSL.
- Be sure of enabling Hyper-V from Windows Features. You also need to enable visualization option from BIOS depending on the system you’re using.