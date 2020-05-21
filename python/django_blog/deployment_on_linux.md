# Deployment on a Linux Server

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
sudo nano /etc/ssh/sshdconfig
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

## Webserver using Apache

### Apache and WSGI installation

We'll install and use apache (nginx later)

```bash
sudo apt-get install apache2
sudo apt-get install libapache2-mod-wsgi-py3
```

### Apache configuration

Now we'll configure our web server

```bash
cd /etc/apache2/sites-available
sudo cp 000-default.conf django_project.conf
sudo nano django_project.conf
```

```apache2
Alias /static /home/lifework/django_project/static
<Directory /home/lifework/django_project/static>
Require all granted
</Directory>

Alias /media /home/lifework/django_project/media
<Directory /home/lifework/django_project/media>
Require all granted
</Directory>

<Directory /home/lifework/django_project/django_project>
<Files wsgi.py>
Require all granted
</Files>
</Directory>

WSGIScriptAlias / /home/lifework/django_project/django_project/wsgi.py
WSGIDaemonProcess django_app python-path=/home/lifework/django_project python-home=/home/lifework/django_project/venv
WSGIProcessGroup django_app
```

Let's enable that site through apache

```bash
sudo a2ensite django_project
```

Right now we have to get apache access to our database.
Apache has to be able to read/write to this folder.

```bash
sudo chown :www-data django_project/db.sqlite3
sudo chmod 664 django_project/db.sqlite3
sudo chown :www-data django_project/
ls- la
```

Let's do the same for the media folder

```bash
sudo chown -R :www-data django_project/media/
sudo chmod -R 775 django_project/media/
```

A few final changes. Let's create a config.json to store our secret variables.

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

with open('/etc/config/django_project/config.json') as config_file:
  config = json.load(config_file)

SECRET_KEY = config["SECRET_KEY"]
...
EMAIL_HOST_USER = config["EMAIL_HOST_USER"]
EMAIL_HOST_PASSWORD = config["EMAIL_HOST_PASSWORD"]
```

At this point it should be fully deployed.
We delete the allow on 8000

```bash
sudo ufw delete allow 8000
```
