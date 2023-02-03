# Install-and-Run-Jenkins-With-Docker-Compose
install install Jenkins as container on ubuntu

### On ubuntu server, first install docker and docker-compose

    sudo apt-get update
    sudo apt-get install docker.io
    sudo systemctl start docker
    sudo systemctl status docker
    sudo apt  install docker-compose

## then, create docker-compose.yaml 
    
    touch docker-compose.yaml 
    vi docker-compose.yaml 
      
## here is the contex of the yaml file: 

  1 #docker-compose.yaml
  2 version: '3.8'
  3 services:
  4   jenkins:
  5   image: jenkins/jenkins:lts
  6    privileged: true
  7    user: root
  8    ports:
  9     - 8080:8080
  10     - 50000:50000
  11    container_name: jenkins
  12    volumes:
  13    - /home/ubuntu/jenkins/jenkins_configuration:/var/jenkins_home
  14    - /var/run/docker.sock:/var/run/docker.sock
      
      
 # this yaml file will get the lastest versio of the jenkins as : mage: jenkins/jenkins:lts
 # set ports, and volumes. 
 ## 
 
- Line #1 is a comment.

- Line #2 tells Docker Compose which version of the Compose specification we’re using.

- Line #3 starts defining services. For now, we just have one. 

The rest of the file defines the Jenkins container. 

- It will run the latest Jenkins image with root privileges. We’re running the container with host networking, so lines #9 and #10 tell Docker to redirect ports 8080 and 50000 to the host’s network. 

The container’s name is jenkins.

- Finally, /home/${myname}/jenkins_compose/jenkins_configuration is mapped to /var/jenkins_home in the container. 

Run docker-compose in the directory where you placed docker-compose.yaml.

      $ docker-compose up -d
      
  Now point a web browser at port 8080 on your host system. You’ll see the unlock page.
![image](https://user-images.githubusercontent.com/56624571/216549542-58e4a442-c196-4d43-9f8c-25e570f8540b.png)

        $ docker logs jenkins | less

Look for a block enclosed with six lines of asterisks.

Enter the password and click Continue.

