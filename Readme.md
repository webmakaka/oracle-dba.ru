# Исходные коды сайта <a href="https://oracle-dba.ru">oracle-dba.ru</a>

<br/>

### Запустить oracle-dba.ru на своем хосте с использованием docker контейнера (на примере ubuntu like дистрибутивов):

Инсталлируете <a href="//sysadm.ru/devops/containers/docker/setup/ubuntu/">docker</a> и docker-compose.

<br/>

### Вариант для внесения изменений

Docker и docker-compose должны быть уже установлены.

Далее:

    $ cd ~
    $ mkdir oracle-dba.ru && cd oracle-dba.ru
    $ git clone --depth=1 https://bitbucket.org/oracle-dba/oracle-dba.ru.git .
    $ docker-compose up

<br/>

Остается в браузере подключиться к localhost:80

В качестве редактора отличное бесплатное решение Visual Studio Code.

В нем можно набирать текст и сразу видеть результат в доп окне. Можно также видеть результат в браузере с небольшими задержками.

<br/>

### Как сервис

    # vi /etc/systemd/system/oracle-dba.ru.service

вставить содержимое файла oracle-dba.ru.service

    # systemctl enable oracle-dba.ru.service
    # systemctl start  oracle-dba.ru.service
    # systemctl status oracle-dba.ru.service

http://localhost:4009
