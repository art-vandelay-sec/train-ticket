This project is ticket seller application in microservice architecture, including 40+ microservices
=========================

- java，spring boot，spring cloud
- nodejs，express
- python，dijango
- go，webgo

---
## Supported Cluster Orchestration
- K8S + Istio
- Docker Swarm

##  Local runtime environment
- jdk8
- maven
- docker
- docker-compose
- k8s
- istio


# Deploy Train Ticket with docker-compose

## SetUp steps
  you just need one machine and installed with  git, jdk8, maven, docker and docker-compose
- setup with the following steps:  
    (1) Clone all the source code to your local computer with git.  
    (2) Move all directory whose name is start with "ts-" to your server's  other directory.   
    (3) Move pom.xml and docker-compose.xml to your server to the same directory with "ts-..." directories.  
    (4) Add the "myproject" directory to your maven ".m2" directory.  
        The directory index is like  /root/.m2/repository/myproject.  
    (5) Open the terminal and enter the directory where pom.xml loacted.   
    (6) Use the instruction: mvn clean package  And waiting for build success.   
    (7) Use the instruction: docker-compose build  And waiting for build success.  
    (8) Use the instruction: docker-compose up   And wating for all services startup
     
## Access the Train Ticket System in Browser 
- before access, you can use "docker ps" to see which port you should access:  
    on default. the port is 80  
    than you can use the ip of your server to access it.  
    Unless something unexpected, if you can see the main interface like below, congratulations!
  ![main interface](https://raw.githubusercontent.com/microcosmx/train_ticket/master/image/main_interface.png)
    
##  The Step of Buy Ticket
    (1) While access the main interface, Input the start city ,destination city, date and train type , And then click "search" button,
        you will get the tickets list , which is like the picture above.
    (2) After select trip and seat type, Click "Booking" button, then it will show login dialog( or you can login before)
        Just follow that step to login
  ![client_login](https://raw.githubusercontent.com/microcosmx/train_ticket/master/image/login.png)
    (3) After login succeed, it will continue with the previous step, in this step, you must choose or add one Contacts,
        And decide whether you need Assurance ,food , or consign, than you can click "Select" button.  
  ![select_contact](https://raw.githubusercontent.com/microcosmx/train_ticket/master/image/select_contace.png)
    (4) After select,it will pop up a dialog for you to check whether the order information is correct, if so, then you can 
       click "submit" button to submit you reservation  
  ![confirm_ticket](https://raw.githubusercontent.com/microcosmx/train_ticket/master/image/confirm_ticket.png)
    (5) The last step is to go to the Order List to find the ticket you reserver before, and click the "Pay" button,
       waitting for success, than the buy ticket flow is over.
  ![pay_ticket](https://raw.githubusercontent.com/microcosmx/train_ticket/master/image/pay_ticket.png)

#  Deploy Train Ticket with k8s
- please follow the below steps:  
  [k8s deploy steps](https://github.com/microcosmx/train_ticket/tree/master/Document/k8s)
  
---

##  Clustering runtime environment(docker swarm):

build:

mvn clean package

docker-compose build

docker-compose up

docker swarm init --advertise-addr 10.141.211.161

docker swarm join-token manager

docker swarm join-token worker


app tag:

docker tag ts/ts-ui-dashboard 10.141.212.25:5555/cluster-ts-ui-dashboard


app local registry:

docker push 10.141.212.25:5555/cluster-ts-ui-dashboard


deploy app (docker swarm):

docker stack deploy --compose-file=docker-compose-swarm.yml my-compose-swarm


monitoring:

docker run -d -p 9000:9000 --name=portainer-ui-local -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer

http://10.141.211.161:9000

---

##  Fault Replication Branches list   
- You can check the fault replication details on following branches of this git repository

F1 
ts-error-process-seq

F2
ts-error-reportui

F3
ts-error-docker-JVM

F4
ts-error-ssl

F5
ts-error-cross-timeout-status(chance)

F7
ts-external-normal

F8
ts-error-redis

F10
ts-error-normal

F11
ts-error-bomupdate

F12
ts-error-processes-seq-status(chance)

F13 
ts-error-queue
