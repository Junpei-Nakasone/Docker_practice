# Docker_memo  

`docker run --name コンテナ名 -d \  
-p ホストのポート番号:コンテナのポート番号 \
イメージ名`  

#### --name  



#### nginxでhttpメソッド制限するには  
起動中のnginxのdefault.confをコピーして取得  
`docker cp tmp-nginx:etc/nginx/conf.d/default.conf ./`  

ローカルのディレクトリでdefault.confの設定を変更  
`  location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
        limit_except POST {
        deny all;
}`  

 
default.conf をコピーするDockerfileを作成
`FROM nginx:latest
COPY default.conf /etc/nginx/conf.d/default.conf`  
  
  
イメージをbuild  
`docker build -t nginx:ver1 .`  

作成したイメージからコンテナを実行  
`docker run --name web -p 8080:80 --rm nginx:ver1`



