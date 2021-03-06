# ASSIST-workshop-120522
Scaleouts ASSIST worskhop

Prerequisites
------------
You need a Linux system with Python 3.8, Docker and a modern GPU, installed with the appropriate Nvidia drivers and Docker, docker compose and Nvidia-docker.   

-  [Docker](https://docs.docker.com/get-docker)
-  [Docker Compose](https://docs.docker.com/compose/install)
-  [A FEDn network (provided by the workshop host)](https://github.com/scaleoutsystems/fedn) 

## Join the federation

- Open a terminal.

- Clone this repo and move in to the ASSIST-workshop-120522 folder:
```
git clone https://github.com/scaleoutsystems/ASSIST-workshop-120522.git
cd ASSIST-workshop-120522
```
- Create a data folder inside of the ASSIST-workshop-120522 folder and put in to the data folder:
```
mkdir data
cd data
```
- Download your local dataset partition from the google drive page and move it to the data folder.
- Unzip your local dataset (inside the data folder):
```
unzip dataset.zip
```
- Download the client.yaml file from the google drive page and put it in the ASSIST-workshop-120522 folder (the easiest way is to use an editor such as vim and copy-paste the content).

- Add the host ip XXX.XXX.XX.XX to the client.yaml file, line 3:
```
discover_host: XXX.XXX.XX.XX
```
- Open the docker-compose.yaml in your prefered editor and add the server ip adress that the workshop host is providing you with, to the combiner namespace, line 5:
```
client0:
  extra_hosts:
    combiner: XXX.XXX.XX.XX
```
Open the docker-compose.yaml and add your name to the client, line 12:
```
    command: /venv/bin/fedn run client --name yourname -in client.yaml
```
Replace yourname with your name. Dont use capitals or special characters.


Connect the client to the FEDn network:
```
docker-compose up
```

, or alternative:
```
docker compose up
```

Make sure the terminal shows: "CLIENT active". 

Now wait for the workshop host to start training.

### Join from an AWS EC2 GPU-enabled instance 
This is an example of how we attached a client using a pre-configured GPU instance in AWS EC2. 
We used the US East (N. Virginia) region, so you might need to adjust AMIs if you use a different region. 

1. Launch a GPU-equipped intance using a Amazon Linux AMI preconfigured with Nvidia drivers and Nvidia-docker. We used 'g3.4xlarge (M60)' and the AMI 'Deep Learning AMI GPU CUDA 11.4.3 (Amazon Linux 2) 20220316'.
2. Follow the general instruction above to clone this repository, stage the dataset, and add 'client.yaml'. 
3. This AMI does not come with docker-compose, so we will instead start the client using Docker: 

Build the image:
```
docker build . -t assist 
```

Start the client in a container. Replace <IP> with the IP-address provided by the workshop host, and give the client a recognizable name (spaces, dashes and underscores in the name are not allowed): 

```
docker run -v /home/ec2-user/ASSIST-workshop-120522/data/:/app/data:ro -v /home/ec2-user/ASSIST-workshop-120522/client.yaml:/app/client.yaml --add-host=combiner:<IP> --gpus all assist:latest /venv/bin/fedn run client -in client.yaml --name YOURNAME
```



