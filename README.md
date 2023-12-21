1.进入manager目录，启动env方法：
     ./env/env.sh
如果打印 3 个 container已经存在，可以先docker rm -f 那3个container
再重新执行env.sh.

2. 然后启动site:
   ./bin/site daemon -c /home/lphilip/go/src/dops-git106.fortinet-us.com/fortiot/daemon/manager/builds/config/site/config.json
此时数据库表会添加到docker中  ot_postgres中

docker exec -it ot_postgres sh
可进入docker操作数据库

psql -U test -h localhost -d testdb

3.查看数据库表创建情况：

SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public';

4. 建立ssh tunnul映射8080端口，这样可以通过笔记本postman访问http server

ssh -L 8080:localhost:8080 lphilip@172.19.152.135

先auth login获取session id， session id会自动载入到其他请求中，
之后就可以进行其他api的调用了。
