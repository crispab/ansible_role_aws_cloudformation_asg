betrcode.aws-cf-asg
===================

*Better Code AWS CloudFormation AutoScalingGroup*

This role creates a AWS AutoScalingGroup and a 
ElasticLoadBalancer. The ASG will start a Docker image of 
your choice.


Requirements
------------

AWS credentials.

Packages:

* boto3


Role Variables
--------------

TODO: 

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

Not dependent on any other role.


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

---

    - hosts: localhost
      connection: local
      gather_facts: yes  # needed for ansible_date_time
      roles:
        - role: betrcode.aws-cf-asg
          docker_image: "nginx:latest"

License
-------

MIT

Author Information
------------------

Max Wenzin, partner at Crisp

https://www.crisp.se/konsulter/max-wenzin

