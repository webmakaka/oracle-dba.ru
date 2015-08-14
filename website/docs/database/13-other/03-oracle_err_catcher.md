---
layout: page
title: Ловец ошибок
permalink: /docs/architecture/other/oracle-err-catcher/
---


<h2>Ловец ошибок:</h2>


<strong>Создаем таблицу для записи сообщений об ошибках.</strong>



    CREATE TABLE error_logs (
    id           NUMBER(10)      NOT NULL,
    prefix       VARCHAR2(50),
    data         VARCHAR2(2000)  NOT NULL,
    error_level  NUMBER(2)       NOT NULL,
    created_date DATE            NOT NULL,
    created_by   VARCHAR2(50)    NOT NULL);


<br/>

    ALTER TABLE error_logs ADD (CONSTRAINT error_logs_pk PRIMARY KEY (id));

<br/>

    CREATE SEQUENCE error_logs_seq;



<br/><br/>
<strong>err.pks</strong>


    CREATE OR REPLACE PACKAGE dsp AS
    -- --------------------------------------------------------------------------
    -- Author       : DR Timothy S Hall
    -- Description  : An extension of the DBMS_OUTPUT package.
    -- --------------------------------------------------------------------------

      PROCEDURE reset_defaults;

      PROCEDURE show_output_on;
      PROCEDURE show_output_off;

      PROCEDURE show_date_on;
      PROCEDURE show_date_off;

      PROCEDURE line_wrap_on;
      PROCEDURE line_wrap_off;

      PROCEDURE set_max_width (p_width  IN  NUMBER);

      PROCEDURE set_date_format (p_date_format  IN  VARCHAR2);

      PROCEDURE file_output_on (p_file_dir   IN  VARCHAR2 DEFAULT NULL,
                                p_file_name  IN  VARCHAR2 DEFAULT NULL);

      PROCEDURE file_output_off;

      FUNCTION get_last_prefix
        RETURN VARCHAR2;

      FUNCTION get_last_data
        RETURN VARCHAR2;

      PROCEDURE line (p_data    IN  VARCHAR2);
      PROCEDURE line (p_data    IN  NUMBER);
      PROCEDURE line (p_data    IN  BOOLEAN);
      PROCEDURE line (p_data    IN  DATE,
                      p_format  IN  VARCHAR2 DEFAULT \'DD-MON-YYYY HH24:MI:SS.FF\');

      PROCEDURE line (p_prefix  IN  VARCHAR2,
                      p_data    IN  VARCHAR2);
      PROCEDURE line (p_prefix  IN  VARCHAR2,
                      p_data    IN  NUMBER);
      PROCEDURE line (p_prefix  IN  VARCHAR2,
                      p_data    IN  BOOLEAN);
      PROCEDURE line (p_prefix  IN  VARCHAR2,
                      p_data    IN  DATE,
                      p_format  IN  VARCHAR2 DEFAULT \'DD-MON-YYYY HH24:MI:SS.FF\');

    END dsp;
    /


<br/>
<strong>dsp.pkb</strong>


    CREATE OR REPLACE PACKAGE BODY dsp AS
    -- --------------------------------------------------------------------------
    -- Author       : DR Timothy S Hall
    -- Description  : An extension of the DBMS_OUTPUT package.
    -- Requirements : dsp.pks
    -- --------------------------------------------------------------------------

    -- Package Variables
    g_show_output  BOOLEAN         := FALSE;
    g_show_date    BOOLEAN         := FALSE;
    g_line_wrap    BOOLEAN         := TRUE;
    g_max_width    NUMBER(10)      := 255;
    g_date_format  VARCHAR2(32767) := \'DD-MON-YYYY HH24:MI:SS.FF\';
    g_file_dir     VARCHAR2(32767) := NULL;
    g_file_name    VARCHAR2(32767) := NULL;
    g_last_prefix  VARCHAR2(32767) := NULL;
    g_last_data    VARCHAR2(32767) := NULL;

    -- Hidden Methods
    PROCEDURE display (p_prefix  IN  VARCHAR2,
                       p_data    IN  VARCHAR2);
    PROCEDURE wrap_line (p_data  IN  VARCHAR2);
    PROCEDURE output (p_data  IN  VARCHAR2);


    -- Exposed Methods

    -- --------------------------------------------------------------------------
    PROCEDURE reset_defaults IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_show_output  := FALSE;
      g_show_date    := FALSE;
      g_line_wrap    := TRUE;
      g_max_width    := 255;
      g_date_format  := \'DD-MON-YYYY HH24:MI:SS.FF\';
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE show_output_on IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_show_output := TRUE;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE show_output_off IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_show_output := FALSE;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE show_date_on IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_show_date := TRUE;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE show_date_off IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_show_date := FALSE;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line_wrap_on IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_line_wrap := TRUE;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line_wrap_off IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_line_wrap := FALSE;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE set_max_width (p_width  IN  NUMBER) IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_max_width := p_width;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE set_date_format (p_date_format  IN  VARCHAR2) IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_date_format := p_date_format;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE file_output_on (p_file_dir   IN  VARCHAR2 DEFAULT NULL,
                              p_file_name  IN  VARCHAR2 DEFAULT NULL) IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_file_dir  := p_file_dir;
      g_file_name := p_file_name;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE file_output_off IS
    -- --------------------------------------------------------------------------
    BEGIN
      g_file_dir  := NULL;
      g_file_name := NULL;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    FUNCTION get_last_prefix
      RETURN VARCHAR2 IS
    -- --------------------------------------------------------------------------
    BEGIN
      RETURN g_last_prefix;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    FUNCTION get_last_data
      RETURN VARCHAR2 IS
    -- --------------------------------------------------------------------------
    BEGIN
      RETURN g_last_data;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line (p_data  IN  VARCHAR2) IS
    -- --------------------------------------------------------------------------
    BEGIN
      display (NULL, p_data);
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line (p_data  IN  NUMBER) IS
    -- --------------------------------------------------------------------------
    BEGIN
      display (NULL, p_data);
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line (p_data  IN  BOOLEAN) IS
    -- --------------------------------------------------------------------------
    BEGIN
      line (NULL, p_data);
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line (p_data    IN  DATE,
                    p_format  IN  VARCHAR2 DEFAULT \'DD-MON-YYYY HH24:MI:SS.FF\') IS
    -- --------------------------------------------------------------------------
    BEGIN
      line (NULL, p_data, p_format);
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line (p_prefix  IN  VARCHAR2,
                    p_data    IN  VARCHAR2) IS
    -- --------------------------------------------------------------------------
    BEGIN
      display (p_prefix, p_data);
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line (p_prefix  IN  VARCHAR2,
                    p_data    IN  NUMBER) IS
    -- --------------------------------------------------------------------------
    BEGIN
      display (p_prefix, TO_CHAR(p_data));
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line (p_prefix  IN  VARCHAR2,
                    p_data    IN  BOOLEAN) IS
    -- --------------------------------------------------------------------------
    BEGIN
      IF p_data THEN
        display (p_prefix, \'TRUE\');
      ELSE
        display (p_prefix, \'FALSE\');
      END IF;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE line (p_prefix  IN  VARCHAR2,
                    p_data    IN  DATE,
                    p_format  IN  VARCHAR2 DEFAULT \'DD-MON-YYYY HH24:MI:SS.FF\') IS
    -- --------------------------------------------------------------------------
    BEGIN
      display (p_prefix, TO_CHAR(p_data, p_format));
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE display (p_prefix  IN  VARCHAR2,
                       p_data    IN  VARCHAR2) IS
    -- --------------------------------------------------------------------------
      l_data  VARCHAR2(32767) := p_data;
    BEGIN
      g_last_prefix := p_prefix;
      g_last_data   := p_data;
      IF g_show_output THEN
        IF l_data IS NULL THEN
          l_data := \'\';
        END IF;

        IF p_prefix IS NOT NULL THEN
          l_data := p_prefix || \' : \' || l_data;
        END IF;

        IF g_show_date THEN
          l_data := TO_CHAR(SYSTIMESTAMP, g_date_format) || \' : \' || l_data;
        END IF;

        IF Length(l_data) > g_max_width THEN
          IF g_line_wrap THEN
            wrap_line (l_data);
          ELSE
            l_data := SUBSTR(l_data, 1, g_max_width);
            output (l_data);
          END IF;
        ELSE
          output (l_data);
        END IF;
      END IF;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE wrap_line (p_data  IN  VARCHAR2) IS
    -- --------------------------------------------------------------------------
      l_data  VARCHAR2(32767) := p_data;
    BEGIN
      LOOP
        display (NULL, SUBSTR(l_data, 1, g_max_width));
        l_data := SUBSTR(l_data, g_max_width + 1);
        EXIT WHEN l_data IS NULL;
      END LOOP;
    END;
    -- --------------------------------------------------------------------------


    -- --------------------------------------------------------------------------
    PROCEDURE output (p_data  IN  VARCHAR2) IS
    -- --------------------------------------------------------------------------
    BEGIN
      IF g_file_dir IS NULL OR g_file_name IS NULL THEN
        DBMS_OUTPUT.put_line(p_data);
      ELSE
        DECLARE
          l_file  UTL_FILE.file_type;
        BEGIN
          l_file := UTL_FILE.fopen (g_file_dir, g_file_name, \'A\');
          UTL_FILE.put_line(l_file, p_data);
          UTL_FILE.fclose (l_file);
        EXCEPTION
          WHEN OTHERS THEN
            UTL_FILE.fclose (l_file);
        END;
      END IF;
    END;
    -- --------------------------------------------------------------------------

    END dsp;
    /

<br/>


<strong>err.pks</strong>


    CREATE OR REPLACE PACKAGE err AS
    -- --------------------------------------------------------------------------
    -- Author       : DR Timothy S Hall
    -- Description  : A simple mechanism for logging error information to a table.
    -- Requirements : err.pkb, dsp.pks, dsp.pkb
    -- --------------------------------------------------------------------------

      PROCEDURE reset_defaults;

      PROCEDURE logs_on;
      PROCEDURE logs_off;

      PROCEDURE set_date_format (p_date_format IN VARCHAR2 DEFAULT \'DD-MON-YYYY HH24:MI:SS\');

      PROCEDURE line (p_prefix       IN  VARCHAR2,
                      p_data         IN  VARCHAR2,
                      p_error_level  IN  NUMBER   DEFAULT 5,
                      p_error_user   IN  VARCHAR2 DEFAULT USER);

      PROCEDURE line (p_data         IN  VARCHAR2,
                      p_error_level  IN  NUMBER   DEFAULT 5,
                      p_error_user   IN  VARCHAR2 DEFAULT USER);

      PROCEDURE display (p_error_level  IN  NUMBER   DEFAULT NULL,
                         p_error_user   IN  VARCHAR2 DEFAULT NULL,
                         p_from_date    IN  DATE     DEFAULT NULL,
                         p_to_date      IN  DATE     DEFAULT NUll);
    END err;
    /


<br/>
<strong>err.pkb</strong>



    CREATE OR REPLACE PACKAGE BODY err AS
    -- --------------------------------------------------------------------------
    -- Author       : DR Timothy S Hall
    -- Description  : A simple mechanism for logging error information to a table.
    -- Requirements : err.pks, dsp.pks, dsp.pkb
    -- --------------------------------------------------------------------------

      -- Package Variables
      g_logs_on     BOOLEAN      := TRUE;
      g_date_format  VARCHAR2(50) := \'DD-MON-YYYY HH24:MI:SS\';

      -- Exposed Methods

      -- --------------------------------------------------------------------------
      PROCEDURE reset_defaults IS
      -- --------------------------------------------------------------------------
      BEGIN
        g_logs_on      := TRUE;
        g_date_format  := \'DD-MON-YYYY HH24:MI:SS\';
      END;
      -- --------------------------------------------------------------------------


      -- --------------------------------------------------------------------------
      PROCEDURE logs_on IS
      -- --------------------------------------------------------------------------
      BEGIN
        g_logs_on := TRUE;
      END;
      -- --------------------------------------------------------------------------


      -- --------------------------------------------------------------------------
      PROCEDURE logs_off IS
      -- --------------------------------------------------------------------------
      BEGIN
        g_logs_on := FALSE;
      END;
      -- --------------------------------------------------------------------------


      -- --------------------------------------------------------------------------
      PROCEDURE set_date_format (p_date_format IN VARCHAR2 DEFAULT \'DD-MON-YYYY HH24:MI:SS\') IS
      -- --------------------------------------------------------------------------
      BEGIN
        g_date_format := p_date_format;
      END;
      -- --------------------------------------------------------------------------


      -- --------------------------------------------------------------------------
      PROCEDURE line (p_prefix       IN  VARCHAR2,
                      p_data         IN  VARCHAR2,
                      p_error_level  IN  NUMBER   DEFAULT 5,
                      p_error_user   IN  VARCHAR2 DEFAULT USER) IS
      -- --------------------------------------------------------------------------
        PRAGMA AUTONOMOUS_TRANSACTION;
      BEGIN
        IF g_logs_on THEN
          INSERT INTO error_logs
          (id,
           prefix,
           data,
           error_level,
           created_date,
           created_by)
          VALUES
          (error_logs_seq.NEXTVAL,
           p_prefix,
           p_data,
           p_error_level,
           SYSDATE,
           p_error_user);

          COMMIT;
        END IF;
      END;
      -- --------------------------------------------------------------------------


      -- --------------------------------------------------------------------------
      PROCEDURE line (p_data         IN  VARCHAR2,
                      p_error_level  IN  NUMBER   DEFAULT 5,
                      p_error_user   IN  VARCHAR2 DEFAULT USER) IS
      -- --------------------------------------------------------------------------
        PRAGMA AUTONOMOUS_TRANSACTION;
      BEGIN
        line (p_prefix       => NULL,
              p_data         => p_data,
              p_error_level  => p_error_level,
              p_error_user   => p_error_user);
      END;
      -- --------------------------------------------------------------------------


      -- --------------------------------------------------------------------------
      PROCEDURE display (p_error_level  IN  NUMBER   DEFAULT NULL,
                         p_error_user   IN  VARCHAR2 DEFAULT NULL,
                         p_from_date    IN  DATE     DEFAULT NULL,
                         p_to_date      IN  DATE     DEFAULT NUll) IS
      -- --------------------------------------------------------------------------
        CURSOR c_errors IS
          SELECT *
          FROM   error_logs
          WHERE  error_level   = NVL(p_error_level, error_level)
          AND    created_by    = NVL(p_error_user, created_by)
          AND    created_date >= NVL(p_from_date, created_date)
          AND    created_date <= NVL(p_to_date, created_date)
          ORDER BY id;
      BEGIN
        FOR cur_rec IN c_errors LOOP
          dsp.line(cur_rec.prefix, cur_rec.data);
        END LOOP;
      END;
      -- --------------------------------------------------------------------------

    END err;
    /

<br/>


    execute err.line(\'This is an error\');


<br/>

<strong>@list_error_logs.sql</strong>

 <br/><br/>


    set feedback off
    alter session set nls_timestamp_format=\'DD-MON-YYYY HH:MI:SS\';

    set feedback on
    set verify off
    set linesize 640
    column id format 99999
    column prefix format a20
    column data format a30
    column created_date format a20
    column created_by format a10



    select
      id,
      prefix,
      data,
      error_level,
      created_date,
      created_by
    from
      error_logs
    where
      nvl(prefix, \'-\') = decode(upper(\'&1\'), \'ALL\', nvl(prefix, \'-\'), \'&1\')
    order by
      id
    ;

<br/>



    SQL> @list_error_logs.sql all

        ID PREFIX               DATA                           ERROR_LEVEL CREATED_DATE         CREATED_BY
    ------ -------------------- ------------------------------ ----------- -------------------- ----------
         1                      This is an error                         5 03.08.2012 21:38:26  SYS

    1 row selected.


<br/>


    CREATE OR REPLACE PROCEDURE exception_job_proc AS
    BEGIN
    -- Force an error.
    RAISE_APPLIcATION_ERROR(-20000, \'Forced error in exception_job_proc\');

    EXCEPTION
      WHEN OTHERS THEN
        ERR.line(p_prefix => \'exception_job_proc\',
        p_data => SQLERRM);


    END exception_job_proc;
    /

<br/>



    EXEC exception_job_proc


 <br/>


    SQL> @list_error_logs.sql exception_job_proc

        ID PREFIX               DATA                           ERROR_LEVEL CREATED_DATE         CREATED_BY
    ------ -------------------- ------------------------------ ----------- -------------------- ----------
         2 exception_job_proc   ORA-20000: Forced error in exc           5 03.08.2012 23:42:01  SYS
                                eption_job_proc


    1 row selected.
