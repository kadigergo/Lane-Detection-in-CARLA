
# we need Ubuntu 20.04 LTS WSL
- wsl --install -d Ubuntu-20.04
- wsl -d Ubuntu-20.04


# install pyenv + python 3.8.5
- sudo apt update
- sudo apt install -y software-properties-common build-essential \
    libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev \
    curl libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev \
    libffi-dev liblzma-dev git

- curl https://pyenv.run | bash


- echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
- echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
- echo 'eval "$(pyenv init - bash)"' >> ~/.bashrc
- . ~/.bashrc

- pyenv install 3.8.5

- pyenv version
- pyenv virtualenv 3.8.5 lane-detection
- pyenv activate lane-detection
- pyenv virtualenvs

- sudo apt -y install unzip nvidia-utils-575

# based on https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_network
- wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.1-1_all.deb
- sudo dpkg -i cuda-keyring_1.1-1_all.deb
- sudo apt-get update
#sudo apt-get -y install cuda-toolkit-11-8
- sudo apt install libcusolver10 libcudnn8



#  https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_network
- wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-keyring_1.0-1_all.deb
- sudo dpkg -i cuda-keyring_1.0-1_all.deb
- sudo apt-get update
- sudo apt-get -y install cuda-11-8
#sudo apt install libcusolver10 libcudnn8


# ha nem jo lefut cpu-n:
  3/456 [..............................] - ETA: 1:28:25 - loss: 0.9575 - dice: 0.0352

# test with
- python testnvidia.py




# set up project https://github.com/kadigergo/Lane-Detection-in-CARLA?tab=readme-ov-file
1. git clone git@github.com:kadigergo/Lane-Detection-in-CARLA.git
2. cd Lane-Detection-in-CARLA
3.  pyenv local 3.8.5
4. mkdir carla-dataset; cd carla-dataset
5. curl -L -o dataset.zip  https://www.kaggle.com/api/v1/datasets/download/thomasfermi/lane-detection-for-carla-driving-simulator
6. unzip dataset.zip
7. cd ..
8. pip install -r requirements.txt
9. python main.py

# for the "Could not load library libcublasLt.so.12. Error: libcublasLt.so.12: cannot open shared object file: No such file or directory" error:
`sudo apt-get install libcublas-12-5`

# cleanup: 
```
sudo apt-get remove -y cuda-cccl-11-8 cuda-command-line-tools-11-8 cuda-compiler-11-8 cuda-cudart-11-8 cuda-cudart-dev-11-8  cuda-cuobjdump-11-8 cuda-cupti-11-8 cuda-cupti-dev-11-8 cuda-cuxxfilt-11-8 cuda-documentation-11-8 cuda-driver-dev-11-8 cuda-gdb-11-8 cuda-keyring cuda-memcheck-11-8 cuda-nsight-11-8 cuda-nsight-compute-11-8 cuda-nsight-systems-11-8 cuda-nvcc-11-8 cuda-nvdisasm-11-8 cuda-nvml-dev-11-8 cuda-nvprof-11-8 cuda-nvprune-11-8 cuda-nvprune-11-8 cuda-nvrtc-11-8 cuda-nvrtc-dev-11-8 cuda-nvtx-11-8 cuda-nvvp-11-8 cuda-profiler-api-11-8 cuda-sanitizer-11-8 cuda-toolkit-11-8-config-common cuda-toolkit-11-config-common cuda-toolkit-12-config-common cuda-toolkit-12-3-config-common cuda-toolkit-config-common libcusolver-11-0 libcusolver10 libcublas-12-5
```
```
 sudo dpkg --purge  cuda-cccl-11-8 cuda-command-line-tools-11-8 cuda-compiler-11-8 cuda-cudart-11-8 cuda-cudart-dev-11-8  cuda-cuobjdump-11-8 cuda-cupti-11-8 cuda-cupti-dev-11-8 cuda-cuxxfilt-11-8 cuda-documentation-11-8 cuda-driver-dev-11-8 cuda-gdb-11-8 cuda-keyring cuda-memcheck-11-8 cuda-nsight-11-8 cuda-nsight-compute-11-8 cuda-nsight-systems-11-8 cuda-nvcc-11-8 cuda-nvdisasm-11-8 cuda-nvml-dev-11-8 cuda-nvprof-11-8 cuda-nvprune-11-8 cuda-nvprune-11-8 cuda-nvrtc-11-8 cuda-nvrtc-dev-11-8 cuda-nvtx-11-8 cuda-nvvp-11-8 cuda-profiler-api-11-8 cuda-sanitizer-11-8 cuda-toolkit-11-8-config-common cuda-toolkit-11-config-common cuda-toolkit-12-config-common cuda-toolkit-12-3-config-common cuda-toolkit-config-common libcusolver-11-0 libcusolver10 libcublas-12-5
```
