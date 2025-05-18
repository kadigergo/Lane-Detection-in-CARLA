
# install pyenv + python 3.8.5
sudo apt update
sudo apt install -y software-properties-common build-essential \
    libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev \
    curl libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev \
    libffi-dev liblzma-dev git

curl https://pyenv.run | bash


echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init - bash)"' >> ~/.bashrc

pyenv install 3.8.5
pyenv local 3.8.5

penv version
pyenv virtualenv 3.8.5 lane-detection
pyenv activate lane-detection
pyenv virtualenvs

# install nvidia cuda (requires ubuntu 20)
# based on https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_network
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-9


# set up project https://github.com/kadigergo/Lane-Detection-in-CARLA?tab=readme-ov-file
1. git clone git@github.com:kadigergo/Lane-Detection-in-CARLA.git
2. cd Lane-Detection-in-CARLA
3. mkdir carla-dataset; cd carla-dataset
4. curl -L -o dataset.zip  https://www.kaggle.com/api/v1/datasets/download/thomasfermi/lane-detection-for-carla-driving-simulator
5. unzip dataset.zip
6. pip install -r requirements.txt

