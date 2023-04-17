# TAO_Yolo_V4
### This is a object detection demo using my own COCO datasets

#### we need the nvidia official TAO .zip file
$ wget --content-disposition https://api.ngc.nvidia.com/v2/resources/nvidia/tao/cv_samples/versions/v1.4.0/zip -O cv_samples_v1.4.0.zip

#### I used the TAO (built-in docker image) with Ubuntu X86-64 Nvidia 3080 to train a Yolo V4 tiny model for my airpods

### For environment
#### Install docker-ce

$ sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit-base

$  nvidia-ctk --version

$ sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml

$ sudo grep "  name:" /etc/cdi/nvidia.yaml

$ curl https://get.docker.com | sh && sudo systemctl --now enable docker


$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
      && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
      && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
            sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
            sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

$ sudo apt-get update

$ sudo apt-get install -y nvidia-container-toolkit

$ sudo nvidia-ctk runtime configure --runtime=docker

$ sudo systemctl restart docker

### Install conda        www.anaconda.com/download/

$ bash Anaconda3-2023.03-Linux-x86_64.sh

$ sudo apt install python-pip

$ pip list

$ pip install opencv-python==3.4.1.15

$ pip install opencv-contirb-python==3.4.1.15

$ sudo gedit /etc/apt/sources.list

$ conda create -n launcher python=3.6

$ conda activate launcher

$ pip3 install nvidia-tao

$ tao --help

$ tao info

$ wget --content-disposition https://api.ngc.nvidia.com/v2/resources/nvidia/tao/cv_samples/versions/v1.4.0/zip -O cv_samples_v1.4.0.zip

#### unzip to this locaton ~/cv_samples_v1.4.0

$ pip3 install jupyter

$ jupyter notebook password

### Run the TAO environment

$ conda env list

$ conda activate launcher

$ cd ~/cv_samples_v1.4.0/

$ jupyter notebook --ip 0.0.0.0 --allow-root --port 8888


#### Using TAO to convert coo dataset to tfrecord dataset
$ tao yolo_v4_tiny dataset_convert -d /workspace/tao-experiments/data/spec-train.txt -o /workspace/tao-experiments/data/training/tfrecords/train --gpu_index 0

$ tao yolo_v4_tiny dataset_convert -d /workspace/tao-experiments/data/spec-val.txt -o /workspace/tao-experiments/data/val/tfrecords/val --gpu_index 0

#### I used roboflow.com to build my airpods COCO datasets (100 photoes) and put it in  ~/cv_samples_v1.4.0/data/
![data](https://user-images.githubusercontent.com/56700281/232538829-ca532b46-61c7-40af-8046-f14a76b4e4e6.png)

#### Then follow the steps in yolo_v4_tiny.ipynb

![dir](https://user-images.githubusercontent.com/56700281/232539152-8fb29b29-a2a1-4c26-8a08-2fed177c41c1.png)

#### It costs 80 epoches to get 99.7%. Finally, I got results of my airpods
![微信图片_20230406105633](https://user-images.githubusercontent.com/56700281/232540414-d9a95e10-3b7f-4a12-bd6f-19802d8d5c68.jpg)
![微信图片_202304061056331](https://user-images.githubusercontent.com/56700281/232540453-f8645c53-1528-4129-bc47-09846aa7a498.jpg)

#### Have fun!


