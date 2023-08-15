# CI-CD-Jenkins                                                                 ************ GoToCode Option, you see te steps******************
**Set up a CICD Pipeline using Jenkinsfile and Docker on AWS EC2**
![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/dd8e0268-cbed-4486-8817-db17df05aff3)

#CI/CD is an essential part of DevOps and any modern software development practice. A purpose-built CI/CD platform can maximize development time by improving an organization’s productivity, increasing efficiency, and streamlining workflows through built-in automation, testing, and collaboration.

**#Key Concepts to be Applied here:-**********

#**What is Continuous Integration:**	

Continuous Integration is a foundational practice in modern software development and is closely associated with the broader DevOps philosophy. It contributes to faster development cycles, improved code quality, and more reliable software releases by promoting a culture of automation, collaboration, and immediate feedback.

**What is Continuous Delivery/Deployment:**

Accurate description of Continuous Delivery and the role of Jenkins in automating the deployment process. Continuous Delivery indeed focuses on automating the steps required to prepare code changes for a potential release to production, ensuring that the software is always ready for deployment. By using Jenkins to automate the deployment of your application to a server or Docker registry after successful build and test phases, you're implementing a streamlined Continuous Delivery/Deployment pipeline. This approach not only ensures the availability of the latest application version but also accelerates the time-to-market for your software, allowing you to deliver updates more quickly and reliably to your end-users

**What is Continuous Testing:**

Continuous Testing ensures ongoing assessment of changes and maintains the quality of the application throughout the development process. By integrating testing into the pipeline, especially during the execution of the Docker image, potential issues are detected early in the development cycle, allowing for prompt remediation and higher-quality software delivery. This approach aligns well with the DevOps philosophy, where collaboration, automation, and feedback are key to achieving faster, more reliable, and high-quality software releases. 

**Infrastructure as Code (IaC):**

IaC is a practice where infrastructure components, such as servers, networks, and databases, are defined, provisioned, and managed using code. This code is written using programming or scripting languages and follows software development practices like version control and automation. By treating infrastructure as code, organizations can achieve consistent, repeatable, and reliable deployments, reduce manual intervention, and improve collaboration between development and operations teams.

**Jenkins Pipeline Scripting and IaC:**

You've correctly highlighted the synergy between Jenkins pipeline scripting and IaC. By using Jenkins pipeline scripting, you can automate the build, test, and deployment process of your application. This script defines the entire software delivery pipeline, including building, testing, and deploying code changes. Treating this pipeline script as code enables you to manage it using version control systems like Git, ensuring traceability, collaboration, and the ability to reproduce the pipeline as needed.

In summary, your description emphasizes the importance of managing infrastructure as code and leveraging Jenkins pipeline scripting to automate the software delivery pipeline. This approach aligns well with modern software development practices, including DevOps and Continuous Integration/Delivery, and contributes to more efficient and reliable software deployments.

**Docker:**

We will containerize our application using Docker to make it more portable and scalable. Docker allows us to package our application and its dependencies into a single, portable unit that can be run consistently on any platform.

**Git:**

We will use Git to manage the source code of our application, making it easier to collaborate and version-control changes.

**Pre-requisites:-**

1.  AWS account and familiarity with AWS EC2.
2.  Docker Hub account.
3.  Familiarity with Git version control and experience with command line interface.
4.  Github account.
Understanding of the Flask application framework and Docker containerization technology.

**Agenda:**

In this blog, we will set up a CI/CD pipeline using Jenkins and Docker by building a simple Flask application, testing it, and deploying it to Docker Hub.

**Containerize a simple Flask application using Docker to make it more portable and scalable.
Use Git to manage the source code of the application to make it easier to collaborate and version-control changes.
Implement Infrastructure as Code for automated build, test, and deployment process using Jenkins pipeline script.
Ensure Continuous Integration of the application by configuring Jenkins to automatically build and test every time code changes are made.
Implement Continuous Delivery/Deployment by configuring Jenkins to automatically deploy the application to a Docker registry when the build and test phases are successful.**

**Step 1: Create an EC2 instance**

****Log in to the Amazon management console, open EC2 Dashboard, click on the Launch Instance drop-down list, and click on Launch Instance as shown below:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/49b8ebc0-a2b3-4abd-a6af-e10036f3f3e1)

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/cb5b2975-223c-4a34-add8-477353bf157b)

