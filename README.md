# Jenkins Master-Slave Setup

การตั้งค่า Jenkins ให้เชื่อมต่อกับ Slave Node (Ubuntu) ผ่าน SSH โดย Master รันใน Docker Container
---


# Jenkins Master Configuration (Inside Docker)

```bash
docker exec -it (jenkins-masterid) bash
Inside the container
mkdir -p /var/jenkins_home/.ssh
chmod 700 /var/jenkins_home/.ssh
ssh-keyscan -H 192.168.64.2(ip os ubuntu) >> /var/jenkins_home/.ssh/known_hosts
chmod 644 /var/jenkins_home/.ssh/known_hosts


---

## 🖥️ Ubuntu Slave Setup

รันคำสั่งต่อไปนี้บนเครื่อง **Slave (Ubuntu)**:

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh



