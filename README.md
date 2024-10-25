''' Переходим в папку проекта '''
cd laravel-compose-docker/
''' Скачать пакет composer docker если нету - apt install -y curl '''
sudo curl -L "https://github.com/docker/compose/releases/download/v2.11.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
''' Даем права на исполнение в любой другой папке хоста ubuntu 22.04'''
chmod +x /usr/local/bin/docker-compose
''' Проверяем версию'''
docker-compose -v
''' Изменяем правило firewall для порта на котором будет laravel отображаться на хост с контейнера'''
ufw allow 8088
''' Создаем проект laravel для этого на хост должен быть composer, php. Если нет ,то - apt install -y composer && apt install -y php '''

docker-compose run composer create-project laravel/laravel .
''' Даем разрешение на папки'''
chmod -R 777 /root/
chmod -R 777 /var/
''' Запускаем остальные контейнеры '''
docker-compose up -d

''' Проверяем контейнер с port-forwarding on host пиз файла docker-compose.yml  '''
curl http://127.0.0.1:8088
![Screnshot](https://github.com/antonffeksdnu/laravel-compose-docker/blob/main/2024-10-25%20105748.png)
