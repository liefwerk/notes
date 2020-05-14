# Installation and setup of Django

## Installation on a linux subsystem (Ubuntu)

The first step is to create a directory, link it with a git repository and check if django is installed.
I'll be using python3 for this project.

`django-admin --version`

If that doesn't work, I found that the following command works well.

`sudo apt-get install python-django`

Then using a django-admin command line, we'll initiate a project.
It is important to already be in the root folder of your git repository.

`django-admin startproject nom_du_projet`
