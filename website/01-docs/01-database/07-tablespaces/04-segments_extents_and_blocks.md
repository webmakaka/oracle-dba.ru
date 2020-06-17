---
layout: page
title: Сегменты > Экстенты > Блоки
description: Сегменты > Экстенты > Блоки
keywords: Oracle Database, Сегменты, Экстенты, Блоки
permalink: /docs/architecture/tablespaces/segments-extents-and-blocks/
---

# Сегменты > Экстенты > Блоки

<br/><br/>

<div align="center">
<img src="https://img.oracledba.net/images/docs/01-oracle-database/07-tablespaces/04-segments_extents_and_blocks/blocks-extents-segments.gif" alt="Блоки Экстенты Сегменты" border="0" />
</div>

<br/>
<h3>Блоки данных (Data Block)</h3>

Блоки данных (Data Block) - мельчайший строительный блок базы данных Oracle, состоящий из определенного количества байт на диске.
Блок данных Oracle - логический компонент базы данных. Диски на которых располагаются блоки Oracle, сами делятся на блоки данных. Обычно блоки данных диска соответствуют блокам данных Oracle.
Размер блока базы данных Oracle устанавливается параметром DB_BLOCK_SIZE в файле init.ora. Размер блока следует воспринимать, как минимальную единицу обновления, выбора или вставки данных.
Общепринятый размер блока - 8 KByte. Если выбрать размер блока 64 KByte, то даже при извлечении имени длиной в четыре символа, придется прочесть весь блок размером 64
KByte, в котором содержатся интересующие четыре буквы.

Все блоки данных можно разделить на две основные части: часть строк данных и часть свободного пространства.

<br/>

<h3>Экстенты (extent)</h3>

Экстенты (extent) - это два или более последовательных блоков данных Oracle, представляющий собой единицу выделения места на диске.
Когда комбинируется несколько непрерывных блоков данных, они называются экстентом. Когда вы создаете объект базы данных вроде таблицы или индекса,
вы выделяете им некоторый начальный объем пространства, называемый начальным экстентом, и, кроме того, указываете размер следующего экстента. Однажды размещенные в таблице или индексе, экстенты остаются выделенными конкретному объекту, пока вы не удалите этот объект из базы данных - тогда пространство,
занимаемое им, вернется в пул свободного пространства базы данных.

<br/>
<h3>Сегменты (segments)</h3>

Сегменты (segments) - набор экстентов, которые вы выделяете логической структуре, такой как таблица или индекс (или некоторый другой объект).
Набор экстентов формирует следующую более крупную единицу хранения, именуемую сегментом. Oracle называет сегментом все пространство, выделенное любому конкретному объекту базы данных.
Поэтому если у вас есть таблица по имени Customer, вы просто ссылаетесь на пространство, выделенное для нее, как на "сегмент Customer". Когда вы создаете индекс, он получает свой собственный сегмент, названные его именем.
Сегменты данных и индексов - наиболее распространенный тип сегментов Oracle. Есть также временные сегменты, которые база данных использует в транзакциях, включающих сортировку, а также сегменты отката, которые база использует для хранения информации отката.
Когда все экстенты сегмента заполнены, Oracle автоматически выделяет дополнительные экстенты при необходимости и эти сегменты могут быть непрерывными.

<table class="RuleInformal" title="Viewing Information About Schema Object Space Use" summary="Column 1 contains the names of views, column 2 describes each view." dir="ltr" border="1" width="100%" frame="border" rules="all" cellpadding="3" cellspacing="0">
<col width="29%" />
<col width="*" />
<thead>
<tr align="left" valign="top">
<th align="left" valign="bottom">View</th>
<th align="left" valign="bottom">Description</th>
</tr>
</thead>
<tbody>
<tr align="left" valign="top">
<td align="left" headers="r1c1-t33"><code>DBA_SEGMENTS</code>
<p><code>USER_SEGMENTS</code></p>
</td>
<td align="left" headers="r2c1-t33 r1c2-t33"><span class="bold"><a name="sthref1724"></a></span>DBA view describes storage allocated for all database segments. User view describes storage allocated for segments for the current user.</td>
</tr>
<tr align="left" valign="top">
<td align="left" headers="r1c1-t33"><code>DBA_EXTENTS</code>
<p><code>USER_EXTENTS</code></p>
</td>
<td align="left" headers="r3c1-t33 r1c2-t33"><span class="bold"><a name="sthref1725"></a></span>DBA view describes extents comprising all segments in the database. User view describes extents comprising segments for the current user.</td>
</tr>
<tr align="left" valign="top">
<td align="left" headers="r1c1-t33"><code>DBA_FREE_SPACE</code>
<p><code>USER_FREE_SPACE</code></p>
</td>
<td align="left" headers="r4c1-t33 r1c2-t33">DBA view lists free extents in all tablespaces. User view shows free space information for tablespaces for which the user has quota.</td>
</tr>
</tbody>
</table>

     SQL> desc DBA_SEGMENTS
     Name                                      Null?    Type
     ----------------------------------------- -------- ----------------------------
     OWNER                                              VARCHAR2(30)
     SEGMENT_NAME                                       VARCHAR2(81)
     PARTITION_NAME                                     VARCHAR2(30)
     SEGMENT_TYPE                                       VARCHAR2(18)
     SEGMENT_SUBTYPE                                    VARCHAR2(10)
     TABLESPACE_NAME                                    VARCHAR2(30)
     HEADER_FILE                                        NUMBER
     HEADER_BLOCK                                       NUMBER
     BYTES                                              NUMBER
     BLOCKS                                             NUMBER
     EXTENTS                                            NUMBER
     INITIAL_EXTENT                                     NUMBER
     NEXT_EXTENT                                        NUMBER
     MIN_EXTENTS                                        NUMBER
     MAX_EXTENTS                                        NUMBER
     MAX_SIZE                                           NUMBER
     RETENTION                                          VARCHAR2(7)
     MINRETENTION                                       NUMBER
     PCT_INCREASE                                       NUMBER
     FREELISTS                                          NUMBER
     FREELIST_GROUPS                                    NUMBER
     RELATIVE_FNO                                       NUMBER
     BUFFER_POOL                                        VARCHAR2(7)
     FLASH_CACHE                                        VARCHAR2(7)
     CELL_FLASH_CACHE                                   VARCHAR2(7)

