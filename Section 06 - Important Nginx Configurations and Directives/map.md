### Step 1 - Setup  Nginx Configuration

```sh
cd /etc/nginx/conf.d

nano map.conf
```
```sh
map $http_user_agent $index_file {
    default          desktop.html;
    ~*iPhone         iphone.html;
    ~*Android        android.html;
}

server {
    listen       80;
    server_name  _;

    location / {
        proxy_pass http://13.63.170.3/$index_file;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

```sh
nginx -t

systemctl reload nginx
```
### Step 2 - Setup HTML Files
```sh
cd /usr/share/nginx/html

touch desktop.html iphone.html android.html

echo "This is Desktop Website" > desktop.html

echo "This is iPhone Website" > iphone.html

echo "This is Android Website" > android.html
```
### Step 3 - Testing

To test as an iPhone:
```sh
curl -H "User-Agent: iPhone" http://localhost
```
To test as an Android:
```sh
curl -H "User-Agent: Android" http://localhost
```
Test Without Mobile User Agent
```sh
curl  http://localhost
```

