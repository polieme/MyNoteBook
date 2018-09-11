> <font color='red'><b>其他组件的安装方式基本一样，比如说tomcat、php、mongodb、mysql等等，因此这里只列举了nginx的安装方式</b></font>

# Docker 安装Nginx
## 方法一、docker pull nginx(推荐)
查找docker hub上的nginx镜像
```
C:\Users\zp>docker search nginx
NAME                                                   DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                                                  Official build of Nginx.                        9300                [OK]
jwilder/nginx-proxy                                    Automated Nginx reverse proxy for docker con…   1384                                    [OK]
richarvey/nginx-php-fpm                                Container running Nginx + PHP-FPM capable of…   610                                     [OK]
jrcs/letsencrypt-nginx-proxy-companion                 LetsEncrypt container to use with nginx as p…   394                                     [OK]
kong                                                   Open-source Microservice & API Management la…   215                 [OK]
webdevops/php-nginx                                    Nginx with PHP-FPM                              111                                     [OK]
kitematic/hello-world-nginx                            A light-weight nginx container that demonstr…   108
zabbix/zabbix-web-nginx-mysql                          Zabbix frontend based on Nginx web-server wi…   62                                      [OK]
bitnami/nginx                                          Bitnami nginx Docker Image                      57                                      [OK]
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5   ubuntu-16-nginx-php-phpmyadmin-mysql-5          43                                      [OK]
linuxserver/nginx                                      An Nginx container, brought to you by LinuxS…   38
tobi312/rpi-nginx                                      NGINX on Raspberry Pi / armhf                   20                                      [OK]
blacklabelops/nginx                                    Dockerized Nginx Reverse Proxy Server.          12                                      [OK]
nginxdemos/nginx-ingress                               NGINX Ingress Controller for Kubernetes . Th…   11
wodby/drupal-nginx                                     Nginx for Drupal container image                10                                      [OK]
webdevops/nginx                                        Nginx container                                 8                                       [OK]
nginxdemos/hello                                       NGINX webserver that serves a simple page co…   8                                       [OK]
centos/nginx-18-centos7                                Platform for running nginx 1.8 or building n…   7
1science/nginx                                         Nginx Docker images that include Consul Temp…   4                                       [OK]
centos/nginx-112-centos7                               Platform for running nginx 1.12 or building …   4
pebbletech/nginx-proxy                                 nginx-proxy sets up a container running ngin…   2                                       [OK]
travix/nginx                                           NGinx reverse proxy                             1                                       [OK]
toccoag/openshift-nginx                                Nginx reverse proxy for Nice running on same…   1                                       [OK]
ansibleplaybookbundle/nginx-apb                        An APB to deploy NGINX                          0                                       [OK]
mailu/nginx                                            Mailu nginx frontend                            0                                       [OK]
```

这里我们拉取官方的镜像
```
C:\Users\zp>docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
be8881be8156: Pull complete
32d9726baeef: Pull complete
87e5e6f71297: Pull complete
Digest: sha256:d85914d547a6c92faa39ce7058bd7529baacab7e0cd4255442b04577c4d1f424
Status: Downloaded newer image for nginx:latest
```

等待下载完成后，我们就可以在本地镜像列表中查找REPOSITORY为nginx的镜像
```powershell
C:\Users\zp>docker images nginx
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              c82521676580        3 weeks ago         109MB

C:\Users\zp>
```