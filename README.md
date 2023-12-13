# FinalExam3504
Repository for Final Exam CLCM 3504

# Table of Contents

- [FinalExam3504](#FinalExam3504)
  - [Table of Contents](#table-of-contents)
  - [Instructions](#instructions)
    - [Workflow](#workflow)
      - [Step_1](#Step-1)
      - [Step_2](#Step-2)
      - [Step_3](#Step-3)
      - [Step_4](#Step-4)
      - [Step_5](#Step-5)
      - [Step_6](#Step-6)
      - [Step_7](#Step-7)
      - [Step_8](#Step-8)
  - [How to ensure automatic deployment](#how-to-ensure-automatic-deployment)
  - [Challenges faced](#challenge-faced)

# Instructions

## Workflow

### Step 1
Setting up EC2 Instance.

I started by creating an EC2 instance, which is like having my own virtual server in the cloud. It's where I plan to run my application.
### Step 2
Connecting via SSH.
After the instance was ready, I connected to it using SSH. SSH is like a secure tunnel that lets me interact with my virtual server as if it were my local machine.
### Step 3
Installing Apache and Docker.
Once connected, I installed Apache and Docker on the EC2 instance. Docker is a tool that helps me package my application and its dependencies into containers, making it easier to deploy and run consistently.
### Step 4
Creating Git Repository.
Next, I set up a Git repository to manage my project's code. Think of Git as a version control system – it helps me keep track of changes and collaborate with others.
### Step 5
Workflow and Secrets.
I established a workflow using GitHub Actions. It's like having a personal assistant for my code, automating tasks like building and deploying. I also added secrets, which are like secure keys or passwords, to make sure sensitive information is kept safe.
### Step 6
Adding Dockerfile.
To tell Docker how to build my application, I created a Dockerfile. It's like a recipe that Docker follows to set up the environment and run my app.
### Step 7
Adding Website Files.
I added the files for my website to the Git repository. This includes HTML, CSS, and any other files that make up my site.
### Step 8
Ready for Hosting.
Now that everything is set up and my code is in the Git repository, my application is ready to be hosted. The Dockerfile and website files will help Docker create a container for my app, making it easy to run on the EC2 instance.

# How to ensure automatic deployment
For every change that is pushed to the main branch, it will automatically build the Docker image and then push the image to the Docker repository (Docker Hub).

After that, if the first stage runs successfully, the GitHub Actions will access to EC2 instance to pull that Docker image and try to stop and remove the old version of the Docker container. Next, it will start a new container by using the new Docker image version that was pulled before.

To ensure that this process won't have any error or mistake, I would like to make sure that we have space left for every time that pull a new image so I decided to remove the unused image by using the command:

docker image prune -f



# Challenge faced
There were several challenges faced by me but anyhow i maintained to overcome them all.

Firstly i would like to say that the main challenge was to deploy the image to EC2 and run the websiteb successfully because everytime i was trying o deploy my website, i get to know a new error but after few attemps like around 14-15 (approx) i came to know where the real issue was and i configured it.

Secondly i will that my website was launched but it was only showing "It Works" and when i was trying to run it was showing that port is already in use but the issue was when i code in EC2 as "Docker ps" there was no information of the container. Then i used these commands to configure the same.

- sudo lsof -i :80
- sudo service httpd stop
- docker stop finalexam
- docker rm finalexam
- sudo service restart docker
- sudo lsof -i :80
- docker run -d -p 80:80 --name finalexam ashxch7/finalexam:latest

Here 80:80 is the port used, ashxch7 is my dockerhub username and finalexam is the name of repository in dockerhub.
