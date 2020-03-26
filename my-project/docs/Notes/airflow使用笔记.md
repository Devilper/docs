# airflow笔记
##　airflow 常用命令行 
### 初始化数据库
`airflow initdb`
### 启动airflow
`airflow webserver -p 8081 -D`　守护进程运行webserver
### 启动调度器
`airflow scheduler -D`　守护进程运行调度
### 测试Ｔask
`airflow test [dag_id] [task_id] [execution_date]`
Example:airflow test example_hello_world_dag hello_task 20180516
### 运行Ｔask
`airflow run dag_id task_id execution_date`
`airflow run -A dag_id task_id execution_date` 忽略依赖
### 运行dag
`airflow trigger_dag dag_id -r RUN_ID -e EXEC_DATE` 运行整个dag文件
### 查看task列表
`airflow list_tasks [dag_id]` 查看task列表
