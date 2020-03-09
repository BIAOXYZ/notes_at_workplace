
# DB2官方

Tutorial: Using the command line processor https://www.ibm.com/support/knowledgecenter/SSEPEK_10.0.0/comref/src/tpc/db2z_tut_clp.html

Command line processor CONNECT command https://www.ibm.com/support/knowledgecenter/SSEPEK_10.0.0/comref/src/tpc/db2z_clpconnectsyntax.html

# DB2其他

Connecting to a Database in Db2 Database Server https://www.db2tutorial.com/getting-started/db2-connect-to-database/
```
C:\Program Files\IBM\SQLLIB\BIN>db2
db2 => connect to books user db2admin using your_password
```

How to Connect to a DB2 Database https://www.xtivia.com/how-to-connect-to-a-db2-database/
- > `db2 list db directory`

How to see the schema of a db2 table (file) https://stackoverflow.com/questions/153769/how-to-see-the-schema-of-a-db2-table-file
- > `db2 describe table user1.department`

# DB2故障处理

### `db2 connect to trader`时报SQL10007N

> 注：其实就是下面的链接里这个脚本连接数据库时出的问题（当然脚本连不上是因为当时名为trader的数据库建不起来），我自己手动登进DB2的pod去试着连DB2，报了这个这个错。后来证明原因是db2的机制要求必须切换到特定的数据库，所以登进去时候是root，应该先执行下 su - db2inst1
>> https://github.com/IBMStockTrader/stocktrader-helm/blob/3981d650f314dfbebedc474818956d361b421080/scripts/setupDB2.sh

DB2START Fails with SQL10007N Message "-1390" could not be retrieved. Reason code: "3" https://www.ibm.com/support/pages/db2start-fails-sql10007n-message-1390-could-not-be-retrieved-reason-code-3

db2关于脚本报错SQL10007N Message "-1390" could not be retrieved. Reason code: "3". https://zhidao.baidu.com/question/578517851.html

SQL10007N Message "-1390" could not be retrieved. Reason code: "3" https://blog.csdn.net/yixiyanyu/article/details/38515825