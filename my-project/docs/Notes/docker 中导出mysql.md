docker 中导出mysql
docker exec -it  mysql_server mysqldump -uroot -proot test_db > /opt/sql_bak/test_db.sql
将文件复制进docker 容器
docker cp /opt/gysql.sql  gysql （容器名称）:/opt/gysql.sql 
选择数据库
use database;
执行命令
source /opt/gysql.sql