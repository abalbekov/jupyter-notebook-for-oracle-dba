One way to connect to oracle from Jupyter Notebook is with cx_Oracle and Easy Connect syntax :
``` python
import cx_Oracle
con=cx_Oracle.connect('{user}/{psw}@{hostname}:{port}/{service_name}')
con.version
```

Another way is to use %sql magic (this still relies on cx_oracle under the covers)
``` python
%load_ext sql
%sql oracle+cx_oracle://{user}:{psw}@{hostname}:{port}/{sid}
%sql select sysdate from dual
```
Notice that connection syntax above uses sid and not service_name. This may be a problem with RAC
