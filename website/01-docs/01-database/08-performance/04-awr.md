---
layout: page
title: Подготовка отчета Automatic Workload Repository (AWR) - Windows - Oracle 10.2
description: Подготовка отчета Automatic Workload Repository (AWR) - Windows - Oracle 10.2
keywords: Oracle Database, Подготовка отчета Automatic Workload Repository (AWR) - Windows - Oracle 10.2
permalink: /database/performance/awr/
---

# Подготовка отчета Automatic Workload Repository (AWR) - Windows - Oracle 10.2

<br/>

Делалось в 2010

<br/>

**1. Копируем файлы**

<br/>

```
awrrpt.sql
awrrpti.sql
awrinput.sql
awrinpnm.sql
```

<br/>

из каталога на сервере C:\oracle\product\10.2.0\db_1\RDBMS\ADMIN на локальный диск клиента (Например в каталог C:\AWR)

<br/>

**2. Создаем файл с именем connections.sql**

<br/>

```sql
conn system/master@<"ip adress">:1521/<"service name">;

@awrrpt.sql
```

<br/>

**3. Создаем файл с именем Run.bat**

<br/>

```sql
chcp 1251

sqlplus /nolog @connections.sql
exit;
```

<br/>

**Результат:**

<br/>

![Oracle DBA](/img/database/performance/awr/awr01.png 'Oracle Подготовка отчета AWR'){: .center-image }

<br/>

**4. запускаем run.bat. Программа спрашивает в каком формате лучше представит информацию.**

![Oracle DBA](/img/database/performance/awr/awr02.png 'Oracle Подготовка отчета AWR'){: .center-image }

<br/>

**5. За какой период интересуют сведения**

![Oracle DBA](/img/database/performance/awr/awr03.png 'Oracle Подготовка отчета AWR'){: .center-image }

<br/>

**6. Начальный и конечный снапшот за данный период**

![Oracle DBA](/img/database/performance/awr/awr04.png 'Oracle Подготовка отчета AWR'){: .center-image }

![Oracle DBA](/img/database/performance/awr/awr05.png 'Oracle Подготовка отчета AWR'){: .center-image }

<br/>

**7. Имя для создаваемого файла отчета. В данном случае report**

![Oracle DBA](/img/database/performance/awr/awr06.png 'Oracle Подготовка отчета AWR'){: .center-image }

<br/>

**8. Сгенерирован файл report.LST. Переименуем его в report.html и запустим**

![Oracle DBA](/img/database/performance/awr/awr07.png 'Oracle Подготовка отчета AWR'){: .center-image }

<br/>

**9. Отчет подготовлен**

![Oracle DBA](/img/database/performance/awr/awr08.png 'Oracle Подготовка отчета AWR'){: .center-image }
