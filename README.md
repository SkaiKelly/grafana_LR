# Semenova

Перед началой установки, нужно установить Linux Oracle на VirtualBox, для этого нужно:

Иметь образ Linux
Выделить 2+ ядер.
Выделать 4096+ МБ оперативы.
При установки операционной системы, нужно будет выбрать английский язык.

Далее переходим к установке Grafana Stack с использованием Docker, вводим следующий набор команд:

1. sudo yum install wget

• устанавливает утилиту wget на вашу систему
![image](https://github.com/user-attachments/assets/b2650d1d-f531-4e25-9842-012e9076cc60)

3. sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo

• Скачиваем файл репозитория
![image](https://github.com/user-attachments/assets/8974b604-8238-4c21-aa7e-33faa8bc1952)

3. sudo yum install docker-ce docker-ce-cli containerd.io

• Устанавливаем docker
![image](https://github.com/user-attachments/assets/ffdd913c-33d2-4489-a59c-581928dbc968)

4. sudo systemctl enable docker --now

• Запускаем его и разрешаем автозапуск

5. sudo yum install curl

• Для этого сначала убедимся в наличие пакета curl

6. COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)

• Использование команды curl для получения последней версии Docker Compose
![image](https://github.com/user-attachments/assets/1a319c45-0467-4354-80ae-8adb82d8ad57)

7. sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose

• Tеперь скачиваем скрипт docker-compose и помещаем его в каталог /usr/bin
![image](https://github.com/user-attachments/assets/6f4a7ffc-ff0c-4155-a082-07d7d0efc5e5)

8. sudo chmod +x /usr/bin/docker-compose

• Предоставление прав на выполнение файла docker-compose.

9. docker-compose --version

• Проверка установленной версии Docker Compose.
![image](https://github.com/user-attachments/assets/5a7024a8-b070-489c-a21b-1799118f110a)

•Можно скачать git прямо из командной строки прописав Y

10. git clone https://github.com/skl256/grafana_stack_for_docker.git

• выдаст ошибку и предложит скачать git, согласиться и продолжить
![image](https://github.com/user-attachments/assets/b469b556-d8b7-467c-a1d9-125487dcafd8)

11. cd grafana_stack_for_docker
    
• переход в папку

12. sudo mkdir -p /mnt/common_volume/swarm/grafana/config

• команда создаёт полный путь /mnt/common_volume/swarm/grafana/config, включая все необходимые промежуточные каталоги, если они ещё не существуют.

13. sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data,loki-data,promtail-data}

• команда создаёт структуру каталогов для Grafana и связанных с ней компонентов, если они ещё не существуют.

14. sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}

• все файлы и каталоги в указанных директориях будут переданы в собственность текущему пользователю и его группе

15. touch /mnt/common_volume/grafana/grafana-config/grafana.ini

• файл grafana.ini уже существует, команда обновит его временные метки (время последнего доступа и изменения). Если файл не существует, команда создаст новый пустой файл с указанным именем по указанному пути.

16. cp config/* /mnt/common_volume/swarm/grafana/config/

• команда копирует все файлы и подкаталоги из директории config в директорию /mnt/common_volume/swarm/grafana/config/

17. mv grafana.yaml docker-compose.yaml 

• команда переименовывает файл grafana.yaml в docker-compose.yaml. Ничего не покажет, но можно проверить при помощи команды ls

18. sudo docker compose up -d

• команда создает и запускает контейнеры в фоновом режиме, используя конфигурацию из файла docker-compose.yml, с правами суперпользователя.
![image](https://github.com/user-attachments/assets/a58b0533-185d-49d2-b5ae-f48ce5ec261f)

![image](https://github.com/user-attachments/assets/929f2f13-f8e2-4a24-8bef-a423f785b144)

19. sudo vi docker-compose.yaml

•команда открывает файл docker-compose.yaml в текстовом редакторе vi с правами суперпользователя, что позволяет вам редактировать его содержимое.

• Нас перекинет в текстовый редактор

• Что-бы что-то изменить в тесковом редакторе нажмите insert на клавиатуре

• Что бы сохранить что-то в этом документе нажимаем Esc пишем :wq! В этом текставом редакторе мы должны поставить node-exporter после services
![image](https://github.com/user-attachments/assets/3b7cdd9c-0a33-4d84-ae8d-d56f99fa35ac)
![image](https://github.com/user-attachments/assets/c2c56867-dfd8-4cd8-aeec-fc2332f54861)

20. sudo vi prometheus.yaml 

• команда открывает файл prometheus.yaml в текстовом редакторе vi с правами суперпользователя.

• /mnt/common_volume/swarm/grafana/config/prometheus.yaml - исправить targets: на exporter:9100,
![image](https://github.com/user-attachments/assets/92943bf8-6331-4269-a1d2-f3dc44080577)
![image](https://github.com/user-attachments/assets/61c52dfe-6091-40d1-a314-80d7bca39245)













![1](https://github.com/user-attachments/assets/d47785a9-3f36-4d62-9012-bc075d5654ce)
