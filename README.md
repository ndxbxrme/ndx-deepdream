# ndx-deepdream
## my adventures with [Google Deepdream](http://googleresearch.blogspot.ch/2015/06/inceptionism-going-deeper-into-neural.html)
i don't understand much or any of this and i hardly ever use linux, so i might not be of any use if you get stuck  
but this is how i have got it working  
![Example image](https://github.com/ndxbxrme/ndx-deepdream/blob/master/examples/maggie-eyes.jpg)  
starting with a blank Ubuntu 64bit Virtual Machine  
  
download [Anaconda](http://continuum.io/downloads)
```bash
sudo apt-get update
sudo apt-get install git
sudo apt-get install curl
sudo apt-get install build-essential libssl-dev
sudo apt-get install autoconf
sudo apt-get install libtool
sudo apt-get install libboost-all-dev
pip install scipy
sudo apt-get install python-scipy
sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev protobuf-compiler gcc-4.6 g++-4.6 gcc-4.6-multilib g++-4.6-multilib gfortran libjpeg62 libfreeimage-dev libatlas-base-dev git python-dev python-pip
sudo apt-get install cmake
sudo apt-get install liblmdb-dev
sudo apt-get install linux-headers-`uname -r`
sudo easy_install numpy

curl https://raw.githubusercontent.com/creationix/nvm/v0.13.1/install.sh | bash

cd Downloads/
bash Anaconda-2.3.0-Linux-x86.sh
cd ..

export CURL_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt

git clone https://github.com/google/protobuf.git
cd protobuf/
./autogen.sh
./configure
make
make check
sudo make install
cd ..

export LD_LIBRARY_PATH=/usr/local/lib

git clone https://github.com/google/glog.git
cd glog/
./configure
make
sudo make check
sudo make install
cd ..

wget https://github.com/schuhschuh/gflags/archive/master.zip
unzip master.zip
cd gflags-master/
mkdir build && cd build
export CXXFLAGS="-fPIC" && cmake .. && make VERBOSE=1
export CXXFLAGS="-fPIC" && cmake .. && make VERBOSE=1
make
sudo make install
cd ..
cd ..

curl -O "http://developer.download.nvidia.com/compute/cuda/6_5/rel/installers/cuda_6.5.14_linux_64.run"

git clone https://github.com/BVLC/caffe.git
cd caffe/
cp Makefile.config.example Makefile.config
```
if you don't have an Nvidia GPU edit Makefile.config to uncomment the line `CPU_ONLY := 1`
```bash
echo "CXX := /usr/bin/g++-4.6" >> Makefile.config
sed -i 's/CXX :=/CXX ?=/' Makefile.config
make all
make test
data/ilsvrc12/get_ilsvrc_aux.sh
sudo pip install -r python/requirements.txt
sudo ln -s /usr/include/python2.7/ /usr/local/include/python2.7
sudo ln -s /usr/local/lib/python2.7/dist-packages/numpy-1.8.1-py2.7-linux-x86_64.egg/numpy/core/include/numpy /usr/local/include/python2.7/numpy
make pycaffe
echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/lib' >> ~/.bashrc
source ~/.bashrc
sudo easy_install pillow
make runtest
export PYTHONPATH=/home/jeff/dev/caffe/python
cd ..

git clone https://github.com/ndxbxrme/ndx-deepdream.git
cd ndx-deepdream/
python deep.py
```
