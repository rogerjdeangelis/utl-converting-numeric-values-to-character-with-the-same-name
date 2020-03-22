# utl-converting-numeric-values-to-character-with-the-same-name
Converting numeric values to character with the same name
    Converting numeric values to character with the same name

    You need to download delimited file from SAS Forum

    github
    https://tinyurl.com/rhdbdhs
    https://github.com/rogerjdeangelis/utl-converting-numeric-values-to-character-with-the-same-name

    SAS Forum
    https://tinyurl.com/te5t7aw
    https://communities.sas.com/t5/SAS-Procedures/change-type-of-variables-numeric-to-character/m-p/633947

    Related github repos

    github
    https://tinyurl.com/y554ztrd
    https://github.com/rogerjdeangelis/utl-converting-all-character-variables-to-numeric-with-the-same-name

    github
    https://tinyurl.com/y37sb9la
    https://github.com/rogerjdeangelis/utl-converting-character-data-in-numeric-columns-to-numbers-using-the-same-column-names


    There is an issue using the variable name 'case' with 'proc sql'.
    I renamed the variable to 'casen';

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    proc import
       datafile="d:/txt/Data_projet_AFRIQUE2.txt"
       dbms=dlm
       out=have(rename=case=casen)
       replace;
       delimiter=';';
       getnames=yes;
    run;quit;


    Middle Observation(529 ) of have - Total Obs 1,059

                                  -TYPE-     -VALUE-        |
     -- CHARACTER --                                        |
    CC3                              C3       MUS           |
    COUNTRY                          C24      Mauritius     |
    EXCH_USD                         C11      5,57016       |
    BANKING_CRISIS                   C9       no_crisis     |
                                                            |

     -- NUMERIC --                                          | RULES
    CASEN                            N8       38            |
    YEAR                             N8       1970          | Convert these to character
    SYSTEMIC_CRISIS                  N8       0             | with the same name
    DOMESTIC_DEBT_IN_DEFAULT         N8       0             |
    SOVEREIGN_EXTERNAL_DEBT_DEFAULT  N8       0             |
    GDP_WEIGHTED_DEFAULT             N8       0             |
    INFLATION_ANNUAL_CPI             N8       11228728      |
    INDEPENDENCE                     N8       1             |
    CURRENCY_CRISES                  N8       0             |
    INFLATION_CRISES                 N8       0             |

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    Middle Observation(529 ) of Last dataset = WORK.WANT - Total Obs 1059


     -- CHARACTER --
    CC3                              C3       MUS
    COUNTRY                          C24      Mauritius
    EXCH_USD                         C11      5,57016
    BANKING_CRISIS                   C9       no_crisis


    CASEN                            C32      38
    YEAR                             C32      1970
    SYSTEMIC_CRISIS                  C32      0
    DOMESTIC_DEBT_IN_DEFAULT         C32      0
    SOVEREIGN_EXTERNAL_DEBT_DEFAULT  C32      0
    GDP_WEIGHTED_DEFAULT             C32      0
    INFLATION_ANNUAL_CPI             C32      11228728
    INDEPENDENCE                     C32      1
    CURRENCY_CRISES                  C32      0
    INFLATION_CRISES                 C32      0

    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;

    %array(nums,values=%utl_varlist(have,keep=_numeric_));
    %array(chrs,values=%utl_varlist(have,keep=_character_));

    %put &=numsn;
    %put &=chrsn;
    %put &=nums5;

    proc sql;
      create
         table want as
      select
         %do_over(chrs,phrase=?,between=comma)
        ,%do_over(nums,phrase=%str(put(?,best32. -l) as ?),between=comma)
      from
         have
    ;quit;

    *          _                 _
     ___  __ _| |   ___ ___   __| | ___
    / __|/ _` | |  / __/ _ \ / _` |/ _ \
    \__ \ (_| | | | (_| (_) | (_| |  __/
    |___/\__, |_|  \___\___/ \__,_|\___|
            |_|
    ;

    * you can get the generated code

    %put %do_over(chrs,phrase=?,between=comma);


    CC3 , COUNTRY , EXCH_USD , BANKING_CRISIS

    %put %do_over(nums,phrase=%str(put(?,best32. -l) as ?),between=comma);

      put(CASEN,best32. -l) as CASEN
    , put(YEAR,best32. -l) as YEAR
    , put(SYSTEMIC_CRISIS,best32. -l) as SYSTEMIC_CRISIS
    , put(DOMESTIC_DEBT_IN_DEFAULT,best32. -l) as DOMESTIC_DEBT_IN_DEFAULT
    , put(SOVEREIGN_EXTERNAL_DEBT_DEFAULT,best32. -l) as SOVEREIGN_EXTERNAL_DEBT_DEFAULT
    , put(GDP_WEIGHTED_DEFAULT,best32. -l) as GDP_WEIGHTED_DEFAULT
    , put(INFLATION_ANNUAL_CPI,best32. -l) as INFLATION_ANNUAL_CPI
    , put(INDEPENDENCE,best32. -l) as INDEPENDENCE
    , put(CURRENCY_CRISES,best32. -l) as CURRENCY_CRISES
    , put(INFLATION_CRISES,best32. -l) as INFLATION_CRISES

    or

    data _null_;
     put
      %do_over(nums,phrase="put(?,best32. -l) as ?" /);
      ;
    run;quit;

    put(CASEN,best32. -l) as CASEN
    put(YEAR,best32. -l) as YEAR
    put(SYSTEMIC_CRISIS,best32. -l) as SYSTEMIC_CRISIS
    put(DOMESTIC_DEBT_IN_DEFAULT,best32. -l) as DOMESTIC_DEBT_IN_DEFAULT
    put(SOVEREIGN_EXTERNAL_DEBT_DEFAULT,best32. -l) as SOVEREIGN_EXTERNAL_DEBT_DEFAULT
    put(GDP_WEIGHTED_DEFAULT,best32. -l) as GDP_WEIGHTED_DEFAULT
    put(INFLATION_ANNUAL_CPI,best32. -l) as INFLATION_ANNUAL_CPI
    put(INDEPENDENCE,best32. -l) as INDEPENDENCE
    put(CURRENCY_CRISES,best32. -l) as CURRENCY_CRISES
    put(INFLATION_CRISES,best32. -l) as INFLATION_CRISES

