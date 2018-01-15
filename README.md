ansible-lc-asg-aws
=========

[![Build Status](https://travis-ci.org/zedit/ansible-aws-lc-asg.svg?branch=dev)](https://travis-ci.org/zedit/ansible-aws-lc-asg) 

This role create AWS Autoscaling Group with Application load balancer.
You can enable support AWS Elastic Container Service, then ASG to be attached on ecs cluster.

Requirements
------------

```sh
Ansible >= 2.4.0.0
boto
boto3
botocore
json
```


Role Variables

main file which contains variables values

vars/main.yml:
```sh
---
###values of variables uses in ALB and ASG###
subnets: - subnets for 
  - "subnet-3a0d4877"
  - "subnet-40b2993b"

###values of variables uses for target group###
target_group:
  name: "my-tg"
  manage: true

###values of variables uses for ALB###
application_load_balancer:
  name: "my-alb"
  subnets: "{{ subnets }}"
  security_groups: "default"
  listeners:
    - Protocol: HTTP 
      Port: 80
      DefaultActions:
        - Type: forward 
          TargetGroupName: "{{ target_group.name }}"

###users values###
user_lc_asg:
  aws_region: "eu-west-2"
  aws_vpc_id: "vpc-00f8c269"
  tg: "{{ target_group }}"
  alb: "{{ application_load_balancer }}"
  subnets: "{{ subnets }}"
```

If the are no custom variables, then the variables are taken from the file
defaults/main.yml

```sh
---
# defaults file for ansible-lc-asg-aws

default_lc_asg:
  aws_region: "us-east-1"
  aws_lc_name: "my-launch-configuration"
  aws_key_pair: "default"
  aws_instance_type: "t2.micro"
  aws_asg_name: "my-asg"
  aws_ami_id: "ami-82f4dae7"

###This line override default variables if custom variables are defined### 
lc_asg: "{{ default_lc_asg | combine(user_lc_asg|default({}), recursive=True) }}"
```

Example Playbook
----------------

Export enviroment variables with AWS credentials:
```sh
export AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY_ID
export AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_ACCESS_KEY
```

Create dir when you clone ansible role from github:
```sh
mkdir -p example/roles
cd example
```

Clone role repository from github and configure ansible:
```sh
cd roles
git clone git@github.com:unicanova/ansible-lc-asg-aws.git
cd ..
```

Edit ansible.cfg
```sh
[defaults]
hostfile = ./hosts.cfg
remote_user = root
host_key_checking = False
timeout = 5
pipelining = True
roles_path = roles
```

Example playbook 
```sh
- hosts: 127.0.0.1
  connection: local
  roles:
   - { role: ansible-lc-asg-aws, tags: 'test' }
```
Run anisble:
```sh
ansible-playbook site.yaml -t test
```

License
-------

MIT

Author Information
------------------
Author: Konstantin Kalinovskyi

Email: k@unicanova.com

Company: UnicaNova 

Website: https://unicanova.com/

