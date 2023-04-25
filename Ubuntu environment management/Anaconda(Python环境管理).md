@[toc]

# Anaconda
从[官网](https://www.anaconda.com/)下载Anaconda Distribution，然后运行
```bash
bash xxx
```
xxx为下载的文件，一路回车加yes就可以了

修改conda采用的镜像源，增加清华的镜像源
```bash
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - defaults    
```

## conda的使用
创建虚拟环境
```bash
conda create -n env_name python=x.x.x
```
其中，env_name是虚拟环境的名字，x.x.x是python的版本

查看虚拟环境列表
```bash
conda env list
```
所有的环境储存在目录 anaconda/envs 中

激活与关闭虚拟环境
```bash
conda activate env_name
conda deactivate
```
删除虚拟环境
```bash
conda remove --name myenv --all
```

## Jupyter notebook
想要在不同的虚拟环境中使用jupyter notebook，需要配置对应的内核，可以参考[ipython官方教程](https://ipython.readthedocs.io/en/stable/install/kernel_install.html#kernels-for-different-environments)
首先，激活环境，myenv是虚拟环境名
下载pip
```bash
source activate myenv
conda install pip
conda install ipykernel
```
然后使用ipykernel命令，创建内核，即可使用
```bash
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```
--display-name参数后面接内核的名字（你取的）
比如，我为虚拟环境pytorch创建议个内核
```bash
python -m ipykernel install --user --name pytorch --display-name "Python (pytorch)"
```

命令jupyter --paths可以查看jupyter内核所在路径
```bash
$ jupyter --paths
config:
    /home/skf/anaconda3/envs/pytorch/etc/jupyter
    /home/skf/.jupyter
    /home/skf/.local/etc/jupyter
    /usr/local/etc/jupyter
    /etc/jupyter
data:
    /home/skf/anaconda3/envs/pytorch/share/jupyter
    /home/skf/.local/share/jupyter
    /usr/local/share/jupyter
    /usr/share/jupyter
runtime:
    /home/skf/.local/share/jupyter/runtime
```
可以在目录~/.local/share/jupyter/kernels中看到你的内核配置目录
```bash
~/.local/share/jupyter/kernels $ ls
pytorch
```
上面的pytorch是我配置的一个虚拟环境pytorch的jupyter内核配置目录

打开jupyter notebook，创建新文件时可以选择加载的内核
![在这里插入图片描述](https://img-blog.csdnimg.cn/5b8ec5fd1163414692c66c39cdf45ef6.png#pic_center)
在编辑文件或运行时也可以选择内核
![在这里插入图片描述](https://img-blog.csdnimg.cn/0984fb461f43401486d6e943a8bad8f6.png#pic_center)


