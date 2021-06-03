---
layout: page
title: Создание табличных пространств
description: Создание табличных пространств
keywords: Oracle Database, Tablespaces
permalink: /docs/architecture/tablespaces/create-new-tablespace/
---

<hr>

Взято http://subscribe.ru/archive/comp.soft.db.oraclefromzero/200304/03160028.html<br/>
Несколько подредактировано.

# Обзор табличных пространств

<p>Табличное пространство Oracle является самым нижним логическим слоем структуры
  данных. Оно состоит из одного или более файлов данных. В ранних версиях СУРБД
  Oracle размер файлов данных был фиксированным, но теперь файлы могут быть увеличены
  как автоматически, так и вручную.</p>
<p>Значимость табличных пространств заключена в том, что они предоставляют великолепную
  степень детализации расположения информации в файлах данных. После создания
  табличного пространства, процесс расположения и распределения таблиц в нем уходит
  из-под Вашего контроля. При аккуратном конфигурировании табличного пространства,
  у Вас будет несколько обобщенных опций, но основная масса работы по внутреннему
  расположению объектов будет выполнена автоматически.</p>

<p>Табличные пространства могут содержать любые из четырех видов сегментов:</p>
<blockquote>
  <p>- <b>сегменты данных (Data segments)</b> - основной тип, используется для
    хранения таблиц и кластеров.<br>
    - <b>индексные сегменты (Index segments)</b> - используются для хранения индексов.<br>
    - <b>сегменты отката (Rollback segments)</b> - специальные сегменты, хранящие
    информацию для отмены выполненных действий.<br>
    - <b>временные сегменты (Temporary segments)</b> - используются для хранения
    временных данных.</p>
</blockquote>
<p>Табличные пространства по умолчанию являются доступными как для чтения, так
  и для записи, но могут быть изменены на состояние &quot;только для чтения&quot;.
  Во многих ситуациях табличные пространства только для чтения могут оказаться
  незаменимыми.</p>

  <h3>Создание табличных пространств</h3>

<p>Создание табличных пространств состоит из указания одного или более файлов
  данных, а также параметров хранения (storage parameters). Параметры хранения
  указывают то, как будут использоваться табличные пространства.</p>
<p>Как и большинство других операций, табличные пространства могут быть созданы
  либо с использованием Oracle Enterprise Manager (графически), либо с помощью
  команд консоли sqlplus.</p>

<h4>Создание табличного пространства командой CREATE TABLESPACE</h4>

<p>Вы можете создать табличное пространство в консоли sqlplus, используя команду
  CREATE TABLESPACE. Команда может быть введена интерактивно или выполнена из
  готового скрипт-файла. По-моему, предпочтительнее пользоваться SQL-скриптом,
  так как он может быть выполнен повторно. Кроме того, можно создать шаблон и
  по надобности вносить изменения. Сохраненный SQL-скрипт может оказаться весьма
  кстати после катастрофы. Итак, для создания табличного пространства
  применяется следующая команда:</p>
