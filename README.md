Stack Builders - AWS provisioning.
=========

[![Build Status](https://travis-ci.org/speedlight/aws-provision.svg?branch=master)](https://travis-ci.org/speedlight/aws-provision)

Generic AWS resource provisioning.

Requirements
------------

- Ansible 2.6+
- boto/boto3 
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

# EC2 AMI ID for the us-weast-2 region: Debian Stretch x86_64
aws_ec2_ami: ami-09d31fc66dcb58522

# EC2 type tag to set for the instances to create.
aws_ec2_type_tag: servers

# RDS database type and port. 
# See: (ansible rds)[https://docs.ansible.com/ansible/latest/modules/rds_module.html] for more information
aws_rds_port: 3306
aws_rds_dbtype: mariadb
aws_rds_instance_type: db.t2.micro
```

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

Example Playbook
----------------
```yaml
- hosts: local
  connection: local
  gather_facts: false
  vars:
    aws_keypair: aws-keypair
    aws_region: us-east-1
    application_rds_username: "appadmin"
    application_rds_password: "1q2w3e4r5t"
    create_ec2: true
    aws_rds_port: 5432
    aws_rds_dbtype: postgres

  roles:
    - role: aws-role
```
-------

MIT

Author Information
------------------

Carlos Egüez, Stack Builders Inc.
