# Jenkins Setup

This guide provides instructions on setting up Jenkins BlueOcean using Docker.

## Installation

Clone the Jenkins templates repository:
```sh
git clone https://github.com/jrzvnn/jenkins-docker-templates.git
```

1. Create a bridge network in Docker using the following command:
```sh
docker network create jenkins

```
2. Navigate to the docker directory:
```sh
cd docker
```
3. Build the Jenkins BlueOcean Docker Image:
```sh
docker build -t myjenkins-blueocean:2.462.1-1 .
```
4. Run the Jenkins BlueOcean container using the following command:
```sh
docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.462.1-1
```
5. Get the initial admin password:
```sh
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```
6. Connect to Jenkins:
Open a web browser and navigate to: [https://localhost:8080/](https://localhost:8080/)

## Notes
The version numbers of the Jenkins BlueOcean image and other components may change over time. For the latest versions and updated instructions, please refer to the official Jenkins documentation.

## Reference
For more detailed information, you can refer to the official Jenkins documentation:
[Installing Jenkins with Docker](https://www.jenkins.io/doc/book/installing/docker/)
