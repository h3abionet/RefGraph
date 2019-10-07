# RefGraphTeam Docker
Docker image and instructions to run RefGraph team software

## Installing docker
The image is built with docker. Docker needs to be installed on your system in order to build and run the image/container.  
Information on how to install docker:  
* [Mac](https://docs.docker.com/docker-for-mac/)
* [Windows](https://docs.docker.com/docker-for-windows/)
* [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

## Building the image
The docker image is built locally from the docker file provided. This allows you to always have the most up-to-date version of software. Please note that you will be downloading a reasonable amount (~ 2 GB).  

The building process will take some time - be patient.  
More information on the image building process and parameters are available at:  
[Build info](https://docs.docker.com/engine/reference/builder/)  

To build the image:  
* navigate to the directory with the `dockerfile`  
* In a terminal, run `sudo docker build -t refgraphteam  ./`  
* Confirm the image built successfully with `sudo docker images`. You should see the `refgraphteam` image.

## Using containers

Please note, the container will be removed after every run. Any output will be stored on your local storage but changes to the container will be lost.

To start the container:  
`sudo docker run -it --name testvg -v ${PWD}:/workspace --rm refgraphteam`  

The above command will create an interactive session during which you can run commands etc.  
Once done; type `exit` and **return** to exit the container.  

Your file output will be available in the current working directory.

## Notes on progressiveCactus
Local installs of progressive cactus are a bit tricky, primarily due to the kyoto* libraries.  

**Disclaimer**  
> The use and implementation of the commands and suggestions below are **at your own risk**.

The first issue is caused by a *symlink* to python2.7, which *conda* seems to change. The below command will *fix* the issue, **however**, it might not play nice with conda.  

`ln -s /usr/lib/python2.7/plat-*/_sysconfigdata_nd.py /usr/lib/python2.7/`  

The second issue is caused by later versions of gcc (gcc >= 6). You can either build with a previous version of gcc, or, you could apply the patches to the kyototycoon library files. A directory with patches is included (cloned from: [nf-annotate](https://github.com/robsyme/nf-annotate/tree/master/patches)).  

### progressiveCactus docker image
The progressiveCactus docker image attaches the current working directory to the container /workspace directory.  

The executable is located in `/progressiveCactus/bin/`.  

To run progressiveCactus simple type `progressiveCactus <"options to progressiveCactus">`.  
