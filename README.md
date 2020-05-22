Stack Builders - AWS base.
=========

[![Build Status](https://travis-ci.org/stackbuilders/aws-base.svg?branch=master)](https://travis-ci.org/stackbuilders/aws-base)

Generic AWS resource provisioning.

Requirements
------------

- Ansible 2.9+
- awscli

Install
--------------
```sh
ansible-galaxy install stackbuilders.aws-provision
```

Role Variables
--------------
Default important variables to set are listed below. For all variables check defaults/main.yml

```sh
# Amazon region where the resources will be provisioned.
aws_region: us-west-2

# VPC network configuration.
aws_vpc_name: project_vpc
aws_vpc_cidr_block: "172.17"
aws_vpc_block: "{{ aws_cidr_block }}.0.0/20"

# EC2 type tag to set for the instances to create.
aws_ec2_type_tag: servers

# RDS database type and port. 
# See: (ansible rds)[https://docs.ansible.com/ansible/latest/modules/rds_module.html] for more information
aws_rds_0X_port: 3306
aws_rds_0X_dbtype: mariadb
aws_rds_0X_instance_type: db.t2.micro
```
Where X is the number of the instance.

AWS Credentials and connection
----------------
In `~/.aws/config` we can set a profile or use the default, for example:
```sh
[default]
region = us-east-1
[project]
region = us-west-2
output = json
```

Then we set Amazon credentials in `~/.aws/credentials` for our profile:
```sh
[project]
aws_access_key_id = AMAZONKEYID
aws_secret_access_key = AMAZONSECRECTKEY
```

To use the aws profile, set the AWS_PROFILE enviroment variable, for exammple at run time:
```sh
AWS_PROFILE=project ansible-playbook playbooks/myplaybook.yml
```

##NOTE: We MUST set the `aws_ec2_ami` value like the following as this depends on the region:
```sh
aws_ec2_ami: ami-09d31fc66dcb58522
```

Example Playbook
----------------
```yaml
- hosts: local
  connection: local
  gather_facts: false
  vars:
    aws_keypair: aws-keypair
    aws_region: us-east-1
    aws_ec2_ami: ami-09e31fc65dcb585aa
    application_rds_username: "appadmin"
    application_rds_password: "1q2w3e4r5t"
    create_ec2: true
    aws_rds_port: 5432
    aws_rds_dbtype: postgres

  roles:
    - role: aws-role
```
-------

MIT, see the [LICENSE](LICENSE) file in this repository.

Author Information
------------------

Carlos Egüez, Stack Builders Inc.
