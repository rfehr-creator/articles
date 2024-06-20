---
title: Tensorflow (Debian)
layout: default
parent: WSL
---

# How to install Tensorflow in WSL Debian with Cuda
## Prerequisites
1. Nvidia driver installed 
2. New WSL Debian environment

## Install Prerequisites
```
sudo apt update
sudo apt install wget
```

## Install Nvidia Toolkit 12.5
```
sudo wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo wget https://developer.download.nvidia.com/compute/cuda/12.5.0/local_installers/cuda-repo-wsl-ubuntu-12-5-local_12.5.0-1_amd64.deb
sudo dpkg -i cuda-repo-wsl-ubuntu-12-5-local_12.5.0-1_amd64.deb
sudo cp /var/cuda-repo-wsl-ubuntu-12-5-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-5
```

## Install pip
```
sudo apt-get install python3-pip
```

## Install Python Virtual Environement
```
sudo apt install python3.11-venv
python3 -m venv .venv
source .venv/bin/activate
```

## Install Tensorflow
```
python3 -m pip install tensorflow[and-cuda]
```

## Add Environment Variables
```
export CUDNN_PATH=$(dirname $(python -c "import nvidia.cudnn;print(nvidia.cudnn.__file__)"))
export LD_LIBRARY_PATH=${CUDNN_PATH}/lib
```

## Verify Tensorflow Installed Correctly
```
python3 -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```
