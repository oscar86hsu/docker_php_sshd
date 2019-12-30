# docker_php_sshd
Dockerized PHP with SSH service and Apache, built on top of [official PHP](https://hub.docker.com/_/php/) images.

## Image tags

- oscar86hsu/php:7.2-apache

## Installed packages

Base:

- [PHP 7.2](https://www.php.net/archive/2019.php#2019-12-18-3)

Package:

- [openssh-server](https://packages.debian.org/zh-tw/jessie/openssh-server)

Default Config:

- `PermitRootLogin yes`
- `PasswordAuthentication yes`
- exposed port 22
- default command: `/usr/sbin/sshd -D`
- root password: `root`

## Getting Started
`docker run -d -p 2222:22 --name php_sshd oscar86hsu/php_sshd:latest`<br>
`ssh root@localhost -p2222`

## Security

Using the image with the default password is dangerous. You should change your password after creating the container.<br>
- To change password, use the following command:
`docker exec -ti php_sshd passwd`

- To not use password and use key instead:<br>
```
docker exec php_sshd passwd -d root
docker exec php_sshd sed -i 's/.*PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
ssh-keygen -t rsa -f ./id_rsa -N ""
docker cp id_rsa.pub php_sshd:/root/.ssh/authorized_keys
docker exec php_sshd chown root:root /root/.ssh/authorized_keys
```

## Useful Links
- [ssh-keygen](https://www.ssh.com/ssh/keygen/)
- [Docker Document](https://docs.docker.com/)


