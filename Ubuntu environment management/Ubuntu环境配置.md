@[toc]
# Ubuntu（22.04）环境配置
## Python
安装pycharm，[官网](https://www.jetbrains.com/pycharm/download/#section=linux)提供的安装方法
```bash
sudo snap install [pycharm-professional|pycharm-community] --classic
```
安装toolbox，从jetbrains官网下载toolbox压缩包，然后解压
```bash
tar xvzf xxx.tar.gz
```
解压后运行，需要使用AppImages，需要FUSE，[官方wiki](https://github.com/AppImage/AppImageKit/wiki/FUSE)

安装pip（若没有安装python，则会自动安装python）
```bash
sudo apt-get install pip
```
## Vim
安装Vim
```bash
sudo apt-get install vim
```

```

## 显卡驱动
检测显卡类型，查看推荐的显卡驱动
```bash
ubuntu-drivers devices
```
安装所有推荐驱动
```bash
sudo ubuntu-drivers autoinstall
```
安装一个驱动
```bash
sudo apt install nvidia-xxx
```
xxx为选择的版本号

## CUDA与CUDNN
安装CUDA，[官网](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=runfile_local)有详细的指导
注意需要支持CUDA的显卡，版本匹配的gcc
使用命令nvidia-smi查看合适的CUDA版本
使用下面的命令进行安装（不同的机器不同）
```bash
wget https://developer.download.nvidia.com/compute/cuda/11.7.1/local_installers/cuda_11.7.1_515.65.01_linux.run
sudo sh cuda_11.7.1_515.65.01_linux.run
```
然后根据提示安装CUDA，安装后，修改.bashrc，增加两条
```bash
export PATH=/usr/local/cuda-11.7/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-11.7/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
命令nvcc -V查看CUDA版本

安装cudnn，前往[官网](https://developer.nvidia.com/rdp/cudnn-download)选择合适的版本，官方有详细的[教程](https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html)
从官网下载后，Enable the local repository，其中${OS}就是ubuntu2204
```bash
sudo dpkg -i cudnn-local-repo-${OS}-8.x.x.x_1.0-1_amd64.deb
```
Import the CUDA GPG key.
```bash
sudo cp /var/cudnn-local-repo-*/cudnn-local-*-keyring.gpg /usr/share/keyrings/
```
Refresh the repository metadata.
```bash
sudo apt-get update
```
Enable the repository. 
```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/${OS}/x86_64/cuda-${OS}.pin 
sudo mv cuda-${OS}.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/${OS}/x86_64/3bf863cc.pub
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/${OS}/x86_64/ /"
sudo apt-get update
```
Copy the cuDNN samples to a writable path.
```bash
cp -r /usr/src/cudnn_samples_v8/ $HOME
```
Compile the mnistCUDNN sample.
```bash
$make clean && make
```
如果在执行make clean && make过程中出现test.c:1:10: fatal error: FreeImage.h: 没有那个文件或目录
那么就执行这一步：
```bash
sudo apt-get install libfreeimage3 libfreeimage-dev
```
Run the mnistCUDNN sample.
```bash
$ ./mnistCUDNN
```
If cuDNN is properly installed and running on your Linux system, you will see a message similar to the following:
```bash
Test passed!
```

