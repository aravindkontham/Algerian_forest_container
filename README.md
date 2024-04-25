# Algerian_forest_container

### Step 1: Search the image of Jupiter
```
docker search tensorflow
```
### step 2: Pull the jupyter/tensorflow-notebook
```
docker pull jupiter/tensorflow-notebook
```
### step 3: Create a container with the pulled image
```
docker run -it -p 8000:8888 --name jupyter jupyter/tensorflow-notebook
```
### step 4: Create yaml file 
```services:
   transformers-notebook:
      build: ./
      # image: jupyter/tensorflow-notebook
      ports:
        - 4000:8888
      environment:
        - JUPYTER_TOKEN=mlforest
      volumes:
        - ./:/home/jovyan

```
### step 5: Create a dockerfile
```
FROM jupyter/tensorflow-notebook
# COPY requirements.txt Google_trans.ipynb ./
# # Copy requirements.txt into the Docker image
# COPY requirements.txt /tmp/requirements.txt
     
USER $NB_UID
RUN pip install --upgrade pip && \
    pip install transformers && \
    pip install pysrt && \
    pip install googletrans==4.0.0-rc1 && \
    fix-permissions "/home/${NB_USER}"
    
COPY  Algerian_forest_fires_dataset_UPDATE.csv Algerian_forest.ipynb ./

```

### Step 6: Docker compose with the written yaml file and dockerfile
```
docker-compose up
```
### check the files
![Screenshot 2024-04-25 093455](https://github.com/aravindkontham/Algerian_forest_container/assets/92075632/60c2dc60-a41c-4fc5-9375-171726710bd6)


### Step 7: Change the image tag
```
docker image tag ml_devops-transformers-notebook:latest aravindkontham/ml_forest_fire:1.0
```
### Step 8: Push the image to the docker hub
```
docker push aravindkontham/ml_forest_fire:1.0
```
### check in the docker hub
![Screenshot 2024-04-25 092756](https://github.com/aravindkontham/Algerian_forest_container/assets/92075632/1d534499-8e8e-4ff1-955a-c49b1d2e5552)


## To test the container
### 1. pull the image from the docker hub

```
docker pull aravindkontham/ml_forest_fire:1.0
```
### 2. Create and run the container with the pulled image
```
docker run -p 1000:8888 aravindkontham/ml_forest_fire:1.0
````
### 3. check the container
![Screenshot 2024-04-25 093229](https://github.com/aravindkontham/Algerian_forest_container/assets/92075632/ae4c930e-de4c-4fbd-a5cd-90d19ea2963e)

