# utl-proc-tabulate-using-a-second-dataset-to-capture-missing-columns-or-rows
    Second classdata dataset in proc tabulte is an alternative to 'preloadfmt'.                                                               
                                                                                                                                              
           Two Solutions                                                                                                                      
                                                                                                                                              
               a. using class dataset with 'proc tabulate'                                                                                    
               b.using preloadfmt                                                                                                             
                                                                                                                                              
    github                                                                                                                                    
    run;quit;https://tinyurl.com/y47ttp4e                                                                                                     
    https://github.com/rogerjdeangelis/utl-proc-tabulate-using-a-second-dataset-to-capture-missing-columns-or-rows                            
                                                                                                                                              
    StackOverflow                                                                                                                             
    https://tinyurl.com/y64a5nwx                                                                                                              
    https://stackoverflow.com/questions/63221367/how-to-create-a-table-in-sas-to-view-the-count-of-column-variable-with-respect-t             
                                                                                                                                              
    macros                                                                                                                                    
    https://tinyurl.com/y9nfugth                                                                                                              
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                                                
                                                                                                                                              
    Problem: My proc tabulate yeilds                                                                                                          
                                                                                                                                              
                                                                                                                                              
        ---------------------------------------------------------                                                                             
        |B  |                         B                         |                                                                             
        |   |---------------------------------------------------|                                                                             
        |   |     0      |     1      |     2      |     4      |                                                                             
        |---+------------+------------+------------+------------|                                                                             
        |0  |        2.00|        1.00|        1.00|           0|                                                                             
        |---+------------+------------+------------+------------|                                                                             
        |1  |        1.00|        1.00|           0|        1.00|                                                                             
        |---+------------+------------+------------+------------|                                                                             
        |2  |        1.00|           0|           0|        2.00|                                                                             
        |---+------------+------------+------------+------------|                                                                             
        |3  |           0|           0|        1.00|        2.00|                                                                             
        |---+------------+------------+------------+------------|                                                                             
        |4  |        1.00|        2.00|        4.00|           0|                                                                             
        ---------------------------------------------------------                                                                             
                                                                                                                                              
    But I want and I want a dataset                                                                                                           
                                                                                                                                              
    ----------------------------------------------------------------------                                                                    
    |A  |                               B                                |                                                                    
    |   |----------------------------------------------------------------|                                                                    
    |   |     0      |     1      |     2      |     3      |     4      |                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |0  |        2.00|        1.00|        1.00|           0|           0|                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |1  |        1.00|        1.00|           0|           0|        1.00|                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |2  |        1.00|           0|           0|           0|        2.00|                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |3  |           0|           0|        1.00|           0|        2.00|                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |4  |        1.00|        2.00|        4.00|           0|           0|                                                                    
    ----------------------------------------------------------------------                                                                    
                                                                                                                                              
    /*                   _                                                                                                                    
    (_)_ __  _ __  _   _| |_                                                                                                                  
    | | `_ \| `_ \| | | | __|                                                                                                                 
    | | | | | |_) | |_| | |_                                                                                                                  
    |_|_| |_| .__/ \__,_|\__|                                                                                                                 
            |_|                                                                                                                               
    */                                                                                                                                        
                                                                                                                                              
    data have;                                                                                                                                
      call streaminit(123);                                                                                                                   
      do id = 1 to 20;                                                                                                                        
        A = rand('integer',0,4);                                                                                                              
        do until (b ne 3);                                                                                                                    
          B = rand('integer',0,4);                                                                                                            
        end;                                                                                                                                  
                                                                                                                                              
        output;                                                                                                                               
      end;                                                                                                                                    
    run;                                                                                                                                      
                                                                                                                                              
    * not 3 is not in the table;                                                                                                              
    WORK.HAVE total obs=20                                                                                                                    
                                                                                                                                              
     ID    A    B                                                                                                                             
                                                                                                                                              
      1    2    0                                                                                                                             
      2    0    1                                                                                                                             
      3    1    1                                                                                                                             
      4    1    0                                                                                                                             
      5    0    0                                                                                                                             
      6    4    1                                                                                                                             
      7    2    4                                                                                                                             
      8    3    4                                                                                                                             
      9    1    4                                                                                                                             
     10    0    2                                                                                                                             
     11    4    0                                                                                                                             
     12    0    0                                                                                                                             
     13    3    4                                                                                                                             
     14    3    2                                                                                                                             
     15    4    2                                                                                                                             
     16    4    2                                                                                                                             
     17    4    1                                                                                                                             
     18    2    4                                                                                                                             
     19    4    2                                                                                                                             
     20    4    2                                                                                                                             
                                                                                                                                              
                                                                                                                                              
    * We have level = 3 here;                                                                                                                 
    WORK.ALLPAIRS total obs=25                                                                                                                
                                                                                                                                              
      A    B                                                                                                                                  
                                                                                                                                              
      0    0                                                                                                                                  
      0    1                                                                                                                                  
      0    2                                                                                                                                  
      0    3                                                                                                                                  
      0    4                                                                                                                                  
                                                                                                                                              
      1    0                                                                                                                                  
      1    1                                                                                                                                  
      1    2                                                                                                                                  
      1    3                                                                                                                                  
      1    4                                                                                                                                  
                                                                                                                                              
      2    0                                                                                                                                  
      2    1                                                                                                                                  
      2    2                                                                                                                                  
      2    3                                                                                                                                  
      2    4                                                                                                                                  
                                                                                                                                              
      3    0                                                                                                                                  
      3    1                                                                                                                                  
      3    2                                                                                                                                  
      3    3                                                                                                                                  
      3    4                                                                                                                                  
                                                                                                                                              
      4    0                                                                                                                                  
      4    1                                                                                                                                  
      4    2                                                                                                                                  
      4    3                                                                                                                                  
      4    4                                                                                                                                  
                                                                                                                                              
                                                                                                                                              
                                                                                                                                              
    /*           _               _                                                                                                            
      ___  _   _| |_ _ __  _   _| |_                                                                                                          
     / _ \| | | | __| `_ \| | | | __|                                                                                                         
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                          
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                         
                    |_|                                                                                                                       
    */                                                                                                                                        
                                                                                                                                              
    Static output                                                                                                                             
                                                                                                                                              
    ----------------------------------------------------------------------                                                                    
    |A  |     0      |     1      |     2      |     3      |     4      |                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |0  |        2.00|        1.00|        1.00|           0|           0|                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |1  |        1.00|        1.00|           0|           0|        1.00|                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |2  |        1.00|           0|           0|           0|        2.00|                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |3  |           0|           0|        1.00|           0|        2.00|                                                                    
    |---+------------+------------+------------+------------+------------|                                                                    
    |4  |        1.00|        2.00|        4.00|           0|           0|                                                                    
    ----------------------------------------------------------------------                                                                    
                                                                                                                                              
    OUTPUT DATASET (SAME WITH PRELOADFMT AND CLASSDATA)                                                                                       
                                                                                                                                              
    Up to 40 obs from WANT_TAB total obs=5                                                                                                    
                                                                                                                                              
     J1A      J20    J31    J42    J53    J64                                                                                                 
                                                                                                                                              
      0        2      1      1      0      0                                                                                                  
      1        1      1      0      0      1                                                                                                  
      2        1      0      0      0      2                                                                                                  
      3        0      0      1      0      2                                                                                                  
      4        1      2      4      0      0                                                                                                  
                                                                                                                                              
    * to print;                                                                                                                               
    proc print data=want_tab(drop=V: rename=( J1A=A J20=B0 J31=B1 J42=B2 J53=B3 J64=B4)) width=min;                                           
    run;quit;                                                                                                                                 
                                                                                                                                              
     A    B0    B1    B2    B3    B4                                                                                                          
                                                                                                                                              
     0    2     1     1     0     0                                                                                                           
     1    1     1     0     0     1                                                                                                           
     2    1     0     0     0     2                                                                                                           
     3    0     0     1     0     2                                                                                                           
     4    1     2     4     0     0                                                                                                           
                                                                                                                                              
    /*                                                                                                                                        
     _ __  _ __ ___   ___ ___  ___ ___                                                                                                        
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|                                                                                                       
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                                       
    | .__/|_|  \___/ \___\___||___/___/                                                                                                       
    |_|             _                   _       _                                                                                             
      __ _      ___| | __ _ ___ ___  __| | __ _| |_ __ _                                                                                      
     / _` |    / __| |/ _` / __/ __|/ _` |/ _` | __/ _` |                                                                                     
    | (_| |_  | (__| | (_| \__ \__ \ (_| | (_| | || (_| |                                                                                     
     \__,_(_)  \___|_|\__,_|___/___/\__,_|\__,_|\__\__,_|                                                                                     
                                                                                                                                              
    */                                                                                                                                        
    data have;                                                                                                                                
      call streaminit(123);                                                                                                                   
      do id = 1 to 20;                                                                                                                        
        A = rand('integer',0,4);                                                                                                              
        do until (b ne 3);                                                                                                                    
          B = rand('integer',0,4);                                                                                                            
        end;                                                                                                                                  
                                                                                                                                              
        output;                                                                                                                               
      end;                                                                                                                                    
    run;                                                                                                                                      
                                                                                                                                              
    proc format ;                                                                                                                             
      value num2num                                                                                                                           
        1='1'                                                                                                                                 
        2='2'                                                                                                                                 
        3='3'                                                                                                                                 
        4='4'                                                                                                                                 
    ;                                                                                                                                         
    run;quit;                                                                                                                                 
                                                                                                                                              
    %utl_odstab(setup);                                                                                                                       
    options  formchar="|";                                                                                                                    
    proc tabulate data=have classdata=allpairs;                                                                                               
      class a b;                                                                                                                              
      table a="", b=""*n=' ' /rts=5 box='A' misstext='0';                                                                                     
    run;quit;                                                                                                                                 
    %utl_odstab(outdsn=want_tab);                                                                                                             
    options FORMCHAR='|----|+|---+=|-/\<>*';                                                                                                  
                                                                                                                                              
    /*                       _                 _  __           _                                                                              
    | |__     _ __  _ __ ___| | ___   __ _  __| |/ _|_ __ ___ | |_                                                                            
    | `_ \   | `_ \| `__/ _ \ |/ _ \ / _` |/ _` | |_| `_ ` _ \| __|                                                                           
    | |_) |  | |_) | | |  __/ | (_) | (_| | (_| |  _| | | | | | |_                                                                            
    |_.__(_) | .__/|_|  \___|_|\___/ \__,_|\__,_|_| |_| |_| |_|\__|                                                                           
             |_|                                                                                                                              
    */                                                                                                                                        
                                                                                                                                              
    %utl_odstab(setup);                                                                                                                       
    options missing = '0' formchar="|";                                                                                                       
    proc tabulate data=have ;                                                                                                                 
      format a b num2num.;                                                                                                                    
      class a b /  preloadfmt missing;                                                                                                        
      table a="", b=""*n=' ' /rts=5 box='A'  misstext='0' printmiss;                                                                          
    run;quit;                                                                                                                                 
    %utl_odstab(outdsn=want_tab);                                                                                                             
    options FORMCHAR='|----|+|---+=|-/\<>*';                                                                                                  
                                                                                                                                              
                                                                                                                                              
                                                                                                                                              
