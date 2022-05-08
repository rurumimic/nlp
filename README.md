# NLP

## Setup

1. [Enable NVIDIA CUDA on WSL](https://docs.microsoft.com/en-us/windows/ai/directml/gpu-cuda-in-wsl)
   - Windows 11, Windows 10 version 21H2
   - Install the GPU driver: [NVIDIA Driver Downloads](https://www.nvidia.com/download/index.aspx)
   - Kernel 5.10.43.3+: `wsl cat /proc/version`
   - Ubuntu 20.04, Docker 19+
2. Install [nvidia-docker](https://github.com/NVIDIA/nvidia-docker)
   - [Install Guide](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#install-guide)
     - [Install NVIDIA Toolkit](#install-nvidia-toolkit)
   - [WSL 2 GPU Support for Docker Desktop on NVIDIA GPUs](https://www.docker.com/blog/wsl-2-gpu-support-for-docker-desktop-on-nvidia-gpus/)
   - [Getting Started with CUDA on WSL 2](https://docs.nvidia.com/cuda/wsl-user-guide/index.html#getting-started-with-cuda-on-wsl)

### Install NVIDIA Toolkit

- [Setting up NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#setting-up-nvidia-container-toolkit)

Setup the package repository sand the GPG key:

```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
    && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
    && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
        sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
        sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
```

Install the nvidia-docker2 package:

```bash
sudo apt-get update
sudo apt-get install -y nvidia-docker2
```

Restart docker.

Check docker image version: [nvidia/cuda](https://hub.docker.com/r/nvidia/cuda/tags/)

Test. run a base CUDA container: 

```bash
sudo docker run --rm --gpus all nvidia/cuda:11.6.1-base-ubuntu20.04 nvidia-smi
```

```bash
NVIDIA-SMI couldn't find libnvidia-ml.so library in your system. Please make sure that the NVIDIA Display Driver is properly installed and present in your system.
Please also try adding directory that contains libnvidia-ml.so to your system PATH.
```
