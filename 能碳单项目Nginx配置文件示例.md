```sh
# 能碳项目

server{
  listen  28080;
  server_name  125.124.133.230;
  
  location / {
    root /carbon/workspace/kawasaki/admin-web/dist;
    index index.html index.htm;
    try_files $uri $uri/ /index.html;
  }

  location /oss/ {
    alias /carbon/data/jenkins/workspace/kawasaki-oss/;
    try_files $uri $uri/ =404;
  }

  location /prod-api/ {
    proxy_set_header Host $http_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header REMOTE-HOST $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_pass http://127.0.0.1:28082/;
  }

  location /report/ {
    proxy_set_header Host $http_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header REMOTE-HOST $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_pass http://127.0.0.1:28083/;
  }

  location  /ship/ {
    proxy_set_header Host $http_host;          
    proxy_set_header X-Real-IP $remote_addr;              
    proxy_set_header REMOTE-HOST $remote_addr;             
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;            
    proxy_pass http://127.0.0.1:28084/;                      
  }

  location  /device/ {      
    proxy_set_header Host $http_host;           
    proxy_set_header X-Real-IP $remote_addr;            
    proxy_set_header REMOTE-HOST $remote_addr;            
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_pass http://127.0.0.1:28085/;                     
 }

  location /upload/ {
    root /usr/local/upload;
    index index.html index.htm;
    try_files $uri $uri/ /index.html;  
  }

}
```

