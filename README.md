# Исходные коды сайта <a href="https://oracle-dba.ru">oracle-dba.ru</a>

Запустить sysadm.ru на своем хосте с использованием docker контейнера:

    $ docker run -i -t -p 80:80 --name oracle-dba.ru marley/oracle-dba.ru

<br/>

### Как сервис

    # vi /etc/systemd/system/oracle-dba.ru.service

вставить содержимое файла oracle-dba.ru.service
    
    # systemctl enable oracle-dba.ru.service
    # systemctl start  oracle-dba.ru.service
    # systemctl status oracle-dba.ru.service


http://localhost:4009