<h5><font color="#0000FF">CREATE TABLESPACE</font><br>
  <font color="#0000FF">DATAFILE</font><font color="#666666"> <font color="#000099">file_specification</font><br>
  [AUTOEXTEND OFF]<br>
  <font color="#000099">или</font> [AUTOEXTEND ON [NEXT <font color="#000099">число</font>
  K <font color="#000099">или</font> M] <br>
  [MAXSIZE UNLIMITED <font color="#000099">или</font> MAXSIZE <font color="#000099">число</font>
  K <font color="#000099">или</font> M]<br>
  [NOLOGGING <font color="#000099">или</font> LOGGING]<br>
  [,<font color="#000099"> file_specification</font><br>
  [AUTOEXTEND OFF]<br>
  <font color="#000099">или</font> [AUTOEXTEND ON [NEXT <font color="#000099">число</font>
  K <font color="#000099">или</font> M] <br>
  [MAXSIZE UNLIMITED <font color="#000099">или</font> MAXSIZE <font color="#000099">число</font>
  K <font color="#000099">или</font> M]<br>
  [NOLOGGING <font color="#000099">или</font> LOGGING]]<br>
  [MINIMUM EXTENT <font color="#000099">число</font> K <font color="#000099">или</font>
  M]<br>
  [DEFAULT STORAGE <font color="#000099">storage_clause</font>]<br>
  [ONLINE <font color="#000099">или</font> OFFLINE]<br>
  [PERMANENT <font color="#000099">или</font> TEMPORARY]</font></h5>
<p><b><font color="#0000FF">DATAFILE</font></b></p>
<blockquote>
  <p>- <b>DATAFILE file_specification</b> - определяет имена (или имя) файлов
    данных, составляющих табличное пространство. File_specification - это 'имя_файла'
    SIZE число (K или M) [REUSE]. Спецификация файла используется для указания
    имени и первоначального размера в (К)илобайтах или в (М)егабайтах файла данных.
    Параметр [REUSE] позволяет воспользоваться уже существующим в системе файлом.</p>
</blockquote>

<p>Уточнения параметра DATAFILE:</p>
<blockquote>
  <p>- <b>AUTOEXTEND OFF</b> - параметр указывает, что средство автоувеличения
    размера файла использоваться не будет.</p>
  <p>- <b>AUTOEXTEND ON</b> - автоувеличение размера файла будет использовано.
    Дополнительно можно указать:</p>
  <p> - <b>NEXT число K или M</b> - когда файл данных самоувеличивается, он изменяется
    на указанный объем.</p>
  <p> - <b>MAXSIZE UNLIMITED</b> - размер файла будет ограничен лишь физическим
    диском и особенностями операционной системы.</p>
  <p> - <b>MAXSIZE число K или M</b> - файл данных не может быть больше указанного
    объема.</p>
</blockquote>
<p>Вот остальные параметры команды CREATE TABLESPACE:</p>
<blockquote>
  <p>- <b>LOGGING</b> - указывает, что в журнал выполненных операций будет заноситься
    информация о таблицах, индексах и разделах. Параметр по умолчанию. Журналирование
    может быть отменено для этих операций опцией NOLOGGING.</p>
  <p>- <b>NOLOGGING</b> - журналирование не будет выполняться для операций, поддерживающих
    эту опцию.</p>
  <p>- <b>MINIMUM EXTENT число K или M</b> - указывает минимальный размер экстентов
    табличного пространства.</p>
  <p>- <b>DEFAULT STORAGE storage_clause</b> - указывает параметры по умолчанию
    хранения табличного пространства.</p>
  <p>- <b>ONLINE</b> - табличное пространство становится оперативным сразу после
    своего создания.</p>
  <p>- <b>OFFLINE</b> - табличное пространство недоступно непосредственно после
    своего создания (до тех пора, пока не будет переведено в оперативное состояние).</p>
  <p>- <b>TEMPORARY</b> - табличное пространство будет использовано для хранения
    временных объектов.</p>
  <p>- <b>PERMANENT </b>- указывает табличному пространству хранить перманентные
    объекты. (Опция по умолчанию).</p>
</blockquote>
<p>Как видите при создании табличного пространства можно указать много различных
  параметров и опций. Среди них есть параметры хранения, которые мы рассмотрим
  чуть ниже в этом же выпуске. Параметры хранения определяют характеристики табличного
  пространства и общие параметры его &quot;роста&quot;.</p>

<h3>Изменение табличных пространств</h3>

<p>Довольно часто приходится менять уже созданное табличное пространство. </p>

<h4><b>Изменение состояния табличного пространства на автономное</b></h4>

<p>Имеем несколько вариантов выполнения такой операции. Это: нормальный, временный
  и немедленный перевод состояния на автономный.</p>

<h4><b>Табличное пространство в нормальном автономном режиме</b></h4>

<p>Перевод состояния табличного пространства на автономное включает выполнение
  контрольной точки для всех файлов данных (принадлежащих данному табличному пространству),
  а затем, собственно, отключение доступа. Нормальный перевод в автономный режим
  требует присутствия и нормального функционирования всех включенных табличных
  пространств. Переход из нормального автономного состояния в оперативный может
  быть произведен без операции восстановления.</p>

<h4><b>Табличное пространство во временном автономном режиме</b></h4>

<p>Перевод табличного пространства в автономный режим с опцией Temporary (временно)
  возможен даже в том случае, если некоторые из файлов данных недоступны. Т.е.
  если у Вас есть какие-либо проблемы с файлом данных, Вы можете перевести табличное
  пространство в автономный режим с опцией &quot;временно&quot;. Для всех доступных
  файлов данных будет произведена контрольная точка. Однако перевод обратно в
  оперативный режим может потребовать восстановления.</p>

<h4><b>Немедленный перевод табличного пространства в автономный режим</b></h4>

<p>Опция Immediate (немедленно, сразу) перевода табличного пространства в автономный
  режим делает именно то, что требуется: сразу переводит табличное пространство
  в автономный режим. Но контрольная точка не будет произведена, поэтому возврат
  в оперативный режим потребует процедуру восстановления.</p>

<h4>Перевод табличного пространства в оперативный режим</h4>

<p>Любое табличное пространство, которое было переведено в автономный режим по
  каким-либо причинам может быть переведено обратно в оперативный режим через
  Enterprise Manager или через Server Manager (с использованием SQL-команды).
  Перевод табличного пространства в оперативный режим изменяет его состояние таким
  образом, что табличное пространство становится доступным для пользователей.
  Возможно, потребуется процедура восстановления, в зависимости от того, как табличное
  пространство было переведено в автономный режим.</p>

<h4>Дефрагментация табличного пространства</h4>

<p>Поскольку в табличном пространстве выделяется место для объектов схемы экстентами
  различных размеров, становится возможной такая ситуация, когда дисковое пространство
  фрагментируется. После назначения экстентов Oracle ищет свободный кусок памяти,
  близкий по размеру к требующемуся для нового экстента. Время от времени в табличном
  пространстве экстенты добавляются и освобождаются, поэтому можно обнаружить
  множество маленьких свободных экстентов сбитых в кучу (процесс напоминает фрагментацию
  файлов на жестком диске).</p>
<p>Дефрагментируя табличное пространство, Вы объединяете маленькие свободные экстенты
  в большие, тем самым, формируя больше места для назначения новых экстентов.<br>
  Фоновый серверный процесс SMON автоматически производит объединение
  мелких свободных экстентов, т.е. дефрагментацию. Естественно, дефрагментация
  происходит постоянно, за исключением тех моментов, когда процесс SMON отключен.
  Очень редко возникает необходимость произвести дефрагментацию вручную, однако
  надо знать, зачем и как это сделать.</p>

<h4>Добавление файлов данных</h4>

<p>Необходимость в новых файлах данных возникает достаточно часто. Новые файлы
  данных нужны либо для увеличения свободного пространства, либо для распределения
  нагрузки ввода-вывода между несколькими физическими дисковыми накопителями.
  Добавить файл в табличное пространство гораздо быстрее, чем сформировать его
  в процессе создания БД. Команда CREATE TABLESPACE работает последовательно,
  т.е. создает один файл данных за раз. Операция же добавления файлов данных может
  быть распараллелена (несколько файлов данных можно добавить за раз).</p>

  <h3>Изменение свойств табличного пространства</h3>

<p>Табличное пространство может быть изменено в Storage Manager и с помощью команды
  ALTER TABLESPACE (которую можно выполнить в Server Manager).</p>

<p>Вы можете воспользоваться следующими возможными опциями:</p>
<blockquote>
  <p>- <b>Online</b> - переводит табличное пространство в оперативный режим<br>
    - <b>Offline</b> - переводит табличное пространство в автономный режим<br>
    - <b>Read Only</b> - переводит табличное пространство в режим &quot;только
    для чтения&quot;<br>
    - <b>Permanent</b> - переводит временное табличное пространство в перманентное<br>
    - <b>Temporary</b> - переводит перманентное табличное пространство во временное</p>
</blockquote>

<h4>Изменение табличного пространства командой ALTER TABLESPACE</h4>

<p>Как видите, диалог редактирования табличного пространства Enterprise Manger
  имеет ограниченное число опций. При использовании команды ALTER TABLESPACE доступны
  абсолютно все возможности. Эта команда может быть использована для изменения
  параметров табличного пространства, указанных при его создании, для изменения
  состояния табличного пространства, или для добавления файлов данных.</p>

<h4>Синтаксис команды ALTER TABLESPACE</h4>

<h5><font color="#0000FF">ALTER TABLESPACE tablespace</font><br>
  <font color="#666666">[LOGGING <font color="#000099">или</font> NOLOGGING]<br>
  [ADD DATAFILE <font color="#000099">file_specification</font><br>
  [AUTOEXTEND OFF]<br>
  <font color="#000099">или</font> [AUTOEXTEND ON [NEXT <font color="#000099">число</font>
  K <font color="#000099">или</font> M] <br>
  [MAXSIZE UNLIMITED <font color="#000099">или</font> MAXSIZE <font color="#000099">число</font>
  K <font color="#000099">или</font> M]]<br>
  [, <font color="#000099">file_specification</font><br>
  [AUTOEXTEND OFF]<br>
  <font color="#000099">или</font> [AUTOEXTEND ON [NEXT <font color="#000099">число</font>
  K <font color="#000099">или</font> M] <br>
  [MAXSIZE UNLIMITED <font color="#000099">или</font> MAXSIZE <font color="#000099">число</font>
  K <font color="#000099">или</font> M]]<br>
  [RENAME DATAFILE '<font color="#000099">filename</font>' [, '<font color="#000099">filename</font>']...
  <br>
  TO '<font color="#000099">filename</font>' [, '<font color="#000099">filename</font>']...]<br>
  [COALESCE]<br>
  [DEFAULT STORAGE <font color="#000099">storage_clause</font>]<br>
  [MINIMUM EXTENT <font color="#000099">число</font> [K <font color="#000099">или</font>
  M]]<br>
  [ONLINE]<br>
  [OFFLINE NORMAL <font color="#000099">или</font> OFFLINE TEMPORARY <font color="#000099">или</font>
  OFFLINE IMMEDIATE]<br>
  [BEGIN BACKUP <font color="#000099">или</font> END BACKUP]<br>
  [READ ONLY <font color="#000099">или</font> READ WRITE]<br>
  [PERMANENT <font color="#000099">или</font> TEMPORARY]</font></h5>
<p>Многие из параметров этой команды нам уже знакомы. Например, LOGGING и NOLOGGING
  аналогичны соответствующим параметрам команды CREATE TABLESPACE. Также, думаю,
  не нуждаются в комментариях ключевые слова AUTOEXTEND, NEXT, MAXSIZE, MINIMUM
  EXTENT, PERMANENT и TEMPORARY.</p>
<blockquote>
  <p>- <b>ADD DATAFILE file_specification</b> - этим параметром указываются один
    или более файлов данных на добавление в табличное пространство. (Что такое
    file_specification, мы уже рассмотрели выше)</p>
  <p>- <b>RENAME DATAFILE 'filename' [, 'filename']... TO 'filename' [, 'filename']
    </b>- параметр команды используется для переименования одного или более файлов
    данных.</p>
  <p>- <b>COALESCE</b> - параметр используется для принудительного выполнения
    дефрагментации табличного пространства, как было описано ранее.</p>
  <p>- <b>DEFAULT STORAGE storage_clause </b>- указывает параметры по умолчанию
    хранения табличного пространства. Эти параметры используются в момент создания
    новых объектов схемы (если, конечно, они не указываются явно при создании
    конкретного объекта).</p>
  <p>- <b>ONLINE</b> - параметр используется для перевода табличного пространства
    в оперативный режим.</p>
  <p>- <b>OFFLINE NORMAL</b> - перевод табличного пространства в нормальный автономный
    режим.</p>
  <p>- <b>OFFLINE TEMPORARY</b> - перевод табличного пространства во временный
    автономный режим.</p>
  <p>- <b>OFFLINE IMMEDIATE</b> - немедленный перевод табличного пространства
    в автономный режим.</p>
  <p>-<b> BEGIN BACKUP</b> - Переводит табличное пространство в автономный режим
    и приостанавливает любые изменения файлов данных на момент создания резервной
    копии.</p>
  <p>- <b>END BACKUP</b> - Переводит табличное пространство обратно в оперативный
    режим и производит запись всех изменений файлов данных, имевших место в процессе
    создания резервной копии.</p>
  <p>- <b>READ ONLY</b> - Переводит табличное пространство в режим &quot;только
    для чтения&quot;.</p>
  <p>- <b>READ WRITE</b> - Переводит табличное пространство из режима &quot;только
    для чтения&quot; в обычный, позволяющий как чтение, так и запись файлов данных.</p>
</blockquote>
<p>Как видно, командой ALTER TABLESPACE табличное пространство можно изменить
  радикально. Поэтому полезно вести журнал изменений табличных пространств.</p>

<h4>Оператор STORAGE</h4>

<p>В командах CREATE TABLESPACE и ALTER TABLESPACE присутствует параметр &quot;DEFAULT
  STORAGE storage_clause&quot;. Здесь мы рассмотрим подробно параметры storage_clause.
  Это достаточно важные параметры, так как они определяют первоначальный размер
  и характеристики табличного пространства, а также дальнейший его рост.</p>

<p>Запомните, что оператор DEFAULT STORAGE используется для создания экстентов.
  А экстенты используются для хранения объектов схемы. Параметры хранения, указанные
  в DEFAULT STORAGE, применяются при создании и росте объектов схемы. К объектам
  схемы, которые создаются с указанием конкретных параметров хранения, параметры
  хранения по умолчанию не применяются.</p>

<p>Оператор STORAGE имеет следующий синтаксис:</p>
<h5><font color="#0000FF">STORAGE</font><br>
  <font color="#666666">(<br>
  [INITIAL <font color="#000099">число</font> K <font color="#000099">или</font>
  M]<br>
  [NEXT <font color="#000099">число</font> K <font color="#000099">или</font>
  M]<br>
  [MINEXTENTS <font color="#000099">число</font>]<br>
  [MAXEXTENTS <font color="#000099">число или</font> MAXEXTENTS UNLIMITED]<br>
  [PCTINCREASE <font color="#000099">число</font>]<br>
  [FREELISTS <font color="#000099">число</font>]<br>
  [FREELIST GROUPS <font color="#000099">число</font>]<br>
  [OPTIMAL [<font color="#000099">число</font> K <font color="#000099">или</font>
  M] <font color="#000099">или</font> [NULL]]<br>
  )</font></h5>
<p>Вот что означают отдельные части оператора:</p>
<blockquote>
  <p>-<b> INITIAL число K или M</b> - указывает первоначальный размер экстентов,
    которые создаются для новых объектов схемы. По умолчанию равен размеру 5-ти
    блоков данных. При указании конкретного размера (в килобайтах или мегабайтах),
    он округляется до кратности 5 блокам данных.</p>
  <p>- <b>NEXT число K или M</b> - указывает размер последующих экстентов. Также
    округляется до кратности 5 блокам данных.</p>
  <p>- <b>MINEXTENTS число</b> - указывает минимальное число экстентов, выделяемых
    для объекта схемы в момент его создания. Каждый из этих экстентов по размеру
    равен числу INITIAL, а для последующих размер рассчитывается на основе параметров
    NEXT и PCTINCREASE. По умолчанию MINEXTENTS = 1, за исключением сегментов
    отката (по умолчанию для них MINEXTENTS = 2).</p>
  <p>- <b>MAXEXTENTS число</b> - максимально число экстентов (включая первый)
    для объектов схемы.</p>
  <p>-<b> MAXEXTENTS UNLIMITED</b> - максимальное количество экстентов не ограничено.
    Не рекомендуется использовать этот параметр для любых объектов (кроме сегментов
    отката).</p>
  <p>- <b>PCTINCREASE число</b> - определяет размер экстентов после второго (т.е.
    начиная с третьего экстента). Размер первоначального экстента равен INITIAL.
    Размер второго экстента равен NEXT. Если PCTINCREASE не равен нулю, то все
    последующие экстенты будут определяться как предыдущий размер экстента, увеличенный
    на процент PCTINCREASE. Если PCTINCREASE равен нулю, то все последующие экстенты
    по размеру будут равны числу NEXT. По умолчанию PCTINCREASE = 50 (для сегментов
    отката по умолчанию он равен нулю).</p>
  <p>- <b>FREELISTS число</b> - указывает число списков свободной памяти для каждой
    группы списков. Список свободной памяти - это связный список доступных блоков
    данных в экстенте, имеющем свободного пространства более чем PCTFREE. В сущности,
    это список блоков, готовых принять информацию. При использовании более одного
    списка, Вы снижаете конфликты вноса информации.</p>
  <p>- <b>FREELIST GROUPS число</b> - указывает число групп списков свободной
    памяти в среде параллельного сервера. Использование нескольких групп позволяет
    каждому экземпляру иметь свой собственный набор списков свободной памяти.
    Параметр используется только в среде параллельного сервера.</p>
  <p>- <b>OPTIMAL число K или M</b> - параметр применим только к сегментам отката.
    Он указывает идеальный размер сегмента. Как мы увидим в одном из следующих
    выпусков, сегмент отката постоянно растет в размерах. А этот параметр указывает
    тот размер, который Oracle должен пытаться сохранить.</p>
  <p>- <b>OPTIMAL NULL</b> - этот параметр указывает сегменту отката никогда не
    пытаться уменьшить свой размер (и приблизить его к желаемому, как в предыдущем
    параметре).</p>
</blockquote>
<p>Параметры хранения могут быть применены не только в процессе создания табличного
  пространства, но и во время создания различных объектов схемы. Размер и характеристики
  табличного пространства оказывают значительное влияние на производительность
  системы.</p>
<p>Примечание: для табличных пространств Вы указывает опции DEFAULT STORAGE (т.е.
  по умолчанию). Эти опции будут применятся при создании объектов схемы, если
  Вы их не перекроете новыми конкретными значениями.</p>

<h3>Табличные пространства &quot;только для чтения&quot;</h3>

<p>Как уже было сказано ранее, есть возможность перевести табличное пространство
  в режим &quot;только для чтения&quot;. Табличное пространство &quot;только для
  чтения&quot; отличается от обычного лишь тем, что не сохраняются изменения объектов
  схемы. В этом случае отпадает необходимость в резервном копировании такого табличного
  пространства.</p>
<p>Так как табличные пространства &quot;только для чтения&quot; не изменяются
  Oracle-сервером, то есть возможность поместить их, например, на компакт-диск.
  Если данные являются архивными по своей природе, но в них периодически возникает
  необходимость, то использование CD-ROM может оказаться идеальным решением.</p>

<h4>Создание табличных пространств &quot;только для чтения&quot;</h4>

<p>Любое табличное пространство первоначально должно быть создано в режиме &quot;чтение-запись&quot;
  и заполнено необходимыми данными. После добавления данных и создания индексов,
  соответствующих Вашим спецификациям, табличное пространство может быть переведено
  в режим &quot;только для чтения&quot;. Это может быть достигнуто несколькими
  способами.</p>
<p>Для Enterprise Manager-а или Storage Manager-а просто откройте форму редактирования
  табличного пространства и поставьте флажок напротив надписи Read Only.</p>
<p>Если Вы нажмете после этого кнопку SHOW SQL, то получите возможность лицезреть
  DDL-команду этой операции. Рекомендую пользоваться этой кнопкой при каждом удобном
  случае, так Вы поймете сущность выполняемых операций.</p>
<p>Также можно воспользоваться командой ALTER TABLESPACE вот так:</p>
<h5>ALTER TABLESPACE CARS READONLY;</h5>
<p>Существует множество причин использования табличных пространств &quot;только
  для чтения&quot;, но они очень специфичны. Нужны они или нет - решать Вам.</p>

<h3>Временные табличные пространства (Temporary Tablespaces)</h3>

<p>Временные табличные пространства используются для выполнения таких операций
  сортировки, которые не вмещаются в оперативную память. Если Вы выделите табличное
  пространство специально для сортировок, то отпадет необходимость выделения памяти
  в других табличных пространствах (что приводит к фрагментации).</p>
<p>Когда операция сортировки не умещается в памяти, она должна создать и воспользоваться
  временным сегментом. В этом временном сегменте выделяются экстенты под операцию
  до тех пор, пока не окажется достаточно места. При использовании больших DSS-запросов
  (Decision Support System - см. выпуск первый), эти временные сегменты могут
  стать по-настоящему гигантскими. С использование табличных пространств, специально
  предназначенных для таких операций, не только сортировка становиться более эффективной,
  но и меньше временных сегментов будет использовано в табличных пространствах
  с данными.</p>

<h4>Создание временных табличных пространств</h4>

<p>Табличное пространство может стать временным как во время создания (CREATE),
  так и во время изменения (ALTER). При использовании Enterprise Manager-а надо
  просто в окне диалога создания/изменения табличного пространства поставить галочку
  напротив Temporary. SQL-команда для выполнения этой операции такова:</p>

<h5>ALTER TABLESPACE CARS TEMPORARY;</h5>

<p>Маловероятно, что Вам когда-либо понадобится переводить перманентные табличные
  пространства во временные и обратно. Временное табличное пространство обычно
  создают таким сразу, и оно остается им на все время своего существования.</p>

<pre>

Locally vs. Dictionary Managed Tablespaces
http://www.orafaq.com/node/3

</pre>

<br/>

    CREATE TABLESPACE ts2 DATAFILE '/u02/oradata/ora112/myts2.dbf' SIZE 50M
          EXTENT MANAGEMENT LOCAL
          SEGMENT SPACE MANAGEMENT AUTO;