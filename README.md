Jenkins Master-Slave Setup
🖥️ Ubuntu Slave Setup
Run the following commands on the slave node (Ubuntu):

sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
Jenkins Master Configuration (Inside Docker)
docker exec -it jenkins-master bash
Inside the container
mkdir -p /var/jenkins_home/.ssh
chmod 700 /var/jenkins_home/.ssh
ssh-keyscan -H 192.168.64.2 >> /var/jenkins_home/.ssh/known_hosts
chmod 644 /var/jenkins_home/.ssh/known_hosts
