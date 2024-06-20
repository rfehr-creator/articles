---
title: PyTorch (Ubuntu)
layout: default
parent: WSL
---

# How to install PyTorch on WSL Ubuntu with Cuda
Prerequisites
1. Nvidia driver installed 
2. New wsl ubuntu environment


```
sudo apt update
```

Install Nvidia Toolkit 12.5
```
sudo wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo wget https://developer.download.nvidia.com/compute/cuda/12.5.0/local_installers/cuda-repo-wsl-ubuntu-12-5-local_12.5.0-1_amd64.deb
sudo dpkg -i cuda-repo-wsl-ubuntu-12-5-local_12.5.0-1_amd64.deb
sudo cp /var/cuda-repo-wsl-ubuntu-12-5-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-5
```

Install pip
```
sudo apt-get install python3-pip
```

Install Pytorch
```
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

Verify Pytorch is installed
```
python3 -c "import torch; print(torch.cuda.is_available())"
```
