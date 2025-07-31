
# 🐳 Install Docker on Ubuntu

Follow these steps to install Docker on a fresh Ubuntu system (works for Ubuntu 20.04, 22.04, etc.).

---

## ✅ Step 1: Update Existing Packages

```bash
sudo apt update && sudo apt upgrade -y
```
---

## ✅ Step 2: Install Prerequisite Packages

```bash
sudo apt install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y
```

---

## ✅ Step 3: Add Docker’s Official GPG Key

```bash
sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

---

## ✅ Step 4: Set Up the Docker Repository

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## ✅ Step 5: Install Docker Engine

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

---

## ✅ Step 6: Enable and Start Docker

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

---

## ✅ Step 7: Verify Docker Installation

```bash
sudo docker run hello-world
```

---

## ✅ (Optional) Run Docker Without `sudo`

```bash
sudo usermod -aG docker $USER
newgrp docker
```

Then try:

```bash
docker ps
```

---

> ⚠️ **Note:** You may need to log out and log back in after adding yourself to the `docker` group.
