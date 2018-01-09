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
--------------
Example role variables is in vars/main.yml

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

Example playbook is in example/site.yml

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

