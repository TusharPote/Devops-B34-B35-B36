
##  ${\color{blue} \textbf{Installation-Steps  \ (Amazon-Linux)}}$ 


````
sudo yum update -y
sudo yum install -y docker
sudo service docker start
sudo usermod -a -G docker ec2-user
newgrp docker
````
````
docker --version
````



##  ${\color{blue} \textbf{Basic \ Docker \ Commands}}$ 
1. List Docker images:
````
   docker images
````
2. Pull Image From REgistry/DockerHub
````
docker pull <image_name>
````
3. Create Conatiner From Image
````
docker run -itd -p 80:80 <image_name>
````
4. List Running Conatainers
````
docker ps
````
5. Log In Into Conatainer
````
docker exec -it <container id> /bin/bash
````

