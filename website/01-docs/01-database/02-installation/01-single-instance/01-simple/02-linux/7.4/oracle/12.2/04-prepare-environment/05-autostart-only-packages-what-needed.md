---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Автозапуск только выбранных программ
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/autostart-only-packages-what-needed/
---


<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Автозапуск только выбранных программ


<br/>

Следующая команда отключает автозапуск сразу всех пакетов.


	# for i in $(chkconfig --list | grep '3:on\|4:on\|5:on' | awk {'print $1'}); do chkconfig --level 345 $i off; done


Посмотреть какие программы сейчас автостартуют при запуске операционной системы.

	# chkconfig --list | grep '3:on\|4:on\|5:on'  |awk '{print $1}' | sort

После этого, включаем в автозапуск следующие программы:

	# {
	chkconfig --level 345 network on
	chkconfig --level 345 sshd on
	chkconfig --level 345 ntpd on
	}

<br/>

	# {
	chkconfig --level 345 auditd on
	chkconfig --level 345 netfs on
	chkconfig --level 345 sysstat on
	chkconfig --level 345 crond on
	chkconfig --level 345 xinetd on
	}


Позднее будет также добавлен:

	# chkconfig --level 345 startupOracleDatabase12R1 on

Обязательно убедиться, что ssh будет запущен при автозапуске!

	# chkconfig --list | grep ssh

Далее, (впрочем, можно и непосредственно перед стартом инсталляции ребутнуть) следует перезагрузить сервер, чтобы просто убедиться, что все нормально поднимается после перезагрузки.

	# reboot
