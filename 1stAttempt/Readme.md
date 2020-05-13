# First Attempt: Set up all environment without Automation & Configuration concept 

## What should I think about this? 
- What kind of element we need to think? Server: AWS, Service: Apache Tomcat, MySQL, Jenkins, Github
- What else? All service runs on docker
- What is unfamiliar concept on me? Configuration (Docker, Kubernetes, Jenkins, Github, and etc)
Let's try: 

1) **Make a server** - In my case, I use Amazon web service with free-tier account. 

2) **Install all service on the server - docker:**
- Update Machine: sudo apt-get update
- Download Dependencies: sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common 
      apt-transport-https: allows package manager to transfer files and data over https
      ca-cerficiates: check security certificates
      curl: tools for transferring data
      software-properties-common: adds scripts for managing software
- Add Docker's GPG Key: curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
- Install the Docker Repository: sudo add-app-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
- Update Repositories: sudo apt-get update
- Install Latest VErsion of Docker: sudo apt-get install docker-ce
- Configure grouping: usermod -a -G docker ubuntu
                                                     - Src: https://phoenixnap.com/kb/how-to-install-docker-on-ubuntu-18-04
3) **Install all service on the server - MySQL: **
- Pull the MySQL Docker Image: docker pull mysql/mysql-server:latest
                               verify the images: docker images
- Deploy the MySQL Container: docker run --name=[container_name] -d mysql/mysql-server:latest
                           **-d** option instructs Docker to run the container as a service in the background
- Connect to the MySQL Docker Container: sudo apt-get install mysql-client 
       Check Initial Password for MySQL: docker logs mysql
                                         docker exec -it [container_name] mysql -uroot -p
                                  mysql> ALTER USER 'root@"localhost' IDENTIFIED BY 'root'@'localhost' IDENTIFIED BY '[newpassword]';
                                  
            
                        
                                       Jenkins: 1) Get image - docker pull jenkins/jenkins
                                           - Src: https://technology.riotgames.com/news/putting-jenkins-docker-container
                                       Apache Tomcet: 1) Get image - docker pull tomcat
                                           - Src: https://hub.docker.com/_/tomcat
                                       MySQL: 1) Get image - docker pull mysql/mysql-server:latest
            Any Chellenging? Port configuration
