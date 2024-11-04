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

    Этап Grafana✨

переходим на сайт localhost:3000

User & Password GRAFANA: admin

Код графаны: 3000
Код прометеуса: http://prometheus:9090
в меню выбираем вкладку Dashboards и создаем Dashboard

ждем кнопку +Add visualization, а после "Configure a new data source"
выбираем Prometheus
Connection

http://prometheus:9090
Authentication

Basic authentication
User: admin
Password: admin
Нажимаем на Save & test и должно показывать зелёную галочку
в меню выбираем вкладку Dashboards и создаем Dashboard

ждем кнопку "Import dashboard"
Find and import dashboards for common applications at grafana.com/dashboards: 1860 //ждем кнопку Load
Select Prometheus ждем кнопку "Import"
![image](https://github.com/user-attachments/assets/68774952-a375-4e77-8b1e-a61d1210d443)

    VicroriaMetrics🎂

Для начала изменим docker-compose.yaml

1. cd grafana_stack_for_docker

• команда cd grafana_stack_for_docker изменяет текущий рабочий каталог на каталог grafana_stack_for_docker.

2. sudo vi docker-compose.yaml

• команда sudo открывает файл docker-compose.yaml в редакторе vi с правами суперпользователя.
![image](https://github.com/user-attachments/assets/1a957374-26c9-4b6f-96c1-0741d8d1b745)

В самом текстовом редакторе после prometheus вставляем
![image](https://github.com/user-attachments/assets/b25ebd84-0173-4e2c-9fe5-c94b7c290a37)
Захом в connection
там где мы писали http:prometheus:9090 пишем http:victoriametrics:9090 И заменяем имя из "Prometheus-2" в "Vika"
нажимаем на dashboards add visualition выбираем "Vika"
снизу меняем на "cod"
Переходим в терминал и пишем

3. curl -G 'http://localhost:8428/api/v1/query'

• команда делает запрос к API для получения данных по метрике OILCOINT_metric1

4. --data-urlencode 'query=OILCOINT_metric1'

• команда выводит информацию о типе и значении этой метрики в формате, который может быть использован системой мониторинга Prometheus.

5. echo -e "# TYPE OILCOINT_metric1 gauge\nOILCOINT_metric1 0"

• команда выводит текст, который может быть использован для определения метрики в формате, совместимом с Prometheus

6. curl --data-binary @- http://localhost:8428/api/v1/import/prometheus

команда отправляет бинарные данные (например, метрики в формате Prometheus) на локальный сервер, который слушает на порту 8428.
![image](https://github.com/user-attachments/assets/45c35e91-2867-4a03-8d27-262c3a7ac9da)

Значение 0 меняем на любое другое

Копируем переменную OILCOINT_metric1 и вставляем в cod

Нажимаем run

![image](https://github.com/user-attachments/assets/e6d1a7a9-3bc7-43da-a19c-c3304a535cb6)
![image](https://github.com/user-attachments/assets/b1fc3cd1-9abf-451d-9779-60872a566a98)
![image](https://github.com/user-attachments/assets/739a9d3f-163b-40df-bc74-f5b76613a5f5)











