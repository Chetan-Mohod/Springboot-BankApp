## End-to-End Bank Application Deployment using DevSecOps on AWS EKS
- This is a multi-tier bank an application written in Java (Springboot).

### PRE-REQUISITES FOR THIS PROJECT:
- AWS Account
- AWS EC2 instance (t2.medium)
- Install Docker
#
### DEPLOYMENT:
| Deployments    | Paths |
| -------- | ------- |
| Deployment using Docker | <a href="#Docker">Click me </a>     |
| Deployment using Docker Compose | <a href="#">Click me </a>     |
| Deployment using Jenkins on EKS | <a href="#">Click me </a>     |
| Deployment using Argocd on EKS| <a href="#">Click me </a>     |

#
### STEPS TO IMPLEMENT THE PROJECT
- **<p id="Docker">Deployment using Docker</p>**
  - Clone the repository
  ```bash
  git clone -b DevOps https://github.com/DevMadhup/Springboot-BankApp.git
  ```
  #
  - Move to the cloned repository
  ```bash
  cd Springboot-BankApp
  ```
  #
  - Build the Dockerfile
  ```bash
  docker build -t madhupdevops/springboot-bankapp .
  ```
> [!Important]
> Make sure to change docker build command with your DockerHub username.
  #
  - Create a docker network
  ```bash
  docker network create bankapp
  ```
  #
  - Run MYSQL container
  ```bash
  docker run -itd --name mysql -e MYSQL_ROOT_PASSWORD=Test@123 -e MYSQL_DATABASE=BankDB --network=bankapp mysql
  ```
  #
  - Run Application container
  ```bash
  docker run -itd --name BankApp -e SPRING_DATASOURCE_USERNAME="root" -e SPRING_DATASOURCE_URL="jdbc:mysql://mysql:3306/BankDB?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC" -e SPRING_DATASOURCE_PASSWORD="Test@123" --network=bankapp -p 8080:8080 madhupdevops/springboot-bankapp
  ```
  #
  - Verify deployment
  ```bash
  docker ps
  ```
  # 
  - Open port 8080 of your AWS instance and access your application
  ```bash
  http://<public-ip>:8080
  ```
  ### Congratulations, you have deployed the application using Docker 