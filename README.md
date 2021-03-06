# utl_cross_platform_unzip_27_files_from_nber_site
Cross Platform Unzip Medicare Point of Sevice Files into SAS datasets.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Cross Platform Unzip Medicare Point of Sevice Files into SAS datasets

    github
    https://tinyurl.com/y84ljxcb
    https://github.com/rogerjdeangelis/utl_cross_platform_unzip_27_files_from_nber_site

    Source zip files
    http://www.nber.org/data/provider-of-services.html

    PROBLEM
         UNZIP d:/pos/zip/pos1991.sas7bdat.zip INTO d:/pos/pos1991.sas7bdat


    INPUT  (META DATA)
    ===================

      Download the very small 27 zip files from
      http://www.nber.org/data/provider-of-services.html
      and put them in folder d:/pos/zip

      WORK.HAVE total obs=27

      Obs      INPDIR      OUTDIR            ZIP

        1    d:/pos/zip    d:/pos    pos1991.sas7bdat.zip
        2    d:/pos/zip    d:/pos    pos1992.sas7bdat.zip
        3    d:/pos/zip    d:/pos    pos1993.sas7bdat.zip
      ...
       25    d:/pos/zip    d:/pos    pos2015.sas7bdat.zip
       26    d:/pos/zip    d:/pos    pos2016.sas7bdat.zip
       27    d:/pos/zip    d:/pos    pos2017.sas7bdat.zip


      EXAMPLE OUTPUT
      --------------

      WORK.LOG

        Up to 40 obs from LOG total obs=27

        Obs      INPDIR      OUTDIR        SAS7BAT        RC     STATUS

          1    d:/pos/zip    d:/pos    pos1991.sas7bdat    0    Completed
          2    d:/pos/zip    d:/pos    pos1992.sas7bdat    0    Completed
          3    d:/pos/zip    d:/pos    pos1993.sas7bdat    0    Completed
        '''
         25    d:/pos/zip    d:/pos    pos2015.sas7bdat    0    Completed
         26    d:/pos/zip    d:/pos    pos2016.sas7bdat    0    Completed
         27    d:/pos/zip    d:/pos    pos2017.sas7bdat    0    Completed


      OUTPUT in d:/pos directory

       d:/pos/pos1991.sas7bdat
       d:/pos/pos1992.sas7bdat
       d:/pos/pos1993.sas7bdat
      ...
       d:/pos/pos2015.sas7bdat
       d:/pos/pos2016.sas7bdat
       d:/pos/pos2017.sas7bdat


    PROCESS
    =======

      %symdel inpDir outDir zip / nowarn;
      data log;

        set have(obs=1);

        sas7bdat=substr(zip,1,16);

        call symputx("inpDir",strip(inpDir));
        call symputx("outDir",strip(outDir));
        call symputx("zip",strip(zip));

        rc=dosubl('
           %utl_submit_r64(resolve(''
             library(R.utils);
             wd=getwd();
             setwd("&inpDir");
             unzip("&zip",exdir="&outDir");
             setwd(wd);
          ''));
          %let rc=&syserr;
       ');

       if symgetn('rc')=0  then status="Completed";
       else status="Failed";

     run;quit;
     
    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;

    data have;
    informat inpdir $10. outDir $7. zip $21.;
    input inpDir outDir zip;
    cards4;
    d:/pos/zip d:/pos pos1991.sas7bdat.zip
    d:/pos/zip d:/pos pos1992.sas7bdat.zip
    d:/pos/zip d:/pos pos1993.sas7bdat.zip
    d:/pos/zip d:/pos pos1994.sas7bdat.zip
    d:/pos/zip d:/pos pos1995.sas7bdat.zip
    d:/pos/zip d:/pos pos1996.sas7bdat.zip
    d:/pos/zip d:/pos pos1997.sas7bdat.zip
    d:/pos/zip d:/pos pos1998.sas7bdat.zip
    d:/pos/zip d:/pos pos1999.sas7bdat.zip
    d:/pos/zip d:/pos pos2000.sas7bdat.zip
    d:/pos/zip d:/pos pos2001.sas7bdat.zip
    d:/pos/zip d:/pos pos2002.sas7bdat.zip
    d:/pos/zip d:/pos pos2003.sas7bdat.zip
    d:/pos/zip d:/pos pos2004.sas7bdat.zip
    d:/pos/zip d:/pos pos2005.sas7bdat.zip
    d:/pos/zip d:/pos pos2006.sas7bdat.zip
    d:/pos/zip d:/pos pos2007.sas7bdat.zip
    d:/pos/zip d:/pos pos2008.sas7bdat.zip
    d:/pos/zip d:/pos pos2009.sas7bdat.zip
    d:/pos/zip d:/pos pos2010.sas7bdat.zip
    d:/pos/zip d:/pos pos2011.sas7bdat.zip
    d:/pos/zip d:/pos pos2012.sas7bdat.zip
    d:/pos/zip d:/pos pos2013.sas7bdat.zip
    d:/pos/zip d:/pos pos2014.sas7bdat.zip
    d:/pos/zip d:/pos pos2015.sas7bdat.zip
    d:/pos/zip d:/pos pos2016.sas7bdat.zip
    d:/pos/zip d:/pos pos2017.sas7bdat.zip
    ;;;;
    run;quit;



    LOG
    ===

    > library(R.utils);         wd=getwd();         setwd("d:/pos/zip");         unzip("pos2017.sas7
    bdat.zip",exdir="d:/pos");         setwd(wd);
    >
    NOTE: 3 lines were written to file PRINT.
    Stderr output:
    Loading required package: R.oo
    Loading required package: R.methodsS3
    R.methodsS3 v1.7.1 (2016-02-15) successfully loaded. See ?R.methodsS3 for help.
    R.oo v1.21.0 (2016-10-30) successfully loaded. See ?R.oo for help.

    Attaching package: 'R.oo'
    The following objects are masked from 'package:methods':
        getClasses, getMethods
    The following objects are masked from 'package:base':
        attach, detach, gc, load, save
    R.utils v2.6.0 (2017-11-04) successfully loaded. See ?R.utils for help.
    Attaching package: 'R.utils'
    The following object is masked from 'package:utils':
        timestamp
    The following objects are masked from 'package:base':
        cat, commandArgs, getOption, inherits, isOpen, parse, warnings

    NOTE: 2 records were read from the infile RUT.
          The minimum record length was 2.
          The maximum record length was 141.
    NOTE: DATA statement used (Total process time):
          real time           3.40 seconds
          user cpu time       0.01 seconds
          system cpu time     0.07 seconds
          memory              1559.00k
          OS Memory           14568.00k
          Timestamp           08/27/2018 12:10:45 PM
          Step Count                        147  Switch Count  0


    MPRINT(UTL_SUBMIT_R64):   filename rut clear;
    NOTE: Fileref RUT has been deassigned.
    MPRINT(UTL_SUBMIT_R64):   filename r_pgm clear;
    NOTE: Fileref R_PGM has been deassigned.
    MPRINT(UTL_SUBMIT_R64):   * use the clipboard to create macro variable;
    SYMBOLGEN:  Macro variable RETURNVAR resolves to N
    MLOGIC(UTL_SUBMIT_R64):  %IF condition %upcase(%substr(&returnVar.,1,1)) ne N is FALSE
    MLOGIC(UTL_SUBMIT_R64):  Ending execution.
    SYMBOLGEN:  Macro variable SYSERR resolves to 0
    NOTE: There were 27 observations read from the data set WORK.HAVE.
    NOTE: The data set WORK.LOG has 27 observations and 5 variables.
    NOTE: DATA statement used (Total process time):
          real time           1:35.36
          user cpu time       2.55 seconds
          system cpu time     5.52 seconds
          memory              1559.00k
          OS Memory           14568.00k
          Timestamp           08/27/2018 12:10:45 PM
          Step Count                        147  Switch Count  54

