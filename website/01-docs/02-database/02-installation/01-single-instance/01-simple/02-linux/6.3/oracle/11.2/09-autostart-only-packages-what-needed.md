---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/12.1/autostart-only-packages-what-needed/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/12.1/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Автозапуск только выбранных программ


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
	chkconfig --level 345 messagebus on
	chkconfig --level 345 netfs on
	chkconfig --level 345 sysstat on
	chkconfig --level 345 crond on
	chkconfig --level 345 xinetd on
	}

Позднее будет также добавлен:

	# chkconfig --level 345 startupOracleDatabase12GR2 on


Обязательно убедиться, что ssh будет запущен при автозапуске!.

	# chkconfig --list | grep ssh

Далее, следует перезагрузить сервер, чтобы просто убедиться, что все нормально поднимается после перезагрузки.

	# reboot
