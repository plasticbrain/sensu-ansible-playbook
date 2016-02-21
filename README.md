# Ansible Playbook to Install Sensu client

## Description
This playbook installs the Sensu client on an Ubuntu 14.04 host, and sets up CPU, disk, memory, HTTP, and MySQL checks.

Packages that are installed: 
 * ruby
 * ruby-dev
 * build-essential
 * python-mysqldb
 * libmysqlclient-dev

Sensu plugins that are installed: 
 * sensu-plugin
 * sensu-plugins-cpu-checks 
 * sensu-plugins-disk-checks
 * sensu-plugins-http
 * sensu-plugins-mysql

Misc:
 * To perform MySQL health/alive checks a new user is created, named `check`, with a randomly generated password and `SELECT` privileges on the `mysql` table. 

## Setup/Configuration
* Edit `sensu.yml` to include the correct `hosts`, `remote_user`, and any other parameters that need to be changed or added.
* Edit `hosts` to include your inventory
* Edit `vars.yml` to include all of the relevant info for your setup
* Add your RabbitMQ server's SSL cert and PEM key to `roles/sensu/files`. Update the paths and filenames in `vars.yml` if needed. By default, it looks for `cert.pem` and `key.pem`, and places them in `/etc/sensu/ssl` on the remote server.
* Edit `/roles/sensu/templates/client.json.j2` to match your needed Sensu client configuration.

## Usage
````
$ ansible-playbook -i hosts sensu.yml
````

Note: You will be prompted for the password for the remote host's MySQL root user
````
Enter MySQL root password (to create health check MySQL user): 
````