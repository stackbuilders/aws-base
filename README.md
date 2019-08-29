Stack Builders - Debian Base
=========

Generic AWS resource provisioning.

Requirements
------------

- Ansible 2.6+
- boto/boto3 
- awscli

Install
--------------
```sh
ansible-galaxy install stackbuilders.aws-role
```

Role Variables
--------------
The important variables to set are listed below. For all variables check defaults/main.yml

```sh
# Amazon region where the resources will be provisioned.
aws_region: us-west-2

# CIDR address block first two octates.
aws_cidr_block: "172.17"

# VPC CIDR block.
aws_vpc_block: "{{ aws_cidr_block }}.0.0/20"

# EC2 AMI ID for the us-weast-2 region: Debian Stretch x86_64
aws_ec2_ami: ami-09d31fc66dcb58522
```
Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
