🛠️ การตั้งค่า Jenkins Master-Slave ด้วย Ubuntu Slave
เอกสารนี้อธิบายขั้นตอนการตั้งค่า Jenkins Master-Slave โดยใช้ Jenkins Master ภายใน Docker และ Ubuntu เป็น Slave Node

🔧 การติดตั้งและตั้งค่า Ubuntu Slave
รันคำสั่งต่อไปนี้บนเครื่อง Slave Node (Ubuntu):

bash
Copy
Edit
sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
📌 ตรวจสอบ ว่า SSH Server ทำงานเรียบร้อย:

bash
Copy
Edit
sudo systemctl status ssh
🐳 การตั้งค่า Jenkins Master (รันใน Docker)
1. เข้าไปใน Container ของ Jenkins Master
bash
Copy
Edit
docker exec -it jenkins-master bash
2. สร้างโฟลเดอร์และกำหนดสิทธิ์สำหรับ SSH
bash
Copy
Edit
mkdir -p /var/jenkins_home/.ssh
chmod 700 /var/jenkins_home/.ssh
3. เพิ่ม SSH Key ของ Slave Node ลงใน known_hosts
เปลี่ยน IP ให้ตรงกับ IP ของ Slave Node (ตัวอย่างนี้ใช้ 192.168.64.2):

bash
Copy
Edit
ssh-keyscan -H 192.168.64.2 >> /var/jenkins_home/.ssh/known_hosts
chmod 644 /var/jenkins_home/.ssh/known_hosts
✅ ขั้นตอนถัดไป
สร้าง SSH Key บน Jenkins Master แล้วนำ public key ไปใส่ใน ~/.ssh/authorized_keys บนเครื่อง Slave

ไปที่ Jenkins UI → Manage Jenkins → Manage Nodes and Clouds → New Node

กำหนดค่าการเชื่อมต่อแบบ SSH กับ Slave Node

📝 หมายเหตุ
ตรวจสอบว่า Jenkins Master และ Slave สามารถ ping หา IP กันได้

พอร์ต 22 บน Slave ต้องเปิดใช้งานสำหรับ SSH

ต้องใช้ Jenkins Plugin เช่น SSH Build Agents Plugin ในการเชื่อมต่อ Slave ผ่าน SSH