**Now, Let’s choose Ubuntu Server 22.04 which is free tier eligible.****

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/115127c2-6354-4c38-8c0b-f227e9e4a1ac)

**choose an Instance Type. Here you can select the type of machine, number of vCPUs, and memory that you want to have. Select t2.micro which is free-tier eligible.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/ea39fc4c-0826-49bb-bd1b-4b3a932df3d7)

**I will select an already existing key pair. You can create new ones in case you don't have any existing ones.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/c67ad9c7-336f-47c4-b7b8-6f39e4861807)

**Under Network Settings, Choose the default VPC with Auto-assign public IP in enable mode. Choose an existing security group that we have been using in all our previous projects with port 8080 open apart from SSH.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/36e15822-0a24-4bc1-ad68-92406ee0c21e)

**Rest of the settings we will keep them at default and go ahead and click on Launch Instance.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/faca734d-4f21-4b8a-a385-f613b1e9d321)

Now, in the next screen, you can see a success message after the successful creation of the EC2 instance, click on Connect to instance button:

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/46460fe1-8b10-4cde-92d9-befbd8bd1210)

**Now connect to instance wizard will open, go to SSH client tab and copy the provided chmod and SSH command:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/3be04384-f716-41cb-9413-69cce3e87bbc)

**Open any SSH Client in your local machine, take the public IP of your EC2 Instance, and add the pem key and you will be able to access your EC2 machine in my case I am using MobaXterm on Windows:**

**I will take Git Bash app here. you can search in google like git SCM: Once downloaded Git, use this**, ![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/e47f3610-7ffe-4deb-937e-7c25b4784178)
 

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/d75fe64c-4dc8-44fa-83b0-205b9cdcd7c3)

**DOWNLOAD WHICH ONE IS SUITABLE FOR YOUR LAPTOP:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/e657a469-7ccb-4fac-bdeb-f0e632636d7f)

**I am using - Git Bash here:-**

**1.  Install Jenkins on Ubuntu EC2 Machine.**

**If you have been following my blog you should have seen that we have been installing Jenkins either from the official Jenkins website or using Jenkins on docker containers. Here we will install Jenkins using a script that basically has the same steps which we can find on the Jenkins official website.******

**So, Now Run like below in your Git Bash.**

# Update package lists
sudo apt-get update

# Install Java 11
sudo apt-get install -y openjdk-11-jdk

# Download Jenkins key and add it to system
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null

# Add Jenkins to system package source list
sudo sh -c 'echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null'

# Update package lists again to include Jenkins and install it
sudo apt-get update
sudo apt-get install -y jenkins

# Verify Jenkins is installed and working
sudo systemctl status jenkins

**Let’s now verify the status of Jenkins:**********

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/b54a62b4-bfce-409d-8c7e-19a34b404688)

**Lets now access the Jenkins Server using the public IP of our Ubuntu EC2 instance on port 8080 and you should see something like the below:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/e27ed243-2c25-42c3-a1ec-63a01c084aa0)

**Navigate to /var/lib/jenkins/secrets/initialAdminPassword and copy the password and unlock Jenkins.**

**After that, Install the suggested plugins:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/1a360726-3f84-4511-a8d9-c2f362bd2e0c)

**Now let’s create our first Admin user and provide the required info:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/6c178520-b8b2-4905-885c-7ebb347506b2)

**After creating the user we should land into the Jenkins dashboard and let’s install the Docker Plugin.**

Click on **Manage Jenkins** -> **Manage Plugins** -> **Available Plugins** and install without restart the **Docker** plugin.

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/8051df17-89fa-4456-a338-22aaaaff8b0d)

**Install Docker now:**

Now on our Jenkins server let’s install the Docker with the following script:

# Update package list
sudo apt-get update

# Install necessary packages to use HTTPS repositories
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y

# Add Docker GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Add Docker repository to sources list
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update package list for the addition to be recognized
sudo apt-get update

# Install Docker CE
sudo apt-get install docker-ce -y

# Add current user to the docker group to run Docker commands without sudo
sudo usermod -aG docker ${USER}

# Activate the changes to groups
su - ${USER}

# Verify Docker is installed and working
sudo systemctl status docker

**After the successful installation of Docker, let’s verify the status of Docker:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/495053b1-d32a-4e92-aec6-7ac763d31205)

**Add the permission for jenkins user to the docker group and restart the Jenkins server.**

**sudo usermod -aG docker jenkins
sudo systemctl restart jenkins**

