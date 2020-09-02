# Deployment

Deployment in this example if done via cf push.\
The application is deployed via ```cf push --random-route```\
Note : cf push needs a manifest.yml to define the application.

## Deployment via Docker Images
### Installation of Docker
* Create new vm to host docker
    * OS : 18.04.LTS
    * Installation procedure
        *  https://docs.docker.com/engine/install/ubuntu/
        * https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04#:~:text=%20How%20To%20Install%20and%20Use%20Docker%20on,of%20passing%20it%20a%20chain%20of...%20More%20

### Manual test on the Docker vm
* ssh to the docker vm
* clone the github library to the docker vm
```cmd
git clone https://github.com/bdelangh/cf-hello-world.git
```
Note : you need branch `1_REST_persist_in_memory`.

* the docker image with the cf command line. `ppiper/cf-cli`. More info on this image can be found at dockerhub [ppiper/cf-cli](https://hub.docker.com/r/ppiper/cf-cli).\
The source repository can be found at [Git Cloud Foundry Command Line Interface (CLI)] Doc(https://github.com/SAP/devops-docker-cf-cli).

* Test the docker cf cli image using 
```
sudo docker run ppiper/cf-cli cf --help
```

* Deploy the application using
```
sudo docker run --rm -v "${PWD}":/project ppiper/cf-cli /bin/bash -c "cf login -u 'user#name' -p 'password' -a 'loginurl' -o 'organization' -s 'space' && cd /project && cf push --random-route"
```

This command needs to be executed from the root directory of your development. The command mounts this root directory to the `/project` direcotry within the vm and executes the `cf push`command from there.

* Test the application via the SCP generated url
