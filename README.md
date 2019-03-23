# Ando

Ando (Ansible + Docker) uses Ansible to provide from a control machine a Docker container on a virtual machine.

In this case, the NCC RPKI-Validator of RIPE is provisioned in a Docker container.

## Requeriments 

The previous requirements to run the repository are:

#### On the control machine
* Run Debian 9 (used as example reference) or any Linux
* Install ansible

```sh
$ sudo apt install python-pip
$ sudo pip install ansible
```
* Generate public and private keys for the user ssh

```sh
$ ssh-keygen -t rsa
```
* Copy the ssh public key on the virtual machine

```sh  
$ ssh-copy-id -i id_rsa.pub <USUARIO>@virtual_machine
```

#### On the virtual machine (Ansible managed node)
* Give super user execution permissions by adding it to the sudo group

```
# adduser <USUARIO> sudo
``` 
## Run

Install git to be able to clone the repository

```sh
$ sudo apt install git
```
Now we clone the repository

```sh
$ git clone https://github.com/sancolo/ando.git
```
The tree of files and directories has the following structure:

```sh
$ tree ando
ando
├── ansible
│   ├── playbooks
│   │   ├── README.md
│   │   ├── rpki-validator.retry
│   │   └── rpki-validator.yml
│   └── README.md
├── docker
│   └── build_rpki-validator
│       ├── Dockerfile
│       └── README.md
└── README.md

```
Finally, we execute ansible with the respective playbook file

```sh
$ cd ando/ansible/playbooks
$ ansible-playbook -K rpki-validator.yml
```

After the installation process we can verify that the rpki-validator is running in the virtual machine entering the url *http://IPv4\_virtual\_machine:8080*


