---
layout: main-anchor
title: tutorial
order: 7
collection: pages_2020
---
### Run your model in Docker
1. You can walk through Step 1-12 from strach to understand the whole pipeline
2. If you have your own code/model ready, you can **skip** Step 3 and Step 6-9, just copy your data to the container by

`docker cp <local_data_path>:[containerID]:<docker_data_path>`

### Training a TensorFlow-based Transformer Model from Scratch in Docker

We will dive head-first into training a transformer model from scratch using a TensorFlow GPU Docker image.


#### Step 1) Launch TensorFlow GPU Docker Container

Using Docker allows us to spin up a fully contained environment for our training needs. We always recommend using Docker, as it allows ultimate flexibility (and forgiveness) in our training environment. To begin we will open a terminal window and enter the following command to launch our NVIDIA CUDA powered container.

`nvidia-docker run -it -p 6007:6006 -v /data:/datasets tensorflow/tensorflow:1.15.0-gpu-py3 bash`

Note: A quick description about the key parameters of the above command (if you’re unfamiliar with Docker).

Docker Syntax|	Description
-|-
nvidia-docker run|	The 'docker run' command specifies the container from. Note in this case we use ‘nvidia-docker run’ to utilize CUDA powered NVIDIA GPUs.
-p 6007:6006|	Expose port 6007 [HOST:CONTAINER] for Tensorboard, type localhost:6007 in your browser to view Tensorboard
-v data:/datasets|	Volume tag, This shares the folder '/data' on the host machine to the /datasets folder in the container. Also explained as: -v /[host folder]:/[container folder]
tensorflow/tensorflow:nightly-gpu|	This the docker image that will run. The Docker Hub format is [PUBLISHER]/[IMAGE REPO]:[IMAGE TAG]

##### hint
You can also use the framework combination named [Deepo](https://github.com/ufoym/deepo)

#### Step 2) Install git
This may be necessary if you are running a fresh docker container.

`apt-get install git`


#### Step 3) Download 'Models' (Transformer Codebase is included here)
In case you do not have the latest up-to-date codebase for the models, the transformer network model is included here and the devs tend to update it quite frequently.

`mkdir /tf-1.5; cd /tf-1.5`  
`git clone https://github.com/tensorflow/models.git`

#### Step 4) Install Requirements for TensorFlow Models
As a necessary step,this will install the python package requirements for training TensorFlow models.

`# cd to the models dir`  
`pip install --user -r official/requirements.txt`


#### Step 5) Export Pythonpath
Export PYTHONPATH to the folder where the models folder are located on your machine. The command below references where the models are located on our system. Be sure to replace the `/transformer/models` syntax with the data path to the folder where you stored/downloaded your models.

`export PYTHONPATH="$PYTHONPATH:/tf-1.5/models"`

#### Step 6) Download and Preprocess the Dataset
The `data_download.py` command will download and preprocess the training and evaluation WMT datasets. Upon download and extraction, the training data is used to generate for what we will use as `VOCAB_FILE` variables. Effectively, the eval and training strings are tokenized, and the results are processed and saved as TFRecords.

NOTE: ([per the official requirements](https://github.com/tensorflow/models/tree/master/official/transformer)): 1.75GB of compressed data will be downloaded. In total, the raw files (compressed, extracted, and combined files) take up 8.4GB of disk space. The resulting TFRecord and vocabulary files are 722MB. The script takes around 40 minutes to run, with the bulk of the time spent downloading and ~15 minutes spent on preprocessing.

`cd /tf-1.5/models/official/transformer`  
`python data_download.py --data_dir=/datasets/transformer`

**Note**: you can skip step 7-9 if you already finished training your model, just test it in the docker from Step 10

#### Step 7) Set Training Variables for the Transformer Model
##### 'PARAM_SET'
This specifies what model to train. `big` or `base`
`PARAM_SET=base`

##### 'DATA_DIR'

This variable should be set to where the training data is located.

`DATA_DIR=/datasets/transformer`

##### 'MODEL_DIR'

This variable specifies the model location based on what model is specified in the `PARAM_SET` variable

`MODEL_DIR=/transformer/model_$PARAM_SET`

##### 'VOCAB_FILE'

This variable expresses where the location of the preprocessed vocab files are located.

`VOCAB_FILE=$DATA_DIR/vocab.ende.32768`

##### 'EXPORT_DIR' Export trained transformer model

This will specify the location when/where you export the model in Tensorflow SavedModel format. This is done when using the flag `export_dir` when training in step 8.

`EXPORT_DIR=/transformer/saved_model`

```
PARAM_SET=base
DATA_DIR=/datasets/transformer
MODEL_DIR=/transformer/model_$PARAM_SET
VOCAB_FILE=$DATA_DIR/vocab.ende.32768
EXPORT_DIR=/transformer/saved_model
```

#### Step 8) Train the Transformer Model
The following command ‘python transformer_main.py’ will train the transformer for a total of 260,000 steps. See how the flags are set up to reference the variables you set in the previous steps. You can train for less than 260,000 steps, it’s up to you.

NOTE: This will take a long time to train depending on your GPU resources. The official TensorFlow transformer model is under constant development, be sure to check periodically on their github for any latest optimizations and techniques to reduce training times.


`python transformer_main.py --data_dir=$DATA_DIR --model_dir=$MODEL_DIR --vocab_file=$VOCAB_FILE --param_set=$PARAM_SET --bleu_source=$DATA_DIR/newstest2014.en --bleu_ref=$DATA_DIR/newstest2014.de --train_steps=260000 --steps_between_evals=1000 --export_dir=$EXPORT_DIR`


#### Step 9) View Transformer Model Results in Tensorboard
As we noted earlier, we can check the status of training in the Tensorboard GUI. To check in real time, run the following command in a separate terminal (or TensorFlow container), and type localhost:6007 in your browser to view Tensorboard. You can also wait until training is complete to use the current container.

`tensorboard --logdir=$MODEL_DIR`

#### Step 10) Test the Trained Transformer Network (Translate English to German)
Now we’ve trained our transformer network, let’s enjoy the fruits of our labor using translate.py! In the command below, replace the text “hello world” with desired text to translate

#### Step 11) `python translate.py --model_dir=$MODEL_DIR --vocab_file=$VOCAB_FILE \
--param_set=$PARAM_SET --text="hello world"`

#### Step 12) save your container to a image
1. Create an account and a repo on Docker Hub, named  **[UserID]** and **[Repo]**
2. Get the **[containerID]** you want by `docker ps -l`
3. construct the image locally  
`docker commit [containerID] [UserID]/[Repo]`
4. check the image  
`docker images`
5. Upload your image to Docker Hub, you may be prompted with username and password of Docker Hub    
`docker push [UserID]/[Repo]`