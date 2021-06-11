Create progect form git:

	$ symfony new guestbook --version=5.0
	$ cd guestbook
	then run
	$ symfony serve

Install dependencies:

	$ symfony composer req profiler --dev
	$ symfony composer req logger
	$ symfony composer req debug --dev
	$ symfony composer req maker --dev
	$ symfony composer req annotations
	$ symfony composer req orm
	$ symfony composer req twig
	$ symfony composer require twig/intl-extra
	$ symfony composer req validator
	$ symfony composer req security
	$ symfony composer req phpunit
	$ symfony composer require browser-kit --dev   --- for functional testing
	$ symfony composer req messenger
	$ symfony composer req mailer
	$ symfony composer req imagine/imagine

To see logs:

	$ symfony server:log 

To see every available commands for make:
	
	$ symfony console list make

Check environment variables:

	$ symfony var:export

Clear cache:

	$ ./bin/console cache:clear

Debug router:

	$ symfony console debug:router

// =============================================

Make controller:

	$ symfony console make:controller ConferenceController
	

// =============================================

Docker.
----------

	$ docker-compose build   --- for the first time
	$ docker-compose up      --- to run (can use -d flag for detach mode)
	$ docker-compose down	 --- to stop

	To see logs:
	$ docker-compose logs

To adminer
	
	In browser type:
		localhost:8085
			database    - MySQL
			server		- mysql8_container
			user		- root
			password 	- password

		localhost:

		!!!!!!!!! --- not good (do not save data after docker-compose down)
		localshot:8085
			database - PostgeSQL	
			server   - postgres_container
			user     - user
			password - password
		!!!!!!!!!!

Connect to docker database:

	$ sudo docker exec -it postgres_container psql -U user -W symfony_guestbook

// =============================================

Database.
-----------

1. Create database:
	Before create go to the .env file and put credentials, then run
	it will create database from .env

	$ php bin/console doctrine:database:create

2. Create entity (table):

	$ symfony console make:entity Conference
		- city , string , 255 , no ;
		- year , string , 4 , no ;
		- isInternational , boolean , no

	$ symfony console make:entity Comment
		- author , string , 255 , no
		- text , text , no
		- email , string , 255 , no
		- createdAt , datetime , no

	Create relation between conference and comment

	$ symfony console make:entity Conference
		- comments, OneToMany, Comment
		- photoFilename, string, 

4. Create migration:

	$ symfony console make:migration

5. Run migration:

	$ symfony console doctrine:migrations:migrate

// =============================================

Admin panel.
-------------

Install:

	$ symfony composer req admin
	then
	$ mkdir src/Controller/Admin
	$ symfony console make:admin:dashboard
	then check in the browser 
		127.0.0.1:8000/admin

// =============================================

Form.
--------

Create form:

	$ symfony console make:form CommentFormType Comment


// =============================================

Security.
----------

Create admin:

	$ symfony console make:user Admin

Encode passowrd:

	$ symfony console security:encode-password

Create admin to database after creation entity:
	
	??? --- not working
	$ symfony run mysql "INSERT INTO admin (id, username, roles, password) \
  VALUES (nextval('admin_id_seq'), 'admin', '[\"ROLE_ADMIN\"]', \
  '\$argon2id\$v=19\$m=65536,t=4,p=1\$wyBWIpmfOXTodG8xdoLbOg\$2+8aSWrMK3rTw58rE7ZHqSk838AFNOn/D+8VvtIl8uk')"

Add to database to the admin table:

	username   --- admin
	roles	   --- ["ROLE_ADMIN"]
	passowrd   --- $argon2id$v=19$m=65536,t=4,p=1$pstqjbXS+c/dPPGNGovDhQ$bW3pk1HB31V4d4WboxMYgkHrWRI/PTbAD7LSbI6cCtE 

To enter to admin:

	username --- admin
	passowrd --- 123

  $ symfony console make:auth
  	> 1 --- Login form authentication

// =============================================
// =============================================
// =============================================

16.1

Online
https://symfony.com/doc/current/the-fast-track/ru/14-form.html

Git whole project:
https://github.com/the-fast-track/book-5.0-1.git