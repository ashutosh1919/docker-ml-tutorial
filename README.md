# Machine Learning on Docker Containers
In this tutorial, you will learn closely working with docker for your Machine Learning or Data Science use cases.

## Prerequisite
- Download and install Docker from [here](https://docs.docker.com/get-docker/) depending upon your system.
- Open the fresh Docker terminal with good internet connection.

## Tutotial Objectives
- To download the Titanic Survival dataset.
- To perform data cleaning and preprocessing
- To build XGBooost/LGBM Model for given data.

## Step 1: Pull Image and Run the Image
- Pull the prebuilt docker image [datmo/xgboost](https://hub.docker.com/r/datmo/xgboost/tags) using below command.
  - `docker pull datmo/xgboost:cpu`
- Run the docker image as container using following command.
  - `docker run -i -t --name xgboost_container -p 8080:80 datmo/xgboost:cpu /bin/bash`
  - Note here that we have provided the name of the created container as `xgboost_container`.
  - We have also enabled port forwarding. Here `8080:80` means that port 8080 of host (your system) and 80 of docker container. The information can be sent from host to container and vice versa from these respective ports.
- Now move to src dir using `cd usr/src/`.

## Step 2: Download the Dataset
- Firstly, created a dir in home dir of container using `mkdir docker_ml_tutorial`.
- Download csv file containing dataset from [here](https://www.kaggle.com/c/titanic/data).
- Now you have dataset in your system. But how can we move it into our container?
- So, here is the power of docker where you can copy data from system to container and vice versa. Same thing we will do here using below command.
- Go into the directory where you have downloaded dataset `train.csv` file and execute following command in a new terminal.
  - `docker cp titanic.csv xgboost_container:/usr/src/docker_ml_tutorial/`
- Now you can go into `docker_ml_tutorial` dir in container and execute `ls` and you can see the file `train.csv` in here.

## Step 3: Configuring your Python Environment
- Check your python version using `python --version`, if it is lesser than python 3.5, then run following commands.
  - `apt-get update -y`
  - `apt install software-properties-common`
  - `add-apt-repository ppa:deadsnakes/ppa`
  - `apt-get update`
  - `apt install python3.7`
  - `update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 1`
  - `apt-get install python3-pip`

## Step 4: Running Jupyter Notebook inside Container
- Now we know that if we run jupyter notebook, we need to open it in browser and for that we need to run notebook on port 80 in container because that's the port which is exposed.
  - `jupyter notebook --ip=0.0.0.0 --port=80`
  - Also note here that we have provided IP as `0.0.0.0` it means this notebook is exposed to all IPs of your host.
  - After running the command, you will see token for the notebook on docker terminal, copy that token and save it for later use.
- Now, you need to see the IP address of your docker-machine. You can get that using below command.
  - `docker-machine ip default`
  - Note here that `default` is the name of my docker-machine. If your system has different name then you can put that instead of `default`.
  - You will get IP of docker machine with this command and IP will look something like `192.168.99.100`. Note that it may be different than this.
- Open the fresh browser tab and copy the IP address and write port as `https://192.168.99.100:8080` and give Enter.
  - Note here that port 8080 of host takes the data forwared by port 80 of docker container.
- You need to enter the token which you have copied previously and now you can access the notebook running inside container from your browser.

## Step 5: Do your ML work
- Create new Python 3 Notebook.
- Import data using pandas and clean data.
- Build Model.
- Take a look at the notebook given in this repository for example.