<br/>

    SQL> desc DBA_EXTENTS
     Name                                      Null?    Type
     ----------------------------------------- -------- ----------------------------
     OWNER                                              VARCHAR2(30)
     SEGMENT_NAME                                       VARCHAR2(81)
     PARTITION_NAME                                     VARCHAR2(30)
     SEGMENT_TYPE                                       VARCHAR2(18)
     TABLESPACE_NAME                                    VARCHAR2(30)
     EXTENT_ID                                          NUMBER
     FILE_ID                                            NUMBER
     BLOCK_ID                                           NUMBER
     BYTES                                              NUMBER
     BLOCKS                                             NUMBER
     RELATIVE_FNO                                       NUMBER

<br/>

     SQL> desc DBA_FREE_SPACE
     Name                                      Null?    Type
     ----------------------------------------- -------- ----------------------------
     TABLESPACE_NAME                                    VARCHAR2(30)
     FILE_ID                                            NUMBER
     BLOCK_ID                                           NUMBER
     BYTES                                              NUMBER
     BLOCKS                                             NUMBER
     RELATIVE_FNO                                       NUMBER

<strong>Displaying Segment Information</strong>

    SQL> SELECT SEGMENT_NAME, TABLESPACE_NAME, BYTES, BLOCKS, EXTENTS
        FROM DBA_SEGMENTS
        WHERE SEGMENT_TYPE = 'INDEX'
        AND OWNER='HR'
        ORDER BY SEGMENT_NAME;

<strong>Displaying Extent Information</strong>

    SQL> SELECT SEGMENT_NAME, SEGMENT_TYPE, TABLESPACE_NAME, EXTENT_ID, BYTES, BLOCKS
        FROM DBA_EXTENTS
        WHERE SEGMENT_TYPE = 'INDEX'
        AND OWNER='HR'
        ORDER BY SEGMENT_NAME;

<strong>Displaying the Free Space (Extents) in a Tablespace</strong>

    SQL> SELECT TABLESPACE_NAME, FILE_ID, BYTES, BLOCKS
        FROM DBA_FREE_SPACE
        WHERE TABLESPACE_NAME='SMUNDO';

<br/>

    SQL>  SELECT segment_name, file_id, block_id
    FROM dba_extents
    WHERE owner = 'SCOTT'
    AND segment_name LIKE 'DEPT%';

<br/>

    SQL> select distinct bytes/blocks from user_segments;

<br/>

    BYTES/BLOCKS
    ------------
            8192

<br/>

    SQL> create tablespace myts1 datafile '/u02/oradata/ora112/myts1_1.dbf' size 512k extent management local;

<br/>

    SQL> create table myt1 (x int) storage(initial 256k next 256k) tablespace myts1;

<br/>

    SQL> select extent_id, bytes, blocks from dba_extents where segment_name = 'MYT1';

<br/>

     EXTENT_ID      BYTES     BLOCKS
    ---------- ---------- ----------
             0      65536          8
             1      65536          8
             2      65536          8
             3      65536          8

<br/>

выделить экстент

    SQL> alter table myt1 allocate extent;

    Table altered.

<br/>

    SQL> alter table myt1 allocate extent;

    Table altered.

<br/>

    SQL> alter table myt1 allocate extent;

    Table altered.

<br/>

    SQL> alter table myt1 allocate extent;
    alter table myt1 allocate extent
    *
    ERROR at line 1:
    ORA-01653: unable to extend table SYSTEM.MYT1 by 8 in tablespace MYTS1

<br/>

    SQL>

     EXTENT_ID      BYTES     BLOCKS
    ---------- ---------- ----------
             0      65536          8
             1      65536          8
             2      65536          8
             3      65536          8
             4      65536          8
             5      65536          8
             6      65536          8

    7 rows selected.

<br/>

7 extenst _ 8 blocks _ block_size (8K) = 448 K
And datafile is 512k
Logically there should be 512k - 448k = 64K free space

<br/>

    SQL> select extents from dba_segments where segment_name = 'MYT1';

<br/>

       EXTENTS
    ----------
             7

<br/>

    SQL> select blocks from dba_extents where segment_name = 'MYT1';

<br/>

        BLOCKS
    ----------
             8
             8
             8
             8
             8
             8
             8

    7 rows selected.
