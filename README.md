# Installing NGINX using ansible

Install nginx using yum module and configuration is to copied using template to /etc/nginx/conf.d/ directory.


## nginx_conf.tmpl

server {
    listen         80 default_server;
    server_name    example.com www.example.com;
    root           /var/www/example.com;
    index          index.html;

}



### NGINX Official Documentation.
 [NGINX] (https://www.linode.com/docs/web-servers/nginx/nginx-installation-and-basic-setup/)



