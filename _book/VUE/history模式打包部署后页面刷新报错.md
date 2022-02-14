### history模式打包部署后页面刷新报错

#### nginx设置

```
upstream api {
    server 127.0.0.1:8080;
}

server {
    listen 80;
    server_name example.org;

    location / {
        root   /data/;
        index  index.html index.htm;
        add_header Cache-Control no-cache;
        add_header Pragma no-cache;
        add_header Expires 0;
        client_max_body_size  500m;
        try_files $uri $uri/ /index.html;此句解决问题
    }

    location = /50x.html {
        root   /data/dist/;
    }

}

server {
    listen 59001;
    server_name example.org;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        #proxy_http_version 1.1;
        #proxy_set_header Upgrade $http_upgrade;
        #proxy_set_header Connection "Upgrade";
    }


}
```

