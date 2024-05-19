# netdevops-lab

Welcome to my home lab that allows me to test new stuff/tools/services, and integrate them in a devops way. All this is done on my free time, so can be pretty low pace :)

I'll try to document as much in here, if I don't forget to !

## Prerequesite

### General

* Having Docker installed on your VM. Tested against Docker Engine `v26.1.0` (both server and client)
* Having Docker Compose installed. Tested against Docker Compose version `v2.26.1`
* Access to internet from VM

### Semaphore UI

* If you already have your own `bolt` database, please store it on your local VM in _semaphore/database_, with name `database.boltdb`
> Remember to set the rights accordingly for semaphore to access your database. If in doubt :
```bash
chmod 777 semaphore/database/database.boltdb
```

## Getting started

Here are the few commands you'll need to get started with the project on your VM.

>Remember to change passwords below !

```bash
cat <<EOT >> ~/.bashrc
# NetDevOps Lab Env Variables
export SEMAPHORE_ADMIN_PASSWORD=password
export AIRFLOW_DB_PASSWORD=password
EOT
docker compose pull
docker compose up
```

`SEMAPHORE_ADMIN_PASSWORD` will define the password of your account in Semaphore UI.

`AIRFLOW_DB_PASSWORD` will define DB password for some services. See _env_ folder for more details.

## What am I actually deploying ?

### Ansible Container

Built from `mathieued/ansible_base:latest` image, that inherits from a `python:3`image, this container will be the one to execute the ansible playbooks in your netdevops platform.

See `ansible_base/Dockerfile` for more details.


### Airflow

Airflow is used here as an advanced scheduler. It implements DAGs to create workflows. COmes handy for scheduled tasks that I need to execute regularly.

Airflow needs :
* a webserver to host the UI
* a worker to execute tasks
* a scheduler

That's why you'll see 3 containers regarding Airflow.

### Semaphore UI

Semaphore is an UI that allows you to ease running of ansible playbooks. It is a light and open-source alternative to Ansible Tower. However, it isn't such advanced as Tower or AWX.