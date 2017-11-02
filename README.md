# utl_shift_elements_let_to_remove_missings
Move all missing elements to the right

    ```  How to remove missing data for many variables from dataset to make new data set with complete data.                                                          ```
    ```                                                                                                                                                               ```
    ```    INPUT                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```      WORK.HAVE total obs=5                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```        ID    VAR1    VAR2    VAR3    VAR4    VAR5                                                                                                             ```
    ```                                                                                                                                                               ```
    ```        1      A               B               C                                                                                                               ```
    ```        2      C               A       A                                                                                                                       ```
    ```        3      A                       A       B                                                                                                               ```
    ```        4      B       B       C                                                                                                                               ```
    ```        5      C               A               C                                                                                                               ```
    ```                                                                                                                                                               ```
    ```     PROCESS                                                                                                                                                   ```
    ```      SAS/WPS - same results                                                                                                                                   ```
    ```        * i could not use just the vars array - odd because the 5 letters are all in var1?;                                                                    ```
    ```        data want;                                                                                                                                             ```
    ```          set have;                                                                                                                                            ```
    ```          array vars $1 var1-var5;                                                                                                                             ```
    ```          array outs $1 out1-out5;                                                                                                                             ```
    ```          str=cats(of vars[*]);                                                                                                                                ```
    ```          call pokelong(str,addrlong(out1),5);                                                                                                                 ```
    ```          keep id out:;                                                                                                                                        ```
    ```        run;quit;                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```     OUTPUT                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```       WORK.WANT total obs=5                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```        ID    OUT1    OUT2    OUT3    OUT4    OUT5                                                                                                             ```
    ```                                                                                                                                                               ```
    ```        1      A       B       C                                                                                                                               ```
    ```        2      C       A       A                                                                                                                               ```
    ```        3      A       A       B                                                                                                                               ```
    ```        4      B       B       C                                                                                                                               ```
    ```        5      C       A       C                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://goo.gl/yj4367                                                                                                                                        ```
    ```  https://communities.sas.com/t5/General-SAS-Programming/How-to-remove-missing-data-for-many-variables-from-dataset-to/m-p/409911#M51410                       ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```  data have;                                                                                                                                                   ```
    ```  input id$ var1$ var2$ var3$ var4$ var5$;                                                                                                                     ```
    ```  infile datalines dsd;                                                                                                                                        ```
    ```  cards4;                                                                                                                                                      ```
    ```  1,A,,B,,C                                                                                                                                                    ```
    ```  2,C,,A,A,                                                                                                                                                    ```
    ```  3,A,,,A,B                                                                                                                                                    ```
    ```  4,B,B,C,,                                                                                                                                                    ```
    ```  5,C,,A,,C                                                                                                                                                    ```
    ```  ;;;;                                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  * WPS                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  %utl_submit_wps64('                                                                                                                                          ```
    ```  libname wrk sas7bdat "%sysfunc(pathname(work))";                                                                                                             ```
    ```  data wrk.wantwps;                                                                                                                                            ```
    ```    set wrk.have;                                                                                                                                              ```
    ```    array vars $1 var1-var5;                                                                                                                                   ```
    ```    array outs $1 out1-out5;                                                                                                                                   ```
    ```    str=cats(of vars[*]);                                                                                                                                      ```
    ```    call pokelong(str,addrlong(out1),5);                                                                                                                       ```
    ```    keep id out:;                                                                                                                                              ```
    ```  run;quit;                                                                                                                                                    ```
    ```  ');                                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  * SAS;                                                                                                                                                       ```
    ```  data want;                                                                                                                                                   ```
    ```    set have;                                                                                                                                                  ```
    ```    array vars $1 var1-var5;                                                                                                                                   ```
    ```    array outs $1 out1-out5;                                                                                                                                   ```
    ```    str=cats(of vars[*]);                                                                                                                                      ```
    ```    call pokelong(str,addrlong(out1),5);                                                                                                                       ```
    ```    keep id out:;                                                                                                                                              ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```

