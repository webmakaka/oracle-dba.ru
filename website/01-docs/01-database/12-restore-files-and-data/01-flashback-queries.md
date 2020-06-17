---
layout: page
title: FlashBack queries
description: FlashBack queries
keywords: Oracle Database, FlashBack queries
permalink: /docs/architecture/restore-files-and-data/flashback-queries/
---

# FlashBack queries

Если пользователь зафиксировал изменения, можно выполнить запрос прошлых данных (flashback queries) для выяснения значений, которые были до изменения (и затем изменить данные, восстановив их старые значения)

    SQL> SELECT salate FROM employees
    AS OF TIMESTAMP (SYSTIMESTAMP-INTERVAL'10' minute)
    WHERE employee_id=100;

Если кому-то из сотрудников недавно ошибочно был изменен оклад, можно вернуть старое значение, выполнив команду UPDATE с подзапросом, в котором возвращается хранившееся ранее значение оклада.

    SQL> UPDATE employees SET salary =
    (SELECT salary FROM employees
    AS OF TIMESTAMP TO_TEMESTAMP
    ('2005-05-04 11:00:00', 'yyyy-mm-dd hh24:mi:ss')
    WHERE employee_id = 200)
