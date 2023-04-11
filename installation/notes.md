## Launch an EC2:
- Name: d2l-cpu
- AMI: Ubuntu 22.04 (ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-20220609)
- Spec: c6i.8xlarge, 64GB EBS (gp3) /dev/sda1
- VPC: default, ap-northeast-1a, subnet public-1a
- Elastic IP: 54.249.149.5
- SG: d2l-sg (SSH, my IP)
- Key pair: ec2-tokyo
- SSH `ssh -i ec2-tokyo.cer ubuntu@54.249.149.5`

## Configure the dev environment
### Update, upgrade and install
```bash
# Update
$ sudo apt update
# Install build essential (CPP, etc.)
$ sudo apt install build-essential
# Upgrade
$ sudo apt -y upgrade
# Check Python3 version
$ python3 -V
# Install pip
$ sudo apt install -y python3-pip
```
### Download and install Miniconda

 - Linux installers
https://docs.conda.io/en/latest/miniconda.html#linux-installers

```bash
# download the installer
$ wget <the Ubuntu installer bash script URL>
# run the installer
$ bash <the downloaded installer script name>
```
Where did Ubuntu install it? `/home/ubuntu/miniconda3`
Do we want it to initialize Conda? `yes`

### Configure Conda env
- Enter the base conda env, or
```bash
$ bash
(base) ubuntu@ip-172-31-46-32:~$
```
- create a conda env
```bash
$ conda create --name d2l python=3.8 -y
# conda installs a bunch of stuff including Python 3.8, pip, etc.
# enter the env we just created
$ conda activate d2l
```

### Install packages for the course

```bash
# Install Jupyter notebook, d2l (the course), torch (PyTorch), torchvision (PyTorch library for CV)
$ pip install jupyter d2l torch torchvision
```

### Get the notebooks

```bash
# download the notebook zip
$ mkdir d2l-zh && cd d2l-zh
$ curl https://zh-v2.d2l.ai/d2l-zh-2.0.0.zip -o d2l-zh.zip
# download unzip
$ sudo apt install unzip
$ unzip d2l-zh.zip && rm d2l-zh.zip
```

Start jupyter notebook
```bash
$ jupyter notebook
```

To open the notebook in local computer's browser:
- Map remote 8888 port to local (open another shell)
```bash
$ ssh -i <ssh key> -L8888:localhost:8888 ubuntu@54.249.149.5
```
- Then you can open the notebook link in local browser
```
http://localhost:8888/?token=e6fbc787804e7b5d9ecd882211d23e7d8c94eb3136e21bc8
```

## Alternative: Run and connect to a local Jupyter server
1. Install Jupyter
```bash
$ pip3 install jupyter
```
2. Start the server
```bash
$ jupyter notebook
```
The server connection URI will be shown in the terminal in the format like the following
```
http://localhost:8889/?token=3537328d33241057ed984417716c9c19a1d0a12caf516536
```
3. Connect the server in VSCode
   1. Select kernel
   2. `shift+cmd+p` to open VS code's command pallete
   3. select "Jupyter: Specify Jupyter Server for Connections"
   4. copy and paste the server connection URI, hit Enter