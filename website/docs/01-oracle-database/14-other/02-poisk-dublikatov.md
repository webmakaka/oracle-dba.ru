---
layout: page
title: Поиск одинаковых записей в базе данных (поиск дубликатов)
permalink: /docs/architecture/other/poisk-dublikatov/
---


<h3>Поиск одинаковых записей в базе данных (поиск дубликатов)</h3><br/>

    select do, count(*)
    from region
    group by do
    having count(*) > 1;
