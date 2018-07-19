# Nginx
- 文件目录
  `cd /etc/nginx`

- 操作
  + 查看状态
  `systemctl status nginx`
  + 开启
  `systemctl start nginx`
  + 停止
  `systemctl stop nginx`

- 反向代理配置
```js
	upstream home {
	    server 127.0.0.1:3000;
	    #server 127.0.0.1:8888;
	    keepalive 64;
	}

	server {
	    listen 80;
	    server_name api.hankc.cn;
	    location / {
	        proxy_set_header X-Real-IP $remote_addr;
	        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	        proxy_set_header Host  $http_host;
	        proxy_set_header X-Nginx-Proxy true;
	        proxy_set_header Connection "";
	        proxy_pass      http://home;
	    }

	}
```

- 代理映射
  + 主页 www.hankc.cn 3000
  + 京东 jd.hankc.cn 3001
  + 美团 mt.hankc.cn 3002

  + 游戏 
  + xxoo xxoo.hankc.cn 4001