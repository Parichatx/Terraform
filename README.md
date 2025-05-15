# Jenkins Master-Slave Setup

การตั้งค่า Jenkins ให้เชื่อมต่อกับ Slave Node (Ubuntu) ผ่าน SSH โดย Master รันใน Docker Container

---

## 🖥️ Ubuntu Slave Setup

รันคำสั่งต่อไปนี้บนเครื่อง **Slave (Ubuntu)**:

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
