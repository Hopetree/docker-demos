# mysql 容器导入本地sql的操作

**step1**:启动docker-compose中mysql的服务
```bash
docker-compose start db
```

**step2**:把本地的sql文件复制到db_data挂载目录中传递给容器

**step3**:使用命令进入运行中的db容器，然后执行数据库表格导入命令
```bash
docker exec -it 67a72b2c711a bash
mysql -uroot -p$MYSQL_ROOT_PASSWORD -D izone --default-character-set=utf8mb4 < /var/lib/mysql/tendcode_20180825-040001.sql
```

**step3**:重启容器
```bash
docker-compose start
docker-compose restart
```