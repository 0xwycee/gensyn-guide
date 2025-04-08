# Gensys-Testnet-Node-Guide

### The Gensyn Protocol is a layer-1 trustless protocol for deep learning computation that directly and immediately rewards supply-side participants for pledging their compute time to the network and performing ML tasks.
-------------------

![image](https://github.com/user-attachments/assets/779fe974-66bf-4b7b-8231-02a66c3dbd35)


# Where to get a node?
---
- Go to https://cloud.vast.ai/?ref_id=168603, make a profile and go to the "Templates" page, select Linux Desktop.
- Go to the "Search" page and filter on this from the top of the page: 1X GPU / On-Demand / RTX 4090 / Planet Earth / Price(inc.)
- Rent the cheapest VPS with a 1x RTX 4090 and a download/upload speed over 200mb/s
- Go to instances page and open your server
- From the service list chose: 6200 > KDE Plasma Desktop (VNC Fallback) > Direct Link

Now you should see your VPS screen![image](https://github.com/user-attachments/assets/c3d1528f-defc-4251-b4c0-6ce5b1903bb4)


---

## Setting up system 

Put all of these commands in your VPS terminal one by one
```
sudo apt update && sudo apt upgrade -y
```

## Essenstials 
```
sudo apt install -y \
  curl \
  git \
  wget \
  nano \
  tmux \
  htop \
  nvme-cli \
  lz4 \
  jq \
  make \
  gcc \
  clang \
  build-essential \
  autoconf \
  automake \
  pkg-config \
  libssl-dev \
  libleveldb-dev \
  libgbm1 \
  bsdmainutils \
  ncdu \
  unzip \
  tar

```

## Installing python 
```
sudo apt-get install -y \
  python3 \
  python3-pip \
  python3-venv \
  python3-dev
```

## Node and Yarn 
```
sudo apt-get update && curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash - && sudo apt-get install -y nodejs && node -v && sudo npm install -g yarn
```


## Install Docker 
```
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do
  sudo apt-get remove $pkg
done

sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

```





---
## Install Python & PIP 
```
sudo apt install python3 -y && sudo apt install python3-pip -y
```
![image](https://github.com/user-attachments/assets/9608067a-c0a1-4572-87cc-d606c239c72a)


## Install Dev. tool 
```
sudo apt install python3-dev python3-venv build-essential -y
```
![image](https://github.com/user-attachments/assets/5a138859-9483-4028-b676-c942a3b5c034)


## Install Yarn
```
sudo apt-get update && sudo apt-get install -y curl gnupg apt-transport-https && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && sudo apt-get update && sudo apt-get install -y yarn
```



# Clone RL-Swarm Repo 
### RL Swarm is an open source system for peer-to-peer reinforcement learning over the internet. Running a swarm node allows you to train your personal model against the swarm intelligence. 

```
git clone https://github.com/gensyn-ai/rl-swarm
```

### Navigate in 
```
cd rl-swarm
```

![image](https://github.com/user-attachments/assets/d033e5ce-ff44-49d8-97c6-c0268061aeb3)


### Install screen 
```
sudo apt install screen -y
```

### Create screen for process  
```
screen -S rlswarm
```
and navigate in rl-swarm again
```
cd rl-swarm
```

### Install and Run Swarm 
```
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

![2025-04-01_22h30_09](https://github.com/user-attachments/assets/a48558bd-9f88-4ac9-8c26-2b437ac2e5ac)


---

## Wait till you see ```waiting for UserData.json to be created```
![image](https://github.com/user-attachments/assets/0eb0a771-3afb-4640-a8a3-38aac53f0aeb)

Now open Browser and Input 
```http://localhost:3000/``` 

![2025-04-02_00h05_35](https://github.com/user-attachments/assets/fbe91e2a-9072-40ca-9794-77753969963c)

## If you get this error
![image](https://github.com/user-attachments/assets/22c95d21-1515-414e-8980-5d37c5bad728)
Go to your terminal and run
```cd /root/rl-swarm/modal-login/ && yarn upgrade &&  yarn add next@latest &&  yarn add viem@latest```
After that restart your VPS and try again


## Access ```.pem``` file and save ```swarm.pem``` to your local PC
### Desktop/workspace/rl-swarm/swarm.pem
![image](https://github.com/user-attachments/assets/4ef4e8be-3ee2-43dc-9d20-79a156d29e38)
#### (!!! THIS FILE IS YOUR ACTUAL NODE YOUR EMAIL WILL BE LINKED TO THIS .PEM FILE, YOU CAN ONLY USE 1 EMAIL PER NODE ID OR ELSE IT WONT GENERATE A CA FOR YOUR NODE ID CHECK NEXT STEP !!!)
#### (!!! IF YOU WANT TO TRANSFER TO ANOTHER VPS WITH THE SAME NODE ID, YOU NEED TO COPY THE .PEM FILE TO THERE AND LOGIN WITH SAME EMAIL AS U USED TO SIGN UP FOR THAT NODE ID !!!)

---


## Search your Node ID
### in @gensyntrackbot from Telegram to see if your Node ID is binded with a EVM CA, if not delete your userdata from rl-swarm/modal-login/temdata/ and delete both files in there -> rerun the swarm and login with different email.
![image](https://github.com/user-attachments/assets/7edd4203-c2b4-45ca-ae30-61720a1a1282)
### You can find your node name in your terminal, its a animal name with your node id behind it (starts with QM) after it starts training rounds (can take an hour or less)
![image](https://github.com/user-attachments/assets/0d2511a2-b69f-4680-b0bc-f0659e135a42)



# Official guide 
[Check Official guide](https://github.com/gensyn-ai/rl-swarm?tab=readme-ov-file)
Support me on X https://x.com/0xwycee
