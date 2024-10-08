##Create a virtual machine with Ubuntu Server 22.04. 
Deploy the latest WordPress on this virtual machine (without containerization). 
Write a script to back up the MySQL/MariaDB database and schedule it to run every weekday at 3 AM UTC. 
The backup name should include the date of its creation - backup_01.12.2023_12.53.sql. 
 Store the backup in the /opt/backups_wordpress directory.


##Устанавливаем VirtualBox
https://i.imgur.com/UtbbUB2.png

##Скачиваем на официальном сайте образ и устанавливаем через VirtualBox.
Устанавливаем и заходим в систему.
https://i.imgur.com/YxKffWT.png

##Обновляем пакеты
```bash
sudo apt update && sudo apt upgrade -y
```
https://i.imgur.com/BlfnGLw.png

##Далее устанавливаем Apache это веб-сервер, который будет хостить WordPress.
```bash
sudo apt install apache2 -y
```

##Запускаем и настраиваем автозапуск
```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```
##Далее необходимо установить MySQL
```bash
sudo apt install mysql-server -y
```
https://i.imgur.com/kDzAC5C.png

##Проверяем статус
https://i.imgur.com/lzO7QPW.png

##Далее проводим базовую настройку безопасности MySQL
```bash
sudo mysql_secure_installation
```
##Проверяем
https://i.imgur.com/j6YnvJD.png

##Далее нам нужно установить PHP и необходимые модули для работы с MySQL
sudo apt install php libapache2-mod-php php-mysql -y

##После установки Apache - перезапускаем, чтобы изменения вступили в силу
https://i.imgur.com/MNUyF4a.png

##Нам необходимо установить и настроить WordPress
https://i.imgur.com/5s3iVFt.png

##Далее разархевируем
https://i.imgur.com/vxrF21u.png

##Перемещаем файлы и удаляем архив
```bash
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
```

##Настраиваем права доступа
https://i.imgur.com/dq7vhAT.png

##Создаем базу данных и пользователя
https://i.imgur.com/kvA0WAR.png

##Далее для wordpress копируем пример конфигурации
```bash
sudo cp wp-config-sample.php wp-config.php
```
##И вносим изменения с данными, которые мы использовали при создании БД
https://i.imgur.com/NJaI4CR.png

##Все сохраняем, выключаем машину, настраиваем в сети мост и проверяем по ip работает наш apache2 или нет.
https://i.imgur.com/7H7sGdu.png

##Далее нам необходимо настроить скрипт для резервного копирования
Начнем с создания директории для резервных копий
sudo mkdir -p /opt/backups_wordpress

##Создаем скрипт для резервного копирования
sudo nano /opt/backup_wp_db.sh
https://i.imgur.com/SKN2STw.png

##Далее делаем файл исполняемым
sudo chmod +x /opt/backup_wp_db.sh

##И проверяем его в ручную
https://i.imgur.com/N1ctfmP.png

##Уведомляет о "небезопасной" передаче пароля, но можно оставить так

##Теперь нам осталось выполнить автоматизацию бекапа, для этого будем писать "задание"
Будем использовать crontab
https://i.imgur.com/WkuMy0z.png

