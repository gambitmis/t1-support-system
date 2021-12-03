# t1-support-system
setup system for tier-1 support

## STEP 1: Update Package and Upgrade
``` console 
ansible-playbook ansible/update-package.yaml
```

## STEP 2: Disable IPv6
``` console 
ansible-playbook ansible/disable-ipv6.yaml 
```

## STEP 3: Install Docker
``` console 
ansible-playbook ansible/disable-ipv6.yaml 
```

## STEP 4: Add Support User
### Password for new users
``` python
python3 -c 'import crypt,getpass;pw=getpass.getpass();print(crypt.crypt(pw) if (pw==getpass.getpass("Confirm: ")) else exit())'
```
example
``` console
Password: 
Confirm: 
$6$/1OFlW9yH1KHHiOm$pn2SfNgbF/rbblahjseab/p1Xb6Z29UZik.BUilZ.TLnp9yvl2HViB3fs8XdVteboeioss7o2A4g1IYxw.TFJ/
```
### update on ansible 


## container network policy 
``` console
docker network create operation --subnet=172.20.0.0/24
docker network create portal --subnet=172.20.1.0/29
docker network create workload --subnet=172.20.10.0/24
```
## install loki docker plugin
https://grafana.com/docs/loki/latest/clients/docker-driver/
https://grafana.com/docs/loki/latest/clients/docker-driver/configuration/
``` console
docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions
```
``` yaml
version: "3.7"
services:
  logger:
    image: grafana/grafana
    logging:
      driver: loki
      options:
        loki-url: "https://<user_id>:<password>@logs-prod-us-central1.grafana.net/loki/api/v1/push"
```

Verifying the Guacamole install
Once the Guacamole image is running, Guacamole should be accessible at http://HOSTNAME:8080/guacamole/, where HOSTNAME is the hostname or address of the machine hosting Docker, and you should a login screen. If using MySQL or PostgreSQL, the database initialization scripts will have created a default administrative user called "guacadmin" with the password "guacadmin". You should log in and change your password immediately. If using LDAP, you should be able to log in as any valid user within your LDAP directory.

If you cannot access Guacamole, or you do not see a login screen, check Docker's logs using the docker logs command to determine if something is wrong. Configuration parameters may have been given incorrectly, or the database may be improperly initialized: