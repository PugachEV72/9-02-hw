# Домашнее задание к занятию "`9.2 Zabbix. Часть 1`" - `Пугач Евгений`


---

### Задание 1

`Решение:`

1. `Установим PostgreSQL`
   `sudo apt install postgresql`
2. `Установим репозиторий Zabbix`
   `wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4%2Bdebian11_all.deb`
   `dpkg -i zabbix-release_6.0-4+debian11_all.deb`
   `apt update`
3. `Установим Zabbix Server, веб-интерфейс и агент`
   `apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent`
4. `Создадим пользователя БД`
   `sudo -u postgres createuser --pwprompt zabbix`
5. `Создадим БД`
   `sudo -u postgres createdb -O zabbix zabbix`
6. `Импортируем начальную схему и данные`
   `zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix`
7. `Настраиваем пароль DBPassword в файле /etc/zabbix/zabbix_server.conf`
   `sudo nano /etc/zabbix/zabbix_server.conf - в строке DBPassword=zabbix`
8. `Запускаем процессы Zabbix сервера и агента`
   `systemctl restart zabbix-server zabbix-agent apache2` 
   `systemctl enable zabbix-server zabbix-agent apache2`
9. `Настраиваем подключение web-интерфейса к PostgreSQL`
   `http://84.252.136.214/zabbix`

![Скрин 1](https://github.com/PugachEV72/Images/blob/master/2023-01-21_13-44-06.png)

![Скрин 2](https://github.com/PugachEV72/Images/blob/master/2023-01-21_13-45-04.png)


---

### Задание 2

`Решение:`

1. `Добавим репозиторий Zabbix`
   `wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4%2Bdebian11_all.deb`
   `dpkg -i zabbix-release_6.0-4+debian11_all.deb`
   `apt update`
2. `Установим Zabbix agent2`
   `apt install zabbix-agent2 zabbix-agent2-plugin-*`
3. `Запускаем процесс Zabbix agent2`
   `systemctl restart zabbix-agent2`
4. `Добавляем Zabbix agent2 в автозагрузку`
   `systemctl enable zabbix-agent2`
5. `Меняем настройки в файле zabbix_agentd.conf`
   `nano /etc/zabbix/zabbix_agentd.conf - в строке Server=84.252.136.214`
6. `Перезапускаем агента`
   `systemctl restart zabbix-agent`

`Повторяем алгоритм для каждого хоста`


![Скрин 3](https://github.com/PugachEV72/Images/blob/master/2023-01-21_17-39-37.png)

![Скрин 4](https://github.com/PugachEV72/Images/blob/master/2023-01-21_18-27-24.png)

![Скрин 5](https://github.com/PugachEV72/Images/blob/master/2023-01-21_18-31-57.png)

![Скрин 6](https://github.com/PugachEV72/Images/blob/master/2023-01-21_18-49-54.png)

![Скрин 7](https://github.com/PugachEV72/Images/blob/master/2023-01-21_18-50-48.png)

![Скрин 8](https://github.com/PugachEV72/Images/blob/master/2023-01-21_19-13-57.png)

![Скрин 9](https://github.com/PugachEV72/Images/blob/master/2023-01-21_19-14-44.png)


