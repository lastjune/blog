###log how to install wordpress in my vps
    
    sudo apt-get update
    sudo apt-get install nginx
    sudo apt-get install mysql-server
    sudo mysql_install_db
    sudo mysql_secure_installation
    sudo apt-get install php5-fpm php5-mysql
    sudo vim /et/php5/fpm/php.ini

find and change the following line:

    cgi.fix_pathinfo=0

restart 

    sudo service php5-fpm restart

config nginx to use php processor

    sudo vim /etc/nginx/sites-avaliable/default

edit it as follow:
	server {
		listen 80 default_server;
		listen [::]:80 default_server ipv6only=on;

		root /usr/share/nginx/html;
		index index.php index.html index.htm;

		server_name server_domain_name_or_IP;

		location / {
			try_files $uri $uri/ =404;
		}

		error_page 404 /404.html;
		error_page 500 502 503 504 /50x.html;
		location = /50x.html {
			root /usr/share/nginx/html;
		}

		location ~ \.php$ {
			try_files $uri =404;
			fastcgi_split_path_info ^(.+\.php)(/.+)$;
			fastcgi_pass unix:/var/run/php5-fpm.sock;
			fastcgi_index index.php;
			fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
			include fastcgi_params;
		}
	}

restart the nginx
	sudo service nginx restart
	sudo rm /usr/share/nginx/html/info.php

create a database and user for wordpress
	mysql -u root -p
	CREATE DATABASE wordpress;
	CREATE USER wordpressuser@localhost IDENTIFIED BY 'password';
	GRANT ALL PRIVILEGES ON wordpress.* TO wordpressuser@localhost;
	flush privileges;
	exit;
go get wordpress
	cd ~
	wget http://wordpress.org/latest.tar.gz
	tar xzvf latest.tar.gz
	sudo apt-get update
	sudo apt-get install php5-gd libssh2-php
configure wordpress

	cd ~/wordpress
	cp wp-config-sample.php wp-config.php
	vim wp-config.php
edit the config file as following:
	// ** MySQL settings - You can get this info from your web host ** //
	/** The name of the database for WordPress */
	define('DB_NAME', 'wordpress');

	/** MySQL database username */
	define('DB_USER', 'wordpressuser');

	/** MySQL database password */
	define('DB_PASSWORD', 'password');

setup document 
	sudo mkdir -p /var/www/html
	sudo rsync -avP ~/wordpress/ /var/www/html/
	cd /var/www/html
	sudo chown -R ubuntu:www-data /var/www/html/*
	mkdir wp-content/uploads
	sudo chown -R :www-data /var/www/html/wp-content/uploads
Modify Nginx Server Blocks
	sudo cp /etc/nginx/sites-available/default /etc/nginx/site-available/worpress
	sudo vim /etc/naginx/sites-available/wordpress
change as follow:
	server {
			listen 80 default_server;
			listen [::]:80 default_server ipv6only=on;

			root /var/www/html;
			index index.php index.html index.htm;

			server_name your_domain.com;

			location / {
					# try_files $uri $uri/ =404;
					try_files $uri $uri/ /index.php?q=$uri&$args;
			}

			error_page 404 /404.html;

			error_page 500 502 503 504 /50x.html;
			location = /50x.html {
					root /usr/share/nginx/html;
			}

			location ~ \.php$ {
					try_files $uri =404;
					fastcgi_split_path_info ^(.+\.php)(/.+)$;
					fastcgi_pass unix:/var/run/php5-fpm.sock;
					fastcgi_index index.php;
					include fastcgi_params;
			}
	}

link our new file to the sites-enabled:
	sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled/
	sudo rm /etc/nginx/sites-enabled/default
	sudo service nginx restart
	sudo service php5-fpm restart
