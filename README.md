# utl-given-group-a-and-subgroup-b1-and-b2-select-the-b-with-the-maximum-x-value-sas-r-python-exel
Given group a and subgroup b1 and b2 select the b with the maximum x value sas r python exel 
    %let pgm=utl-given-group-a-and-subgroup-b1-and-b2-select-the-b-with-the-maximum-x-value-sas-r-python-exel;

    Given group a and subgroup b1 and b2 select the b with the maximum x value sas r python exel

    I was unable to install the python polars language.
    All posted solutions in stackoverflow use the polars language.

      SOLUTIONS
           1 sas sql
           2 error polar python
             My processor suppors all of these
             ERROR
             The following required CPU features were not detected:
                avx2, fma, bmi1, bmi2, lzcnt, movbe
           3 r sql
           4 python sql
           5 sas dow loop
           6 excel not shown see https://tinyurl.com/2s92n76c


    stackoverflow
    https://tinyurl.com/2vyfbd8s
    https://stackoverflow.com/questions/79384474/polars-get-column-value-at-another-columns-min-max-value


    /**************************************************************************************************************************/
    /*                              |                                                      |                                  */
    /*      INPUT                   |       PROCESS                                        | OUTPUT                           */
    /*      =====                   |       =======                                        | ======                           */
    /*                              |                                                      |                                  */
    /*                              |                                                      |  A  B   X MAX_B                  */
    /*    A     B      X            |  1 SAS SQL SAME CODE                                 |                                  */
    /*                              |    SAS R PYTHON R EXCEL                              |  a0 b1  0  b2 (b with max x)     */
    /*    a0    b1     0            |  ======================                              |  a0 b2 10  b2                    */
    /*    a0    b2    10            |                                                      |  a1 b1  5  b1                    */
    /*    a1    b1     5            |  select                                              |  a1 b2  1  b1                    */
    /*    a1    b2     1            |    l.a                                               |                                  */
    /*                              |   ,l.b                                               |                                  */
    /*  options validvarname=upcase;|   ,l.x                                               |                                  */
    /*  libname sd1 "d:/sd1";       |   ,r.b as max_b                                      |                                  */
    /*  data sd1.have;              |  from                                                |                                  */
    /*  input a$ b$ x;              |    sd1.have as l left join (                         |                                  */
    /*  cards4;                     |     select                                           |                                  */
    /*  a0 b1 0                     |       a                                              |                                  */
    /*  a0 b2 10                    |      ,b                                              |                                  */
    /*  a1 b1 5                     |      ,x                                              |                                  */
    /*  a1 b2 1                     |     from                                             |                                  */
    /*  ;;;;                        |       sd1.have                                       |                                  */
    /*  run;quit;                   |     group                                            |                                  */
    /*                              |       by a                                           |                                  */
    /*                              |     having                                           |                                  */
    /*                              |       x = max(x)                                     |                                  */
    /*                              |     /*----                                           |                                  */
    /*                              |      A     B      X                                  |                                  */
    /*                              |      a0    b2    10                                  |                                  */
    /*                              |      a1    b1     5                                  |                                  */
    /*                              |     ----*/                                           |                                  */
    /*                              |     ) as r                                           |                                  */
    /*                              |  on l.a = r.a                                        |                                  */
    /*                              |                                                      |                                  */
    /*                              |-----------------------------------------------------------------------------------------*/
    /*                              |                                                      |                                  */
    /*                              | 2 ERROR POLAR PYTHON                                 |                                  */
    /*                              | ====================                                 |                                  */
    /*                              | (complex single line of code?)                       |                                  */
    /*                              |                                                      |                                  */
    /*                              | have.with_columns(                                   |                                  */
    /*                              |  pl.col.B.sort_by("X").last().over("A").alias("y")   |                                  */
    /*                              |  )                                                   |                                  */
    /*                              |                                                      |                                  */
    /*                              |-----------------------------------------------------------------------------------------*/
    /*                              |                                                      |                                  */
    /*                              | 5 SAS DATASTEP                                       |                                  */
    /*                              | ==============                                       |                                  */
    /*                              |                                                      |                                  */
    /*                              | data want;                                           |                                  */
    /*                              |                                                      |                                  */
    /*                              |   do until (last.a);                                 |                                  */
    /*                              |     set sd1.have;                                    |                                  */
    /*                              |     by a;                                            |                                  */
    /*                              |     if x > val then do;                              |                                  */
    /*                              |         val= x;                                      |                                  */
    /*                              |         bmax=b;                                      |                                  */
    /*                              |     end;                                             |                                  */
    /*                              |   end;                                               |                                  */
    /*                              |                                                      |                                  */
    /*                              |   do until (last.a);                                 |                                  */
    /*                              |     set sd1.have;                                    |                                  */
    /*                              |     by a;                                            |                                  */
    /*                              |     output;                                          |                                  */
    /*                              |   end;                                               |                                  */
    /*                              |                                                      |                                  */
    /*                              | run;quit;                                            |                                  */
    /*                              |                                                      |                                  */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
    input a$ b$ x;
    cards4;
    a0 b1 0
    a0 b2 10
    a1 b1 5
    a1 b2 1
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   A     B      X                                                                                                       */
    /*                                                                                                                        */
    /*   a0    b1     0                                                                                                       */
    /*   a0    b2    10                                                                                                       */
    /*   a1    b1     5                                                                                                       */
    /*   a1    b2     1                                                                                                       */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                             _
    / |  ___  __ _ ___   ___  __ _| |
    | | / __|/ _` / __| / __|/ _` | |
    | | \__ \ (_| \__ \ \__ \ (_| | |
    |_| |___/\__,_|___/ |___/\__, |_|
                                |_|
    */

    proc sql;
      create
        table want as
      select
        l.a
       ,l.b
       ,l.x
       ,r.b as max_b
      from
        sd1.have as l left join (
         select
           a
          ,b
          ,x
         from
           sd1.have
         group
           by a
         having
           x = max(x)

         /*----
          A     B      X
          a0    b2    10
          a1    b1     5
         ----*/
         ) as r
     on l.a = r.a
    ;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   A     B      X    MAX_B                                                                                              */
    /*                                                                                                                        */
    /*   a0    b1     0     b2                                                                                                */
    /*   a0    b2    10     b2                                                                                                */
    /*   a1    b1     5     b1                                                                                                */
    /*   a1    b2     1     b1                                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                   _
    |___ /  _ __   ___  __ _| |
      |_ \ | `__| / __|/ _` | |
     ___) || |    \__ \ (_| | |
    |____/ |_|    |___/\__, |_|
                   |_|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(sqldf)
    source("c:/oto/fn_tosas9x.R")
    have<-read_sas("d:/sd1/have.sas7bdat")
    print(have)
    want <- sqldf('
      select
        l.a
       ,l.b
       ,l.x
       ,r.b as max_b
      from
        have as l left join (
         select
           a
          ,b
          ,x
         from
           have
         group
           by a
         having
           x = max(x)
         ) as r
     on l.a = r.a
     ')
    want;
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                   |                                                                                                    */
    /* R                 | SAS                                                                                                */
    /*                   |                                                                                                    */
    /*    A  B  X MAX_B  | ROWNAMES    A     B      X    MAX_B                                                                */
    /*                   |                                                                                                    */
    /* 1 a0 b1  0    b2  |     1       a0    b1     0     b2                                                                  */
    /* 2 a0 b2 10    b2  |     2       a0    b2    10     b2                                                                  */
    /* 3 a1 b1  5    b1  |     3       a1    b1     5     b1                                                                  */
    /* 4 a1 b2  1    b1  |     4       a1    b2     1     b1                                                                  */
    /*                   |                                                                                                    */
    /**************************************************************************************************************************/

    /*  _                 _   _                             _
    | || |    _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
    | || |_  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
    |__   _| | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
       |_|   | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
             |_|    |___/                                |_|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_pybeginx;
    parmcards4;
    exec(open('c:/oto/fn_python.py').read());
    have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat');
    want=pdsql('''
      select
        l.a                      \
       ,l.b                      \
       ,l.x                      \
       ,r.b as max_b             \
      from                       \
        have as l left join (    \
         select                  \
           a                     \
          ,b                     \
          ,x                     \
         from                    \
           have                  \
         group                   \
           by a                  \
         having                  \
           x = max(x)            \
         ) as r                  \
     on l.a = r.a
       ''');
    print(want);
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx;

    proc print data=sd1.pywant;
    run;quit;


    /**************************************************************************************************************************/
    /*                       |                                                                                                */
    /* R                     | SAS                                                                                            */
    /*                       |                                                                                                */
    /*     A   B     X max_b | A     B      X    MAX_B                                                                        */
    /*                       |                                                                                                */
    /* 0  a0  b1   0.0    b2 | a0    b1     0     b2                                                                          */
    /* 1  a0  b2  10.0    b2 | a0    b2    10     b2                                                                          */
    /* 2  a1  b1   5.0    b1 | a1    b1     5     b1                                                                          */
    /* 3  a1  b2   1.0    b1 | a1    b2     1     b1                                                                          */
    /*                       |                                                                                                */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
