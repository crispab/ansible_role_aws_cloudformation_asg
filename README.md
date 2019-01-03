crisp.aws_cloudformation_asg
============================

*Crisp AWS CloudFormation AutoScalingGroup*

This role creates a AWS AutoScalingGroup and a ElasticLoadBalancer. 
The ASG will start a Docker image of your choice.

Most of the resources are created by CloudFormation. 
The Route 53 DNS entry is outside the CloudFormation stack because it acts as a pointer 
between different ELBs (inside stacks) and can not be modified this way if it was inside a stack.

The main upside of using CloudFormation is that cleanup of old resources is much easier.
However, the Ansible module for querying which stacks exists is not very nice. It returns a hard-to-use
data structure (for my use-case) and offers very little querying options. 


Every time the playbook is run it will:

* Create a new CloudFormation stack containing:
    * A new SecurityGroup for the instances
    * A new SecurityGroup for the ElasticLoadBalancer
    * A new LaunchConfiguration for the AutoScalingGroup
    * A new TargetGroup for the AutoScalingGroup
    * A new AutoScalingGroup
    * A new ElasticLoadBalancer
    * A new Listener for the ElasticLoadBalancer
* Create/update the DNS alias to point to the new load balancer
* Delete (cleanup) any old stacks created by this role

The main benefit of this is that *all* infrastructure is replaced on every deployment.


Requirements
------------

AWS credentials.

Packages:

* boto3


Role Variables
--------------

* `vpc` - the AWS VPC identifier (your vpc)
* `region` - the AWS region to deploy to (example: eu-west-1)
* `subnets` - a list of subnets to deploy to. Must be at least 2. (needs to exist already)
* `aws_key` - the instance key which can be used to log in to the created instances (needs to exist already)
* `route53_zone` - the Route 53 zone where you want to create your DNS entry. (needs to exist already)
* `instance_profile` - the name of the instance profile (or IAM Role) that the created instances will get. (needs to exist already)


Required environment variables:

* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`



Dependencies
------------

Not dependent on any other role.


Example Playbook
----------------

---

    - hosts: localhost
      connection: local
      gather_facts: yes  # needed for ansible_date_time
      roles:
        - role: betrcode.aws_cloudformation_asg
          docker_image: "nginx:latest"


License
-------

MIT


Author Information
------------------

Max Wenzin, partner at Crisp

https://www.crisp.se/konsulter/max-wenzin

