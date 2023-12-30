---
layout:       post
title: Xilinx Vitis AI安装步骤-包括Ubuntu、Docker安装
subtitle: 
date: 2023-06-04 17:00:00 +0800
author:       "Yang"
categories: [软件安装, VCK5000]
tags: 
    - 软件安装 
    - VCK5000
catalog:      true # 是否用目录
header-img:  
header-style:  # 要不要用图片
header-mask:  # 图片阴暗程度 如果不用图片就设置为0
multilingual: false # 如果为true则会在文章开头显示中英文
mathjax: true # 数学公式？
published: true # 是否展示在页面，为false则完全找不到
hidden: false # 是否展示在主页，不展示在主页在分类里面还可以看见

description: Transformers入门，Huggingface，Finetune，BERT # 没用
---


# 环境安装流程 

---

[toc]

---

## Ubuntu 20.04 安装
1. 下载镜像：[ubuntu-20.04.6-desktop-amd64.iso](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/20.04/ubuntu-20.04.6-desktop-amd64.iso)
2. 下载 rufus: [官网地址](https://rufus.ie/zh/)
3. 制作USB启动盘
4. 开机按 __Delete__ 键进入 BIOS
5. 启动项将首选项改为 USB 启动盘
6. 重新启动进入安装程序
    * 选择 English
    * 有线网账号密码：7220044 | Fpga123-123，获得 IP （例如：113.54.130.163）
    * 选择 Mininal installation
    * 选择 Erase disk and install Ubuntu
    * 设置用户名密码是：shao21 | UESTC-shao21
7. 安装配置 ssh
```bash
sudo apt-get update
sudo apt install openssh-server
sudo apt-get install vim
sudo vim /etc/ssh/sshd_config
```
端口号修改为23321后保存，继续执行
```bash
sudo systemctl restart sshd
sudo ufw allow 23321
```
8. 关闭自动锁屏：
    * 点击右上角 Settings
    * 点击 Privacy
    * 点击 Screen Lock
    * 关闭自动锁屏
---

## CUDA 11.3 & cuDNN 安装
1. 查看当前驱动
```bash
dpkg -l | grep nvidia
```
2. 卸载原本的驱动并清理链接
```bash
sudo apt-get purge nvidia*
sudo apt autoremove
```
3. 查询可用驱动
```bash
ubuntu-drivers devices
```
4. 自动安装推荐的驱动
```bash
sudo ubuntu-drivers autoinstall
```
5. 重启，然后验证驱动是否安装成功
```
sudo reboot
nvidia-smi
```
6. 下载并运行 CUDA 11.3.1 安装程序
```bash
cd ~
wget https://developer.download.nvidia.com/compute/cuda/11.3.1/local_installers/cuda_11.3.1_465.19.01_linux.run
sudo apt install gcc
sudo sh cuda_11.3.1_465.19.01_linux.run
```
7. 只勾选 __CUDA Toolkit 11.3__，然后安装
8. 添加环境变量
```bash
sudo vim /etc/profile
```
```bash
export CUDA_HOME=/usr/local/cuda-11.3
export PATH=$PATH:$CUDA_HOME/bin
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/cuda-11.3/lib64
```
9. 下载并安装 cuDNN 8.9.2.26
```bash
cd ~
wget https://developer.nvidia.com/downloads/compute/cudnn/secure/8.9.2/local_installers/11.x/cudnn-linux-x86_64-8.9.2.26_cuda11-archive.tar.xz
tar -xvf cudnn-linux-x86_64-8.9.2.26_cuda11-archive.tar.xz
cd cudnn-linux-x86_64-8.9.2.26_cuda11-archive
sudo cp -r ./bin/* /usr/local/cuda-11.3/bin
sudo cp -r ./lib/* /usr/local/cuda-11.3/lib64
```
10. 验证是否安装成功
```bash
source /etc/profile
nvcc -V
nvidia-smi
```

---

## docker & nvidia docker 安装
1. 安装docker
```bash
sudo apt-get install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
docker version
```
2. 安装 nvidia container toolkit
```bash
sudo apt-get install curl
wget https://download.docker.com/linux/ubuntu/gpg
sudo apt-key add gpg
vim installNvidiaContainer.sh
```
```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
sudo curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
sudo curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
```
保存后执行
```bash
./installNvidiaContainer.sh
sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker
rm installNvidiaContainer.sh
```
3. 创建多个新用户并添加docker用户组权限
```bash
cd ~
vim addUsers.sh
```
```bash
for name in aifpga maomao yangyang lichangyv
do
    echo $name
    useradd -d /home/$name -m -s /bin/bash $name
    echo $name:$name | chpasswd
    usermod -aG docker ${name}
    # passwd --expire $name
    echo "$user add successfuly"
done
```
保存后执行
```bash
./addUsers.sh
```

---

## Vitis & Vivado & Vitis HLS 安装
1. 下载 Vitis 包并进入目录
2. 配置 dash（键盘选择 __No__）
```bash
sudo dpkg-reconfigure dash 
```
3. 安装依赖包并执行安装程序
```bash
sudo apt-get install ocl-icd-libopencl1
sudo apt-get install opencl-headers
sudo apt-get install ocl-icd-opencl-dev
sudo apt install libstdc++6
sudo apt install libncurses5
sudo apt-get install libtinfo5
sudo chmod +x xsetup
sudo ./xsetup
```
4. 选择安装内容（需在本机使用图形界面操作）
    1. 选择 __Vitis__
    2. 选择以下内容（共210.68GB）
        * __Vitis Unified Software Platform__
        * __Vitis Model Composer__
        * __DocNav__
        * __Install devices for Alveo and edge acceleration platforms__
        * __Install Devices for Kria soMs and starter Kits__
        * __Devices for Custom Platforms__
        * __Engineering Sample Devices for Custom Platforms__
    3. 其他配置默认，然后等待安装完成
5. 配置环境
```bash
sudo vim /etc/profile
```
```bash
source /tools/Xilinx/Vivado/2023.1/settings64.sh
source /tools/Xilinx/Vitis/2023.1/settings64.sh
source /tools/Xilinx/Vitis_HLS/2023.1/settings64.sh
```
6. 安装 USB 驱动
```bash
cd /tools/Xilinx/Vivado/2023.1/data/xicom/cable_drivers/lin64/install_script/install_drivers
sudo ./install_drivers
```
7. 验证是否安装成功
```bash
source /etc/profile
vitis
vivado
vitis_hls
```
无论执行哪一个都有图形界面弹出

---

## Vitis AI 安装
1. 克隆 Vitis AI 仓库
```bash
cd ~
git clone https://github.com/Xilinx/Vitis-AI
```
2. 构建基于 Pytorch-CUDA 的镜像
```bash
cd Vitis-AI/docker
./docker_build.sh -t gpu -f pytorch
```
3. 验证是否安装成功
```bash
cd ../
./docker_run.sh xilinx/vitis-ai-pytorch-gpu:3.5.0.001-a350fc104
```

---

