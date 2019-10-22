# Installing NGINX using ansible

Install nginx using yum module and configuration is copied using template to /etc/nginx/conf.d/ directory.


## **nginx_install.yml**
````yml
---
- name: "To Deploy NGINX"
  hosts: all
  become: yes
  vars:
   domain: example.com
  tasks:

   - name: "Installing NGINX"
     apt:
             name: nginx
             state: present
             update_cache: yes


   - name: "Adding conf file"
     template:
             src: nginx_conf.tmpl
             dest: "/etc/nginx/conf.d/{{ domain }}.conf"

   - name: "Creating DocumentRoot"
     file:
             path: "/var/www/html/{{ domain }}"
             state: directory

   - name: "Removing Default.conf"
     file:
             path: /etc/nginx/site-enabled/default
             state: absent

   - name: "Adding Index.html"
     copy:
             content: "<h1> IT WORKED </h1>"
             dest: "/var/www/html/{{ domain }}/index.html"


   - name: "Restarting NGINX"
     service:
             name: nginx
             state: restarted

## Template - nginx_conf.tmpl
````
```
server {
    listen         80 default_server;
    server_name    example.com www.example.com;
    root           /var/www/example.com;
    index          index.html;

}
```


### NGINX Official Documentation.
 [NGINX] (https://www.linode.com/docs/web-servers/nginx/nginx-installation-and-basic-setup/)

