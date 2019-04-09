### nginx反向代理

【nginx配置】
```
进入配置：cd /usr/local/etc/nginx
vim配置： vim nginx.conf
```
【nginx启动】
```
进入：cd /usr/local/Cellar/nginx/1.12.1/bin/
启动：nginx 
刷新： nginx -s reload
```
【nginx授权】
```
// cat /etc/group|grep apple
cd /usr/local/var/run/nginx
ls -al
授予权限：sudo chmod -R 777 proxy_temp/
```
