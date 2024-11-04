# Semenova

Перед началой установки, нужно установить Linux Oracle на VirtualBox, для этого нужно:

Иметь образ Linux
Выделить 2+ ядер.
Выделать 4096+ МБ оперативы.
При установки операционной системы, нужно будет выбрать английский язык.

Далее переходим к установке Grafana Stack с использованием Docker, вводим следующий набор команд:

sudo yum install wget 
эта комнда устанавливает утилиту wget на вашу систему
![image](https://github.com/user-attachments/assets/b2650d1d-f531-4e25-9842-012e9076cc60)

sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo
Скачиваем файл репозитория
![image](https://github.com/user-attachments/assets/8974b604-8238-4c21-aa7e-33faa8bc1952)

sudo yum install docker-ce docker-ce-cli containerd.io
![image](https://github.com/user-attachments/assets/ffdd913c-33d2-4489-a59c-581928dbc968)

sudo systemctl enable docker --now
sudo yum install curl
COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)
![image](https://github.com/user-attachments/assets/1a319c45-0467-4354-80ae-8adb82d8ad57)

sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose
![image](https://github.com/user-attachments/assets/6f4a7ffc-ff0c-4155-a082-07d7d0efc5e5)

![image](https://github.com/user-attachments/assets/5a7024a8-b070-489c-a21b-1799118f110a)

![image](https://github.com/user-attachments/assets/b469b556-d8b7-467c-a1d9-125487dcafd8)

![image](https://github.com/user-attachments/assets/a58b0533-185d-49d2-b5ae-f48ce5ec261f)

![image](https://github.com/user-attachments/assets/929f2f13-f8e2-4a24-8bef-a423f785b144)

![image](https://github.com/user-attachments/assets/3b7cdd9c-0a33-4d84-ae8d-d56f99fa35ac)

![image](https://github.com/user-attachments/assets/92943bf8-6331-4269-a1d2-f3dc44080577)
![image](https://github.com/user-attachments/assets/61c52dfe-6091-40d1-a314-80d7bca39245)













![1](https://github.com/user-attachments/assets/d47785a9-3f36-4d62-9012-bc075d5654ce)
