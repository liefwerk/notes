# Deployment on a Linux Server

Let's learn how to deploy our django project into a linux server.
We'll be using a Debian 9, NGINX and Gunicorn.

## SSH key based authorization

Let's setup ssh key-based auth.
We are logged in as our main user in the home directory.

```bash
mkdir -p ~/.ssh
ls -la
```

In our local computer we'll create a new ssh key (or use an existing one)

```bash
ssh-keygen -b 4096
```

Then from the local computer we'll send it through scp

```bash
sudo scp ~/.ssh/id_rsa.pub user@IP_ADDRESS:~/.ssh/authorized_keys
```

Now we go back to our server.

```bash
sudo chmod 700 ~/.ssh/
sudo chmod 600 ~/.ssh/*
```

## More setup to secure the server

### Deativating the password login

We can also deactivate connection with a password.

```bash
sudo nano /etc/ssh/sshd_config
```

In this file we'll change the PermitRootLogin

```bash
PermitRootLogin no
...
PasswordAuthentication no
```

We then have to restart the ssh service

```bash
sudo systemctl restart sshd
```

### Setting up a Firewall

Last thing is to setup a firewall

```bash
sudo apt-get install ufw
```

A few basic rules

```bash
sudo ufw default allow outgoing
sudo ufw default deny incoming
sudo ufw allow ssh
sudo ufw allow 8000
```

To enabled them:

```bash
sudo ufw enable
sudo ufw status
```

To delete an existing rules

```bash
sudo ufw delete allow 8000
```

## Put our web app on the web server

If we are using a virtual env, we can load a requirements.txt file in our project

```bash
source path/env/bin/activate
```

That will show `(django_env)` at the top of our terminal.
Now we load the requirements in the file

```bash
pip freeze
pip freeze > requirements.txt
```

We can now put this file into our `django_project`

To put our app to our server, we'll use scp
We first naviguate to our project folder

```bash
scp -r django_project user@IP_ADDRESS:~/
```

## Setup the Virtual Environnement

In our server terminal:

```bash
sudo apt-get install python3-pip
sudo apt-get install python3-venv
```

To create a virtual environnement we simply do these commands

```bash
python3.6 -m venv django_project/venv
ls django_project/
```

To activate it

```bash
cd django_project/
source venv/bin/activate
```

Now let's install all the requirements of our txt file

```bash
pip install -r requirements.txt
```

Then we'll modify some settings in the `settings.py` file

```bash
ALLOW_HOSTS = ['IP_ADDRESS']
...
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
STATIC_URL = '/static/'
```

Now to get our static file working, we'll run a command

```bash
python manage.py collectstatic
```

Now let's run our dev server and access it from the outside.

```bash
python manage.py runserver 0.0.0.0:8000
```

Now we test our site, but we won't be running this with the django server?
Let's kill that server with `ctrl+c` and run a reliable server.

### A few changes

A few changes in our project first.
Let's create a config.json to store our secret variables.

```bash
sudo touch /etc/django_project/config.json
sudo nano /etc/django_project/config.json
```

In these we'll create a JSON array and put our secret variables

```json
{
  "SECRET_KEY": "SECRET_KEY",
  "EMAIL_HOST_USER": "EMAIL_HOST_USER",
  "EMAIL_HOST_PASSWORD": "EMAIL_HOST_PASSWORD"
}
```

Then in secrets.py, we'll import the json file

```py
import json

with open('/etc/django_project/config.json') as config_file:
  config = json.load(config_file)

SECRET_KEY = config["SECRET_KEY"]
...
EMAIL_HOST_USER = config["EMAIL_HOST_USER"]
EMAIL_HOST_PASSWORD = config["EMAIL_HOST_PASSWORD"]
```

## Creating a database

### Installing PostgreSQL

```bash
sudo apt install postgresql postgresql-contrib
```

Let's check that everything is well installed with these commands

```bash
sudo -u postgres psql -c "SELECT version();"
sudo systemctl status postgresql
```

To switch user and access PostgreSQL we run that command

```bash
sudo su - postgres
```

### Database Setup

#### Creating the database

Let's create a db using PostgreSQL.

```bash
sudo su - postgres
createdb mydb
```

#### Creating the user

Now we create the DB user this way

```bash
createuser -P username
```

#### Giving privileges to the user

```bash
psql
GRANT ALL PRIVILEGES ON DATABASE django_db TO user;
```

## Webserver using NGINX and Gunicorn

### Setup of NGINX

This is assuming we already have nginx installed and we launched our virtual environment.

```bash
sudo nano /etc/nginx/sites-available/myproject
```

Now let's enter these lines into the editor

```nginx
server {
    server_name IP_ADDRESS;

    access_log off;

    location /static/ {
        alias /home/user/django_project/static/;
    }

    location /static/ {
        alias /home/user/django_project/media/;
    }

    location / {
        proxy_pass http://127.0.0.1:8001;
        proxy_set_header X-Forwarded-Host $server_name;
        proxy_set_header X-Real-IP $remote_addr;
        add_header P3P 'CP="ALL DSP COR PSAa PSDa OUR NOR ONL UNI COM NAV"';
    }
}
```

Then we'll set up a symbolic link in sites-enabled direectory so NGINX knows it's activated

```nginx
cd /etc/nginx/sites-enabled
sudo ln -s ../sites-available/myproject
```

We'll restart nginx

```nginx
sudo service nginx restart
```

Eventually, we can checl if there are som error with this command

```nginx
systemctl status nginx.service
```

### Setup of Gunicorn

## Webserver using Apache

```bash
source /home/user/django_project/venv/bin/activate
```

Once the cirtualenv in active we install Gunicorn

```bash
pip install gunicorn
```

And we can finally bind requets for the domain or ip to port 8001 that we selected
From the same directory as manage.py, we'll run that command

```bash
gunicorn django_project.wsgi:application
```
