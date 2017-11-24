This is a Linux Server Configuration project of Full stack nano degree.
The aim of this project is to configure [this project](https://github.com/YukinoKoh/fsnd-catalog) to Ubuntu Linux server with basic secure manner.

# IP address and related information
- hosted address: [54.249.127.217](http://54.249.127.217/)
- SSH port: 2200 
- HTTP port: 80
- NTP port: 123

# Configuration process
### Get server
1. Start a new Ubuntu Linux Server instance on [Amazon Lightsail](https://lightsail.aws.amazon.com)
2. Connect to the server, using SSH via browser (from Amazon website), or via own SSH client
### Set basic security 
The Details are written in [Note-security.md](Note-security.md) 
1. Change default SSH port
2. Connect to the server with SSH key
3. Set firewall
4. Update packages
5. Manage user account for the server 
### Deploy the project
The Details are written in [Note-deploy.md](Note-deploy.md) 
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
### Check the configuration changes
1. Visit the public IP address from a browser.
2. To check error, visit `/var/log/apache2/error.log`


# A list of third party resources
| Package name         | Object                          |
|----------------------|---------------------------------|
| finger               | Disply user information         |
| Apache2              | HTTP server                     |
| postgresql           | PostgreSQL                      | 
| git                  | Version control                 |
| python-pip           | Module installer                |
| flask                | Python web app framework        |
| python-sqlalchemy    | Python database                 |
| python-psycopg2      | Python database adapter         |
| httplib2             | HTTP client library for Python  |
| json                 | Json helper for Python          |

# Links
- [Ubuntu package](https://packages.ubuntu.com/)
- [ufw](https://help.ubuntu.com/lts/serverguide/firewall.html#firewall-ufw)
- [ssh persmissions are too open](https://stackoverflow.com/questions/9270734/ssh-permissions-are-too-open-error)
- [about psql drop user](https://stackoverflow.com/questions/3023583/postgresql-how-to-quickly-drop-a-user-with-existing-privileges)
- [psql user management](https://www.a2hosting.com/kb/developer-corner/postgresql/managing-postgresql-databases-and-users-from-the-command-line#Deleting-PostgreSQL-users)
