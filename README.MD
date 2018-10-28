## 2018/09 BuRnCycL

Ansible Playbook for InfluxDB using self-signed certificates. Prerequisite for ansible-grafana.

## Prerequisites
Make sure the remote computer has the proper ansible ssh key in /root/.ssh/authorized_keys

Ubuntu
```
sudo apt-add-repository ppa:ansible/ansible
sudo apt-add-repository universe
sudo apt update
sudo apt install -y git ansible make python
```

## Generate SSL Public Private key
To get going, you'll need to generate influxdb.pem and store the private key in Ansible Vault. Opted to do this in lieu of pyopenssl.

```
openssl req -new -x509 -keyout influxdb.pem -out influxdb.pem -days 3650 -nodes
```

```
cat ./influxdb.pem
```

Include this in secrets.yml created below.

## Create secrets.yml

Reference secrets.yml.example

Now create a new file in the root directory for this project called secrets.yml
```
vi secrets.yml
```

Encrypt the secrets file with Ansible Vault
```
ansible-vault encrypt secrets.yml
```

## Modify inventory

Point this at the host you wish to deploy InfluxDB
```
vi ./inventory
``` 

## Modify group_vars (if needed).

```
vi ./group_vars/all
```

## Install/Configure InfluxDB

```
make
```

Or individual stages with:

```
make install
```

```
make configure
```


