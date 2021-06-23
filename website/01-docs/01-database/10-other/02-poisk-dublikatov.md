---
layout: page
title: Поиск одинаковых записей в базе данных (поиск дубликатов)
description: Поиск одинаковых записей в базе данных (поиск дубликатов)
keywords: Oracle Database, поиск дубликатов
permalink: /docs/architecture/other/poisk-dublikatov/
---

# Поиск одинаковых записей в базе данных (поиск дубликатов)

```sql
select do, count(*)
from region
group by do
having count(*) > 1;
```

<br/>

См. также [здесь](//plsql.ru/other/interview-questions/plsql/).
