# Semenova


sudo yum install wget
![image](https://github.com/user-attachments/assets/b2650d1d-f531-4e25-9842-012e9076cc60)

sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo
![image](https://github.com/user-attachments/assets/8974b604-8238-4c21-aa7e-33faa8bc1952)

sudo yum install docker-ce docker-ce-cli containerd.io
![image](https://github.com/user-attachments/assets/ffdd913c-33d2-4489-a59c-581928dbc968)

sudo systemctl enable docker --now
sudo yum install curl
COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)
![image](https://github.com/user-attachments/assets/1a319c45-0467-4354-80ae-8adb82d8ad57)




![1](https://github.com/user-attachments/assets/d47785a9-3f36-4d62-9012-bc075d5654ce)
