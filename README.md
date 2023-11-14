# docker

sudo apt-get update
sudo apt-get remove docker docker-engine docker.io
sudo apt install docker
------------------------------
-- start docker
sudo systemctl start docker
sudo systemctl enable docker
-- check
docker --version
-------------------------------


sudo docker login
sudo docker images
sudo docker tag bulletinboard(repo name):1.0(tag) nikhildongre8109(dockerid)/bb1(name)
sudo docker images
sudo docker push nikhildongre8109/bb1
-- it will start pushing img, then check on docker hub


sudo pull nikhildongre8109/bb1
--pulls back the img













































PUSH IMAGES ON DOCKER REPOSITORY


sudo docker login      >>> To login to docker account give user name and password

sudo docker images  >>> List the docker images 

sudo docker  tag  repositoryname:tag  dockerid/newname

sudo docker images >>> To view the newly created image version 

sudo docker push dockerid/newname   >>> To push the local image to docker hub 

sudo docker rmi repositoryname:tag   >>> To remove the local repository

sudo docker pull repositoryname:tag    >>> To pull the new repository from hub


Docker
Docker is a platform for developers and sysadmins to build, run, and share applications with containers. The use of containers to deploy applications is called containerization. Containers are not new, but their use for easily deploying applications is.
Containerization is increasingly popular because containers are:
Flexible: Even the most complex applications can be containerized.
Lightweight: Containers leverage and share the host kernel, making them much more efficient in terms of system resources than virtual machines.
Portable: You can build locally, deploy to the cloud, and run anywhere.
Loosely coupled: Containers are highly self sufficient and encapsulated, allowing you to replace or upgrade one without disrupting others.
Scalable: You can increase and automatically distribute container replicas across a datacenter.
Secure: Containers apply aggressive constraints and isolations to processes without any configuration required on the part of the user.
Images and containers
Fundamentally, a container is nothing but a running process, with some added encapsulation features applied to it in order to keep it isolated from the host and from other containers. One of the most important aspects of container isolation is that each container interacts with its own private filesystem; this filesystem is provided by a Docker image. An image includes everything needed to run an application - the code or binary, runtimes, dependencies, and any other filesystem objects required.
Containers and virtual machines
A container runs natively on Linux and shares the kernel of the host machine with other containers. It runs a discrete process, taking no more memory than any other executable, making it lightweight.
By contrast, a virtual machine (VM) runs a full-blown “guest” operating system with virtual access to host resources through a hypervisor. In general, VMs incur a lot of overhead beyond what is being consumed by your application logic.





 
 
The installation steps are for the Ubuntu 16.04 LTS
 
 
Updating the local databases
 
-->sudo apt-get update
 
 
Uninstalling the older versions if any
 
-->sudo apt-get remove docker docker-engine docker.io
 
 
Installing a Docker
 
--> sudo apt install docker.io
 
Start and automate the docker
 
--> sudo systemctl start docker
--> sudo systemctl enable docker
 
Checking the version of docker
 
--> docker --version
 
 
 
Get  the example project from git
 
sudo git clone https://github.com/dockersamples/node-bulletin-board
cd node-bulletin-board/bulletin-board-app
 
 
DOCKER FILE
 
# Use the official image as a parent image
FROM node:current-slim
 
# Set the working directory
WORKDIR /usr/src/app
 
# Copy the file from your host to your current location
COPY package.json .
 
# Run the command inside your image filesystem
RUN npm install
 
# Inform Docker that the container is listening on the specified port at runtime.
EXPOSE 8080
 
# Run the specified command within the container.
CMD [ "npm", "start" ]
 
# Copy the rest of your app's source code from your host to your image filesystem.
COPY . .
 
Build and test your image
sudo docker image build -t bulletinboard:1.0 .
 
Run your image as a container
sudo docker container run --publish 8000:8080 --detach --name bb bulletinboard:1.0
 
http://localhost:8000
to access your application
 
Stop your DOCKER
docker container rm --force bb


--------------------------------------------------------------------------------------------------------
 Que 1)  You are a system administrator working with Docker in a Linux environment. Your task is to run an Ubuntu container and, within that container, execute the "whalesay" command to make a whale say "boo." This exercise will test your knowledge of creating and running containers within Docker, even when it involves running additional commands within the containers.
