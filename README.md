1. リポジトリをクローンする  
git clone <リポジトリ名>  

2. 生成されたディレクトリに移動する  
cd laravel-app  

3. phpディレクトリのdocker imageの作成  
docker image build -t <任意の名前> ./docker/php  

4. phpコンテナの起動  
docker run --name <任意の名前> -v <srcディレクトリのパス>:var/www/src -d <作成したphpのDockerimage>  

5. phpコンテナの中に入ってIPアドレスを調べる  
docker exec -it <phpコンテナ名> bash  
hostname -i  
exit  

6. nginxディレクトリのdefault.confの下記の記述を先ほど調べたIPアドレスに書き換え  
fastcgi_pass 172.17.0.3:9000;  

7. nginxディレクトリのdocker imageを作成  
docker image build -t <任意の名前> ./docker/nginx  

8. nginxコンテナの起動  
docker run --name <任意の名前> -v <srcディレクトリのパス>:var/www/src -p 80:80 -d <作成したnginxのdocker image>  

7. mysqlディレクトリのdocker imageを作成  
docker image build -t <任意の名前> ./docker/db  

8. mysqlコンテナの起動  
docker run --name <任意の名前> -d -p 3306:3306 <作成したmysqlのdocker image>  

9. mysqlコンテナの中に入りIPアドレスを調べる  
docker exec -it <mysqlコンテナ> bash
hostname -i  
exit  

10. phpコンテナに入ってlaravelの.envを編集する
docker exec -it <phpコンテナ> bash  
cd laravel-app  
vi .env  
DB_CONNECTION=mysql  
DB_HOST=<mysqlコンテナのIPアドレス>  
DB_PORT=3306  
DB_DATABASE=sample  
DB_USERNAME=user  
DB_PASSWORD=password123  

11. laravelとmysqlの接続を確認する  
php artisan migrate  
exit  
