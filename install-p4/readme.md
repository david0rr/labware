# Install P4 (2018)

Installs a release rather than Git.



## Ubuntu 16.04 VM

```shell
apt-get install python-numpy python-scipy python-dev libgsl-dev

wget https://github.com/pgfoster/p4-phylogenetics/archive/1.2.tar.gz
tar -xzf 1.2.tar.gz
cd p4-phylogenetics-1.2
vim setup.py
# Redefine the below vars, save and exit
# my_include_dirs = ['/usr/include']
# my_lib_dirs = ['/usr/lib/x86_64-linux-gnu']

python setup.py build
python setup.py install
p4 # installed in $PATH
```



## ARC3

```shell
module load python/2.7.13
module load gsl

pip install --user numpy scipy

wget ftp://ftp.gnu.org/gnu/gsl/gsl-2.4.tar.gz
tar -xzf gsl-2.4.tar.gz
cd gsl-2.4
./configure && make

wget https://github.com/pgfoster/p4-phylogenetics/archive/1.2.tar.gz
tar -xzf 1.2.tar.gz
cd p4-phylogenetics-1.2
vim setup.py
# Redefine the below vars, save and exit
# my_include_dirs = ['/nobackup/fbsbco/p4/gsl-2.4']
# my_lib_dirs = ['/nobackup/fbsbco/p4/gsl-2.4']

python setup.py build
python setup.py install --user
cd bin
```

#### To run
```shell
module load gsl
cd bin
./p4 # NOT installed in $PATH, can be added manually

```