ChatGPT
Certainly! To accomplish this task, follow these steps:

Install Docker:
Make sure Docker is installed on your Linux system. You can follow the official Docker installation guide for Ubuntu: Get Docker.

Pull the Ubuntu Image:
Open a terminal and run the following command to download the Ubuntu Docker image from Docker Hub:

bash
Copy code
docker pull ubuntu
Run an Ubuntu Container:
Now, you can create and run an interactive shell within a new Ubuntu container:

bash
Copy code
docker run -it --name my_ubuntu_container ubuntu /bin/bash
This command starts a new container named "my_ubuntu_container" with an interactive shell.

Install the "cowsay" Package:
Inside the running container, install the "cowsay" package, which includes the "whalesay" command:

bash
Copy code
apt-get update
apt-get install -y cowsay
Run the "whalesay" Command:
Now, you can use the "whalesay" command within the container:

bash
Copy code
whalesay boo
This will make the whale say "boo."

Exit the Container:
Type exit to leave the container's interactive shell.

Commit Changes to a New Image (Optional):
If you want to keep the changes you made to the container, you can commit them to a new Docker image. Replace my_ubuntu_container with the actual container ID or name and my_custom_ubuntu_image with your desired image name:

bash
Copy code
docker commit my_ubuntu_container my_custom_ubuntu_image
This creates a new Docker image with the changes you made.

Clean Up (Optional):
If you don't plan to use the container or image further, you can clean up by stopping and removing the container:

bash
Copy code
docker stop my_ubuntu_container
docker rm my_ubuntu_container
Additionally, you can remove the image if you created a new one:

bash
Copy code
docker rmi my_custom_ubuntu_image
That's it! You've now run an Ubuntu container and made a whale say "boo" using the "whalesay" command.


Que 2) You're a software developer with a busy schedule, and you've found creative ways to manage your free time and productivity. You decide to use Docker to run two separate containers to fulfil different needs during your breaks. One container runs a game, specifically the classic game of Minesweeper, while the other container is set up for Python development when you're busy with coding tasks.
ChatGPT
Certainly! Setting up Docker containers for Minesweeper and Python development can be a great way to efficiently manage your free time and productivity. Here's a guide to help you with this setup:

1. Minesweeper Container:
a. Pull the Minesweeper Docker Image:
bash
Copy code
docker pull jarl-dk/minesweeper
b. Run the Minesweeper Container:
bash
Copy code
docker run -it --name minesweeper_container jarl-dk/minesweeper
This will start the Minesweeper game inside the container. When you're done playing, you can simply exit the game, and the container will stop.

2. Python Development Container:
a. Create a Dockerfile for Python Development:
Create a Dockerfile (e.g., named Dockerfile_python) with the following content:

Dockerfile
Copy code
FROM python:3.9

WORKDIR /app

# Install any additional dependencies you need for development
RUN pip install jupyterlab

CMD ["bash"]
b. Build the Python Development Image:
Navigate to the directory where your Dockerfile is located and run:

bash
Copy code
docker build -t python_dev_image .
c. Run the Python Development Container:
bash
Copy code
docker run -it --name python_dev_container -v $(pwd):/app -p 8888:8888 python_dev_image
This will start a Python development environment with JupyterLab. You can access JupyterLab in your browser at http://localhost:8888.

3. Managing Containers:
a. Switching Between Containers:
When you want to switch between the Minesweeper and Python development containers, you can stop the current container and start the other:

To stop a container:

bash
Copy code
docker stop minesweeper_container
# or
docker stop python_dev_container
To start a container:

bash
Copy code
docker start minesweeper_container
# or
docker start python_dev_container
b. Cleaning Up:
If you want to remove the containers:

bash
Copy code
docker rm minesweeper_container
docker rm python_dev_container
4. Enjoy Your Breaks!
Now you can easily switch between playing Minesweeper and doing Python development during your breaks. This setup allows you to efficiently use your free time and stay productive with your coding tasks.


--------------------------------------------------------------------------------------------------------
cloudsim files: - https://drive.google.com/file/d/1p_mEGiTeCCTv3l83cKPKY-h3PZh7DfhD/view