**Configure your DockerHub Credentials**

**Create an account in DockerHub or log into your existing DockerHub account. Go to ‘Account Settings’ under your account name and then ‘Security’ as shown below to create a token:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/45c19397-968f-43d5-be28-0ee82f67519a)

**Make sure to save your access token since it only appears one time when generating it.**

Now we will add this token to our Jenkins UI. For that, go to **Manage Jenkins** -> **Credentials** -> **System** -> **Global credentials** -> + **Add credentials**. Enter your Docker Hub username, provide any ID (make sure you place this same ID under Environment Variables later), and a brief description of the credentials.

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/9d44fae9-1865-4760-80e0-19bca9bd188a)

**Create Environment Variables**

**Now we will create the environment variables which we will use later in the Jenkinsfile for the Docker image and for the Docker Hub credentials.**

**Go to Manage Jenkins -> Configure System and under ‘Global properties’ add them as shown in the picture below.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/4cc28451-04f6-486d-b9cd-f98a4b7021ac)

**Click on Apply and Save to Continue.**

**Let's Create Jenkins Job**

****In your Jenkins Dashboard go to New Item -> Pipeline and enter the name of your project.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/f059ead7-847b-4f63-8c4c-fd98367b2f69)

**Now we will configure this new job. Under General, give some description of your project. Select GitHub project among the options and add the link of your GitHub repository as shown below:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/1b728fd9-5e2f-4c7d-bf5a-f81d5e30530b)

****Now in the Pipeline section, under SCM select ‘Git’ and enter the URL of the repository again.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/7aa367ef-dacc-4a53-a497-1395889f0829)

**Scrolling down you will see Script Path which has by default Jenkinsfile mentioned which should match the name of your Jenkinsfile in your GitHub repository.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/ab62e8c6-49d9-43b2-8171-f6dd752399fd)

**Click on Apply and Save.**

**Build the Pipeline by clicking on the Build Now button on the left navigation bar.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/74d04e78-bb9f-4564-b094-fc648cc422d1)

**The above screenshot shows that the build has been successful. We can also verify by checking our Docker Hub Account to see whether the Image has been uploaded or not:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/f06e45bf-5981-45cb-943f-043e301b6def)

**Adding Webhook to our Jenkins Pipeline**

**A Webhook, also known as a Web Callback or HTTP push API is a mechanism for an application to provide real-time data to other apps. A Webhook sends data to other applications in real-time, so you get it right away.**

****To add a webhook in our GitHub repo go to the settings, click on webhooks, and then on Add webhook as shown below:**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/f41ebe63-7acf-456d-b6f5-7d49a31b3c06)

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/67a7229e-c1ee-4ea2-91cc-9f78ae712963)

**On the next screen provide the following info:**

Payload URL: [EC2-IP-Address:8080/github-webhook/]
Content type: application/json
Trigger only on the push event

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/3faf4da0-9edb-414b-943c-b2dff2c5a5cb)

**Click on Add Webhook to proceed.**

**Now under Build Triggers select the option GitHub hook trigger for GITScm polling, click on Apply and Save to continue.**

When Jenkins receives a GitHub push hook, GitHub Plugin checks to see whether the hook came from a GitHub repository which matches the Git repository defined in SCM/Git section of this job. If they match and this option is enabled, GitHub Plugin triggers a one-time polling on GITScm.

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/bf063d70-c203-4b95-8135-0a2596bc7f20)

**Now After that, we will install the GitHub Integration plugin in our Jenkins Server**

Jenkins -> **Manage Jenkins** -> Manage Plugins -> **Install github integration plugin**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/f78eacd2-80e3-4897-ab7f-135247190d2a)

**Let’s do some minor changes in README.md in our GitHub repo, commit and push your changes. which should trigger the Jenkins Job, thus displaying the successful integration of Github webhooks with Jenkins that ensured that the latest changes are tested, built, and deployed as quickly as possible.**

![image](https://github.com/MyDevOps-Venky/CiCd-Jenkins_Project1/assets/128009454/9654b24f-f138-4b97-8e39-640833b1a0e0)

**Also if we check the console output of our 2nd Build we should notice the line saying Started by GitHub** push "your name here"

*********Finally, we learned how to containerize a Flask application with Docker, using Git for version control, and automate the build, test, and deployment process with Jenkins, also we learned how to push the Docker Image to DockerHub.In the end, we also showed how Jenkins detected any code changes using the powerful Webhook.******************














