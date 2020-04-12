# Creating docker instance on AWS using Ansible.

There are many advantages of infrastructure automation. We can implememt any software project without worring about the system configuration. This project utilizes ansible to create a AWS ec2 instanance dynamically and then run a docker on the remote ec2. 


### Prerequisites

```
python
ansible
ubuntu machine

```

### STEP 1 : Creating ansible vaults for AWS secret.

Execute below command and add aws_access_key_id and aws_secret_access_key in the file created by the command.

```
sudo ansible-vault create vars/vault.yml
```

[default]
aws_access_key = XXXXXXXXXXX
aws_secret_key = XXXXXXXXXXXXXX

### STEP 2 : Initilize AWS variables.

Update vars/vars.yml file to update relevent aws details. Here I have used details related to my aws account.

```
aws_region_id : eu-central-1
aws_vpc_id : vpc-07db38c12d26359ac
aws_sub_id : subnet-042581e3da666d445
aws_ami_id : ami-050a22b7e0cf85dd0

aws_instance_type : t2.micro

aws_sec_key : abhishek-vpc

IdFile : /home/abhishek/.aws/abhishek-vpc.pem

default_jenkin_image : jenkins

public_ip : ''
instance_id : ''

```

### STEP 3 : Execute ansible-playbook to create ec2 and then run 'docker pull' inside ec2.
```
sudo ansible-playbook create_ec2.yml --ask-vault-pass
```
The command will ask the vault password which is created in the STEP1. The aws instance will be terminiated after docker is pulled.
## Authors

* **Abhishek Kumar** - *Initial work* - [aktechthoughts](https://github.com/aktechthoughts)


## License

This project is licensed under the MIT License.

## Acknowledgments

* **Erika Heidi** - *Digital Ocean* - [anisble-cheat-sheet](https://www.digitalocean.com/community/cheatsheets/how-to-use-ansible-cheat-sheet-guide)
* **C Tarwater** - *chrisanthropic.com* - [ansible-ec2-aws](https://www.chrisanthropic.com/blog/2016/ansible-loops-and-aws-ec2-now-with-working-tags/)

