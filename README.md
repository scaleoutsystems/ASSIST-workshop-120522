# ASSIST-workshop-120522
Scaleouts ASSIST worskhop

Prerequisites
-------------

-  `Docker <https://docs.docker.com/get-docker>`
-  `Docker Compose <https://docs.docker.com/compose/install>`
-  `Python 3.8 <https://www.python.org/downloads>`

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
- Download your local dataset partition from XXX and move it to the data folder.
- Unzip your local dataset (inside the data folder):
```
unzip dataset.zip
```
- Download the client.yaml file from XXX and put it in the ASSIST-workshop-120522 folder.

- Open the docker-compose.yaml in your prefered editor and add the server ip adress that the workshop is providing to you, to the combiner namespace, line X:
```
client0:
  extra_hosts:
    combiner: XXX.XXX.XX.XX
```
Connect to the Reducer server:
```
docker-compose up
```
Make sure the terminal shows: CLIENT active
Now wait for the Reducer to start the federation.
