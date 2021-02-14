# Docker WordPress Environment
## Differences from the main version

This configuration, unlike the `main` one, installs all WordPress files into the current directory instead of a volume in order to provide access to all files through the IDE for later debugging

## Description

This is a configured Docker environment for developing websites on WordPress (mostly plugins and themes).
Includes:
* Git
* Composer
* Yarn
* NodeJS
* XDebug
* MailHog (is an email-testing tool with a fake SMTP server underneath)

### Links

If the containers are running you can access them via the following links:

* Website - http://wordpress.local
* MailHog - http://mail.wordpress.local
* Adminer - http://db.wordpress.local
* Traefik - http://traefik.wordpress.local

## Installation
### Docker Setup

Install a current Docker version per instructions - https://docs.docker.com/install/linux/docker-ce/ubuntu/

Install docker-compose - https://docs.docker.com/compose/install/

Create Docker-Network:

```shell
docker network create proxy
```

`Note: If you get an error message:`

```shell
Error response from daemon: could not find an available, non-overlapping IPv4 address pool among the defaults to assign to the network
```

try the following command instead that uses a subnet most likely not in use on your system:

```shell
docker network create --subnet=10.100.0.0/16 --ip-range=10.100.0.0/24 proxy
```

### PHP Configuration

Configuration files for PHP are located in the folder `.docker/php/conf.d`.
You can change existing settings in the appropriate files or add new ones to the `./docker/php/conf.d/custom.ini` file.

Don't forget to restart the container to make the change take effect.

### MySQL Configuration

Configuration file for MySQL is location in the folder `.docker/mysql/conf.d/mysql.cnf`. You can add the settings you need to it.

Don't forget to restart the container to make the change take effect.

### Hosts Configuration

#### Linux

Add the following hosts to `/etc/hosts`:

```
127.0.0.1 wordpress.local
127.0.0.1 db.wordpress.local
127.0.0.1 mail.wordpress.local
127.0.0.1 traefik.wordpress.local
```

Command:

```shell
echo "127.0.0.1 wordpress.local db.wordpress.local mail.wordpress.local traefik.wordpress.local" | sudo tee -a /etc/hosts
```

#### Windows

Add the following hosts to `C:\Windows\System32\drivers\etc\hosts`:

```
127.0.0.1 wordpress.local
127.0.0.1 db.wordpress.local
127.0.0.1 mail.wordpress.local
127.0.0.1 traefik.wordpress.local
```

### Run

Start Containers:

```shell
docker-compose up -d
```

Stop Containers:

```shell
docker-compose down
```