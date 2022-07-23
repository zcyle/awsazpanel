docker创建网络

- docker network create cdntip_network

启动mysql容器

- mkdir /data
- docker run -d -it --network cdntip_network -v /data/mysql:/var/lib/mysql --name panel_mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=panel mysql:5.7 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci

启动 cloudpanel 

- docker run -d -it --network cdntip_network -p 8111:80 --name panel cdntip/panel

进入容器

- docker exec -it panel /bin/bash

创建管理员
- python manage.py createsuperuser --username admin --email admin@admin.com

添加aws镜像
- python manage.py aws_update_images


打开浏览器，输入  ip:8111

其它说明
- 后端暂时未上传到github, 但是代码都是未加密的, 在容器中可以看到。
- docker 暂时只有x86平台(不支持arm平台)
- 目前版本为预览版，有问题请到群里反馈 @cdntip
