# Stack Builders - AWS base

[![Build Status](https://travis-ci.org/stackbuilders/aws-base.svg?branch=master)](https://travis-ci.org/stackbuilders/aws-base)

Generic AWS resource provisioning.

## Requirements

- Ansible 2.9+
- awscli

## Usage

Install Ansible role:

```sh
ansible-galaxy install stackbuilders.aws-base
```

Example playbook:

```yaml
- hosts: local
  connection: local
  gather_facts: false
  vars:
    aws_base_keypair: aws-keypair
    aws_base_region: us-east-1
    aws_base_ec2_ami: ami-09e31fc65dcb585aa
    application_rds_username: "appadmin"
    application_rds_password: "1q2w3e4r5t"
    create_ec2: true
    aws_base_rds_port: 5432
    aws_base_rds_dbtype: postgres

  roles:
    - role: stackbuilders.aws-base
```

## Role Variables

Default important variables to set are listed below. For all variables check
defaults/main.yml

```sh
# Amazon region where the resources will be provisioned.
aws_base_region: us-west-2

# VPC network configuration.
aws_base_vpc_name: project_vpc
aws_base_vpc_cidr_block: "172.17"
aws_base_vpc_block: "{{ aws_cidr_block }}.0.0/20"

# EC2 type tag to set for the instances to create.
aws_base_ec2_type_tag: servers

# RDS database type and port.
# See: (ansible rds)[https://docs.ansible.com/ansible/latest/modules/rds_module.html] for more information
aws_base_rds_0X_port: 3306
aws_base_rds_0X_dbtype: mariadb
aws_base_rds_0X_instance_type: db.t2.micro
```

Where X is the number of the instance.

## AWS Credentials and connection

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

To use the AWS profile, set the AWS_PROFILE enviroment variable, for exammple
at run time:

```sh
AWS_PROFILE=project ansible-playbook playbooks/myplaybook.yml
```

## License

MIT, see the [LICENSE](LICENSE) file in this repository.

## Author Information

Carlos Egüez, Stack Builders Inc.
