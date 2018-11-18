**step1**:使用 docker-compose run 命令启动一个 Django 应用
```shell
docker-compose run web django-admin.py startproject django_example .
```
这将在当前目录生成一个 Django 应用:
```bash
ls
Dockerfile       docker-compose.yml          django_example       manage.py       requirements.txt
```

**step2**:修改文件的权限（Linux用户需要做）
```bash
sudo chown -R $USER:$USER .
```

**step3**: 修改 django_example/settings.py 
```python
import pymysql
pymysql.install_as_MySQLdb()

# 数据库的信息全部使用docker-compose.yml 中定义的
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',  # 修改数据库为MySQL，并进行配置
        'NAME': 'izone',       # 数据库的名称
        'USER': 'root',        # 数据库的用户名
        'PASSWORD': 'python',  # 数据库的密码
        'HOST': 'db',          
        'PORT': 3306,
        'OPTIONS': {'charset': 'utf8mb4', }
    }
}
```

**step4**:启动服务
```bash
docker-compose up
```

**step5**:查看服务运行状态，打开浏览器登录 http://localhost:8000/

**更多命令**：

后台运行
```bash
docker-compose up -d
```
创建表格
```bash
docker-compose run web python manage.py makemigrations
docker-compose run web python manage.py migrate
```
创建管理用户
```bash
docker-compose run web python manage.py createsuperuser
```
查看服务依赖的镜像
```bash
docker-compose images
```
查看服务启动的容器
```bash
docker-compose ps
```
停止服务 && 重启服务
```bash
docker-compose stop
docker-compose restart
```

docker-compose 命令：https://github.com/yeasy/docker_practice/blob/master/compose/commands.md

