
# Jenkins Server with Docker-Compose

This repository contains a Docker Compose file for running a Jenkins server with Docker.  
  
## Requirements

-   [Docker](https://www.docker.com/get-started)
-   [Docker Compose](https://docs.docker.com/compose/install/)
  
    
## Build Jenkins Server Docker Image
  
Execute the VSCode-Task or run the following command:
`docker build -t jenkins-docker-blueocean:2.395 .` 
  
## Usage
  
To start the Jenkins server, simply run the following commands:
  
`mkdir jenkins-data jenkins-docker-certs` (this will ensure the right folder-permissions)  
`docker-compose up -d`  
  
This will start a Jenkins server container and map its default port (8080) to the host machine's port 8080.

To access the Jenkins server, open a web browser and go to `http://localhost:8080`. You will be prompted to enter the initial admin password which can be found by running the following command:

`docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword` 

After entering the initial admin password, you can follow the setup wizard to configure Jenkins.

## Configuration

This Jenkins server is configured with the following plugins:

-   Blue Ocean
-   Docker-Workflow

If you need to install additional plugins, you can do so by navigating to "Manage Jenkins" > "Manage Plugins" and searching for the plugin you want to install.

## Reference Nodes and Clouds
In order to run builds on the docker-host as containers we will utilize socat, as declared in the docker-compose. 
Please use the following Docker-Host URI:

> tcp://socat:2375

![screenshot](/img/docker_uri.png)

Keep in mind: You will need to enable the Docker-Plugin first! Also pay attention to the fact that using Label expressions to reference your Docker-Clouds still adds a space at the end, which you will need to remove.

Also don't forget to tick the Enable-Box after setting the Host-URI. After that add a Agent-Template of your choice.

## Maintenance

To stop the Jenkins server container, run the following command:

`docker-compose down` 

This will stop and remove the Jenkins server container.

## Contributing

If you would like to contribute to this repository, please create a pull request and include a detailed description of your changes.

## License

This project is licensed under the MIT License. See the [LICENSE](https://chat.openai.com/LICENSE) file for details.
