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


# docker-compose  
webサーバー、DBサーバー、キャッシュサーバーなど定義を一つのymlファイルに記述しておくことで、そのymlファイルを基にアプリケーションに必要なコンテナをまとめて起動できる  

#### ymlとは  
構造化されたデータを表現するためのフォーマット。直感的に書かれているのでファイルを見れば構造は大体理解できる。  
##### Compose実行ステップ  
1. Dockerfileを用意するか、使用するイメージをDocker Hubなどに用意する  
2. docker-compose.ymlを定義する  
3. docker-compose upを実行する  
