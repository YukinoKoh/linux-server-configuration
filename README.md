This is a Linux Server Configuration project.
The aim of this project is to configure [this project](https://github.com/YukinoKoh/fsnd-catalog) to Ubuntu Linux server with basic secure manner.

## INFO: IP address and related information
- IP address: 54.249.127.217
- SSH port: 2200 
- HTTP port: 80
- NTP port: 123

## Configuration process
#### Get server
1. Start a new Ubuntu Linux Server instance on [Amazon Lightsail](https://lightsail.aws.amazon.com)
- get public IP address at the Amazon console
#### Set basic 
2. Connect to the server, using SSH via browser (from Amazon website), or via own SSH client
3. Fill the secure crierias (Secure criterias)
4. Local time zone to UTC
- `sudo dpkg-reconfigure tzdata`
#### Deploy project
5. Install Apache to serve a Python project
- `sudo apt-get install apache2`: to install Apache
- `sudo apache2ctl restart`: to restart Apache
- Confirm it by visiting the IP address that the index is served from `var/www/html/index.html`.
6. Install PostgreSQL for database
- `sudo apt-get install postgresql`
7. Install git
- `sudo apt-get install git`
7. Deploy the project (Deploy the project) 
#### Check the configuration changes
8. Visit the public IP address from a browser.
9. To check error, visit `/var/log/apache2/error.log`

## Secure criterias
The Details are written in `Note-security.md` 
1. Change default SSH port 22 to 2200
2. Connect to the server via SSH
3. Set firewall
4. Manage installed packages
5. Manage user account for the server 

## deploy the project
The Details are written in `Note-deploy.md` 
1. Clone project under `/var/www/` 
2. Create `app.wsgi` to test Apache
3. Modify `app.wsgi` to test flask
4. Modify `app.wsgi` to serve the project
5. Install the related modules
6. Set up Postgresql
7. Modify the database path
8. Modify the Oauth path
9. Change file accessibility 
(Step 3 is only for test.)


## A list of third party resources
| Package name         | Object                                                |
|----------------------|-------------------------------------------------------|
| finger               | Disply user information                               |
| Apache2              | HTTP server                                           |
| postgresql           | postgreSQL                                            | 
| postgresql-contrib   |                                                       |
| git                  | version control with repository                       |
| python-pip           | module install                                        |
| flask                | python web app framework                              |
| python-sqlalchemy    | python database                                       |
| python-psycopg2      | database adapter                                      |
| oauth2client         | framework for 3rd party authorization (verification)  |
| requests 
| httplib2

## Links
- [](https://github.com/ghoshabhi/P5-Linux-Config)
- [Hari Vedam GitHub repository](https://github.com/harushimo/linux-server-configuration)
- [about psql drop user](https://stackoverflow.com/questions/3023583/postgresql-how-to-quickly-drop-a-user-with-existing-privileges)
- [psql user management](https://www.a2hosting.com/kb/developer-corner/postgresql/managing-postgresql-databases-and-users-from-the-command-line#Deleting-PostgreSQL-users)
