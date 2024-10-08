
Устанавливаем VirtualBox
```https://i.imgur.com/UtbbUB2.png
```
Скачиваем на официальном сайте образ и устанавливаем через VirtualBox.
Устанавливаем и заходим в систему.
https://i.imgur.com/YxKffWT.png

Обновляем пакеты
```sudo apt update && sudo apt upgrade -y```
https://i.imgur.com/BlfnGLw.png

Далее устанавливаем Apache это веб-сервер, который будет хостить WordPress.
```sudo apt install apache2 -y```

Запускаем и настраиваем автозапуск
```
sudo systemctl start apache2
sudo systemctl enable apache2
```
Далее необходимо установить MySQL
```
sudo apt install mysql-server -y
```
https://i.imgur.com/kDzAC5C.png

Проверяем статус
https://i.imgur.com/lzO7QPW.png

Далее проводим базовую настройку безопасности MySQL
```
sudo mysql_secure_installation
```
Проверяем
https://i.imgur.com/j6YnvJD.png

Далее нам нужно установить PHP и необходимые модули для работы с MySQL
sudo apt install php libapache2-mod-php php-mysql -y

После установки Apache - перезапускаем, чтобы изменения вступили в силу
https://i.imgur.com/MNUyF4a.png

Нам необходимо установить и настроить WordPress
https://i.imgur.com/5s3iVFt.png

Далее разархевируем
https://i.imgur.com/vxrF21u.png

Перемещаем файлы и удаляем архив
```
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
```

Настраиваем права доступа
https://i.imgur.com/dq7vhAT.png

Создаем базу данных и пользователя
https://i.imgur.com/kvA0WAR.png

Далее для wordpress копируем пример конфигурации
```
sudo cp wp-config-sample.php wp-config.php
```
И вносим изменения с данными, которые мы использовали при создании БД
https://i.imgur.com/NJaI4CR.png
