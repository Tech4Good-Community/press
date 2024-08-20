# Press

This is "Press," a custom application built using Frappe, designed to manage and operate Frappe Cloud. This app is responsible for handling various aspects of the Frappe Cloud ecosystem, including infrastructure management, subscription services, marketplace functionalities, Software as a Service (SaaS) operations, and much more.

The other crucial component of the Frappe Cloud infrastructure is called "Agent." The Agent is a Flask-based application that runs on every server within a typical cluster. Its primary role is to execute tasks in response to HTTP requests. These tasks, known as "Agent Jobs," include creating new sites, installing apps, updating existing sites, setting up benches, and a wide range of other actions. Essentially, any operation you need to perform on Frappe Cloud is just a simple request away, with the Agent ensuring that the task is carried out seamlessly.

## Prerequisites
- Frappe Bench (https://github.com/frappe/bench)
- Docker
- Certbot with route53 plugin
- AWS account (for route53 & S3)
- Digital Ocean account (for [container registry](https://www.digitalocean.com/products/container-registry))

## Local Setup

```bash
sudo apt install fail2ban supervisor nginx -y

sudo apt install apt install certbot python3-certbot-nginx -y

# This is to check the auto-renew of the SSL certificate 
systemctl status certbot.timer

# install system pip if not already (usually not installed)
sudo apt install python3-pip
pip3 install certbot-dns-route53

#create a bench directory
bench init frappe-bench

#get press, payments application 

bench get-app press
bench get-app payments
#enable multitenancy 
bench config dns_multitenant on

#create a new site
bench new-site fc.local --admin-password <site-admin-password> --db-root-password <mariadb-root-password>

bench use fc.local

bench set-config -g developer_mode 1

bench --site fc.local add-to-hosts

bench --site fc.local install-app press



```
