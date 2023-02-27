# rocky-sshd
Star this repository if it is useful for you.  
[![Docker Stars](https://img.shields.io/docker/stars/takeyamajp/rocky-sshd.svg)](https://hub.docker.com/r/takeyamajp/rocky-sshd/)
[![Docker Pulls](https://img.shields.io/docker/pulls/takeyamajp/rocky-sshd.svg)](https://hub.docker.com/r/takeyamajp/rocky-sshd/)
[![license](https://img.shields.io/github/license/takeyamajp/docker-rocky-sshd.svg)](https://github.com/takeyamajp/docker-rocky-sshd/blob/master/LICENSE)

## Supported tags and respective Dockerfile links  
- [`latest`, `rocky9`](https://github.com/takeyamajp/docker-rocky-sshd/blob/master/rocky9/Dockerfile)
- [`rocky8`](https://github.com/takeyamajp/docker-rocky-sshd/blob/master/rocky8/Dockerfile)

 ### Supported architectures: ([`more info`](https://github.com/docker-library/official-images#architectures-other-than-amd64))  
 `amd64`, `arm64(for Raspberry Pi)`

## Image summary
    FROM rockylinux:9  
    MAINTAINER "Hiroki Takeyama"
    
    ENV TIMEZONE Asia/Tokyo
    
    ENV ROOT_PASSWORD root
    
    EXPOSE 22

## How to use
This container can be accessed by SSH and SFTP clients.

    docker run -d --name rocky-sshd \  
           -e TIMEZONE=Asia/Tokyo \  
           -e ROOT_PASSWORD=root \  
           -p 8022:22 \  
           takeyamajp/rocky-sshd

You can add extra ports and volumes as follows if you want.

    docker run -d --name rocky-sshd \  
           -e TIMEZONE=Asia/Tokyo \  
           -e ROOT_PASSWORD=root \  
           -p 8022:22 \  
           -p 8080:80 \  
           -v /my/own/datadir:/var/www/html \  
           takeyamajp/rocky-sshd

SCP command can be used for transferring files.

    scp -P 8022 -r /my/own/httpd.conf root@localhost:/etc/httpd/conf/httpd.conf

## Time zone
You can use any time zone such as America/Chicago that can be used in Rocky Linux.  

See below for zones.  
https://www.unicode.org/cldr/charts/latest/verify/zones/en.html

## Logging
This container logs the beginning, authentication, and termination of each connection.  
Use the following command to view the logs in real time.

    docker logs -f rocky-sshd
