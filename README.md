# Исходные коды сайта <a href="http://oracle-dba.ru">oracle-dba.ru</a>

[![Join the chat at https://gitter.im/oracle-dba-ru/Lobby](https://badges.gitter.im/oracle-dba-ru/Lobby.svg)](https://gitter.im/oracle-dba-ru/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Как скопировать и запустить oracle-dba.ru на свой хост с использованием docker контейнера:

Инсталлируете docker, далее:

    $ docker pull marley/centos6-for-dev
    $ docker run -i -t –rm -p 80:8080 –-name oradev marley/centos6-for-dev /bin/bash

<br/>

    $ source ~/.bash_profile
    $ cd /projects
    $ git clone --depth=1 https://github.com/plsql/oracle-dba.ru
    $ cd oracle-dba.ru
    $ gem install jekyll
    $ jekyll serve --watch --host 0.0.0.0 --port 8080


<br/>

Остается в браузере подключиться к localhost
