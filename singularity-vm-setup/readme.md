# Configure Singularity dev environment 

Since the Mac containers are broken for the current version of Vagrant (see [#1568](https://github.com/singularityware/singularity/issues/1568)), the best way is to create a new development with a Xenial base image.



Mac terminal

```shell
brew cask install virtualbox vagrant vagrant-manager
vagrant plugin install vagrant-vbguest
mkdir singularity-vm && cd singularity-vm
singularity init ubuntu/xenial64
vagrant up
vagrant ssh
```


Ubuntu terminal, following instructions from: http://singularity.lbl.gov/install-linux

```Shell
sudo apt-get install libarchive-dev squashfs-tools
$VERSION=2.5.1
wget https://github.com/singularityware/singularity/releases/download/$VERSION/singularity-$VERSION.tar.gz
tar xvf singularity-$VERSION.tar.gz
cd singularity-$VERSION
./configure --prefix=/usr/local
make
sudo make install
```

