ansible-lc-asg-aws
=========

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
In vars/main.yml

```sh
###Uncomment aws_ecs, aws_ecs_clustername, aws_ecs_ec2_role if you be used ecs###
#aws_ecs: "Yes"
#aws_ecs_clustername: "name of ecs cluster"
aws_region: "region id"
aws_lc_name: "name of LaunchConfigurations"
aws_ami_id: "ami id"
aws_key_pair: "ssh key name"
aws_sg_alb: "security group for alb"
aws_sg_lc: ['security group for LaunchConfigurations']
aws_instance_type: "instance type"
aws_asg_name: "auto scaling group name"
aws_vpc_id: "vpc id for LaunchConfigurations and target group"
###aws_vpc_zone - vpc subnets for autoscaling group###
aws_vpc_zone: ['subnet id for availability zone a', 'subnet id for availability zone b', 'subnet id for availability zone c']
aws_alb_name: "Name of ALB"
###subneta, subnetb, subnetc - vpc subnets for ALB###
aws_alb_subnet_az_a: "subnet id for availability zone a"
aws_alb_subnet_az_b: "subnet id for availability zone b"
aws_alb_subnet_az_c: "subnet id for availability zone c"
aws_tg_name: "name of target group"
###Uncomment if you use ecs instance type###
#aws_ecs_ec2_role: "ecsInstanceRole"
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
mkdir -p example/Roles
cd example
```

Clone role repository from github and configure ansible:
```sh
cd Roles
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
roles_path = Roles
```

Edit site.yaml
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
Author: Sergey Ovsienko 

Email: so@unicanova.com

Company: UnicaNova 

Website: https://unicanova.com/

