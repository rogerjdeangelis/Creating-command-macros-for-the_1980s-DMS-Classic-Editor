# Creating-command-macros-for-the_1980s-DMS-Editor
Creating command macros for the 1980s DMS Editor

    Creating command macros for the 1980s DMS Classic Editor

      Thanks to Rick Langston, it is much easier to run all of SAS on a
      function key, mouse action or the 1980s clean command line.
      It is also possible to programmatically read text from the program editor
      in a number of ways and pass the text to a command macro.

      I wish the SAS brain trust would experiment mor with DOSUBL and %dosubl.
      Bart and I have tried and discovered some powerful functionality?

      This is a dumb I have about 100 more interesting command macros, R head, tail, summary ....

    Type:  fq class sex*age on the 1980s DMS Editor

    Command ===> fq class sex*age
    00001
    00002
    00003
    ...

    This will appear in the output window


    The FREQ Procedure

                                           Cumulative    Cumulative
    SEX    AGE    Frequency     Percent     Frequency      Percent
    ---------------------------------------------------------------
    F       11           1        5.26             1         5.26
    F       12           2       10.53             3        15.79
    F       13           2       10.53             5        26.32
    F       14           2       10.53             7        36.84
    F       15           2       10.53             9        47.37
    M       11           1        5.26            10        52.63
    M       12           3       15.79            13        68.42
    M       13           1        5.26            14        73.68
    M       14           2       10.53            16        84.21
    M       15           2       10.53            18        94.74
    M       16           1        5.26            19       100.00


    Put this macros in your autocall library

    %macro fq / cmd parmbuff;
       %local sd1 var  rc;
       %let sd1=%scan(&syspbuff,1);
       %let var=%scan(&syspbuff,2,%str( ));
       %let rc=%dosubl('
          proc freq data=sashelp.&sd1;
            table &var / list;
          run;quit;
        ');
    %mend fq;

    Note if you highlight the dataset or the variable in your program editor
    that text can be read by command macros
    
     * you need this macro;
    %macro dosubl(arg);
    %let rc=%qsysfunc(dosubl(&arg));
    %mend dosubl;

    Other Classic editor functionality
    https://github.com/rogerjdeangelis?tab=repositories&q=classic+editor&type=&language=
