## docker-compose方式快速创建Jimv-C节点
Jimv-C地址: https://github.com/jamesiter/JimV-C

### 说明
1、在docker-compose.yml文件base构建参数处手动填写相关信息，包括mysql及redis信息

2、在redis.conf 最后一行配置redis密码，需要和docker-compose.yml 里一致

3、data目录为持久化数据目录，包括mysql数据目录，redis数据目录，及template模板路径

4、在宿主机上开启nfs，共享data/templates目录，给计算节点使用

* 这里用到了 `wait-for-it.sh` 等待mysql服务器启动完成才启动应用程序，项目地址为: https://github.com/vishnubob/wait-for-it
