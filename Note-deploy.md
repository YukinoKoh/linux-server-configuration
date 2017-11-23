# Deploy the project
This is a note to deploy a database project to the ubuntu linux server
1. Set time zone to local UTC
2. Install basics to deploy the project
3. Clone the project from git repository
4. Test Apache (create `app.wsgi`)
5. Serve the project (modify `app.wsgi`)
6. Install the related modules
7. Set up Postgresql
8. Modify the database path
9. Modify the Oauth path
10. Change file accessibility 

# 1. Set time zone to local UTC
1. `sudo dpkg-reconfigure tzdata`
2. Select city accordingly

# 2. Install basics to the deploy project
1. Install Apache to serve a Python project
- `sudo apt-get install apache2`: to install Apache
- `sudo apache2ctl restart`: to restart Apache
- Confirm it by visiting the IP address that the index is served from `var/www/html/index.html`.
2. Install PostgreSQL for database
- `sudo apt-get install postgresql`
3. Install git
- `sudo apt-get install git`

# 3. Clone the project from git repository
1. Clone the project to `/var/www/`
2. Check if it's been cloned
```
ls /var/www/
>> sfnd-catalog html
```

# 4. Test Apache
#### Test 'hello world' app
1. Create `app.wsgi` under `/var/www/sfnd-catalog`
```
def application(environ, start_response):
    status = '200 OK'
    output = 'Hello world!'

    response_headers = [('Content-type', 'text/plain'), ('Content-Length', str(len(output)))]
    start_response(status, response_headers)

    return [output]
```
2. Overrwite the configuratrion file `/etc/apache2/sites-enabled/000-default.conf`
```
WSGIScriptAlias / /var/www/fsnd-catalog/app.wsgi
</VirtualHost>
``` 
3. `sudo apache2ctl restart`: to restart

#### Test flask app
1. Modify `app.wsgi` with `sample.py`
```
mport sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/fsnd-catalog")

from sample import app as application
application.secret_key = 'your_secret_key'
```
2. Install related modules
```
sudo apt-get install python-flask
```
3. `sudo apache2ctl restart`: to restart

# 5. Serve the project
Modify `app.wsgi` to import app from `project.py`
```
from project import app as application
```  

# 6. Install the related modules
```
sudo apt-get install python-pip python-flask python-sqlalchemy python-psycopg2
sudo pip install [MODULES]
```

# 7. Set up Postgresql
Create psql database and user for the project
1. Switch (log in) to sql user: `sudo -i -u postgres` (to log out: `exit)`
2. start psql: `psql` (to quit: `\q`)
3. Create psql user `catalog` with password `catalog` with login and createdb permission
```
CREATE USER catalog WITH PASSWORD 'catalog';
ALTER USER catalog CREATEDB;
```
4. Create dabtabase for the project
```
CREATE DATABASE researchoption WITH OWNER catalog;
```
5. Limit public access to the user `catalog` 
```
REVOKE ALL ON SCHEMA public FROM public;
GRANT ALL ON SCHEMA public TO catalog;
```
6. Exit Postgresql
- `\q` to quit `psql` mode 
- `exit` to exit Postgres

#### psql command lines
- `\q`: to quit
- `PSQL database_name`: access the database
- `\l`: list of database
- `\du`: list of database users
- `\d`: to check the table ownership
- `REVOKE connect ON DATABASE database_name FROM PUBLIC;`: remove public access
- `GRANT connect ON DATABASE database_name TO rolename;`: give the user the psrmission to access the specified db
- `CREATEDB database_name`: create database
- `DROP DATABASE daabase_name`: drop database
- `ALTER DATABASE database_name OWNER TO rolename;`: alter database owner
- `CRAETE ROLE rolename WITH LOGIN`: create the user with access permission
- `DROP OWNED BY rolename`: delete the object depend on the user
- `DROP USER rolename`: delete the user
- `\PASSWORD rolename`: add password to the user 
- `ALTER ROLE rolename WITH LOGIN;`: give access permission to the user
- `ALTER USER rolename PASSWORD 'new password';`: change passowrd
#### psql related links
- [About user and role in Postres](https://stackoverflow.com/questions/27709456/what-is-the-difference-between-a-user-and-a-role)
- [About psql drop user](https://stackoverflow.com/questions/3023583/postgresql-how-to-quickly-drop-a-user-with-existing-privileges)
- [psql commands](https://www.a2hosting.com/kb/developer-corner/postgresql/managing-postgresql-databases-and-users-from-the-command-line#Deleting-PostgreSQL-users)


# 8. Modify the database path
1. Change the database path in `database_setup.py`, `initial_data.py`, and `common.py`
```
engine = create_engine('postgresql://catalog:catalog@localhost/researchoption')
```
The basic syntax is `postgresql://username:password@host:port/database`

2. Run `sudo python database_setup.py` and `sudo python initial_data.py` 


# 9. Modify Oauth path 
1. Change the oauth related json path to `/var/www/fsnd-catalog/fb_client.json` in `common.py`
2. Change target site url to public IP at [Facebook developer site](https://developers.facebook.com/docs/facebook-login/web) 

# 10. Limit file accessibility 
Change unnecessary file to serve the app unaccessable
- `.git`, `researchoption.db`, `database_setup.py`, `initial_data.py`, `sample.py`, `README.md`, `.vagrant`, `Vagrantfile`, `.DS_Store`, and `*.pyc`
```
sudo chmod 700 [file name]
```
- owner: read / write / execute
- group:
- all:

