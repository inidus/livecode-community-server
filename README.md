# LiveCode Community Server - Dockerised!

LiveCode is a scripting language maintained by [LiveCode Ltd](http://www.livecode.com/).

This repo provides LiveCode Community Server running as a Docker multi-container application. Also provided is a Vagrant environment to run the containers.

- livecode-centos7-httpd
  - LiveCode Community Server running as a CGI handler within an Apache web server environment on Centos 7.
- maria-db
  - Official build of MariaDB, the community-developed fork of MySQL.
- nginx
  - Official build of Nginx.
- nginx-filebeat
  - Example showing shipping Nginx logs to ELK with Filebeat

## Getting Started
These instructions will get you a LiveCode Community Server environment up and running on your local machine for development and testing purposes.

### Prerequisites

Required: [Docker](https://www.docker.com/) & [Docker Compose](https://docs.docker.com/compose/)

Optional: [Vagrant](https://www.vagrantup.com/)

### Run with Docker

Clone the repository `git clone` and change into the directory

Add your LiveCode to the folder `user-data/html`

Add your database .sql (if required) to the folder `user-data/mariadb/db-src`

Build the containers `docker-compose build`

Start the application `docker-compose -f docker-compose.yml up`

Open [http://127.0.0.1](http://127.0.0.1) in your browser


### Run in Vagrant environment

Clone the repository `git clone` and change into the directory

Add your LiveCode to the folder `user-data/html`

Add your database .sql (if required) to the folder `user-data/mariadb/db-src`

Start the Vagrant box `vagrant up`

Open [http://192.168.50.100](http://192.168.50.100) in your browser. Vagrant will also create a hosts entry for livecode.local (subject to plugin compatability) so [http://livecode.local](http://livecode.local) should also work in your browser.

## Container settings

### MariaDB
Configure the MariaDB container by modifying the `docker-compose.yml` / `docker-compose-vagrant.yml` files.

```
MYSQL_ROOT_PASSWORD: livecode
MYSQL_USER: livecodeuser
MYSQL_PASSWORD: livecode
MYSQL_DATABASE: livecode
```

#### Initialisation

The directory `./user-data/mariadb/db-src` is used for `/docker-entrypoint-initdb.d`

Place MairaDB/MySQL dump/create files with the suffix .sql in `./user-data/mariadb/db-src` for automagical execution on container initialisation.

#### Persistence

The volume db-data is defined and mounted at `/var/lib/mysql`

## Contributing

Please read [CONTRIBUTING](CONTRIBUTING) for details on our code of conduct, and the process for submitting pull requests to us.

## Authors

* [Rob Dyke](https://github.com/robdyke) for Inidus Ltd

See also the list of contributors and acknowledgments below.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

## Acknowledgments

* [DevBandit](https://github.com/DevBandit)'s blog about [vagrant-and-docker](http://devbandit.com/2015/05/29/vagrant-and-docker.html).
* [Techstrategies](https://github.com/techstrategies/) for [docker-livecode](https://github.com/techstrategies/docker-livecode)
* [leighmcculloch](https://github.com/leighmcculloch) for  [vagrant-docker-compose](https://github.com/leighmcculloch/vagrant-docker-compose).
* [devopsgroup-io](https://github.com/devopsgroup-io) for  [vagrant-hostmanager](https://github.com/devopsgroup-io/vagrant-hostmanager).
