Slack Notify
=========

Slack integration for ansible deployments

Requirements
------------

- Ansible 2.0.1 or higher.
- Tested on Ubuntu 14.04 and Amazon 7

Role Variables
--------------

| parameter             | required | default | choices | comments |
| --------------------- | -------- | ------- | -------- |-------- |
| ec2_load_balancer | yes| | | A list of VPC subnets to use when creating ELB. Zones should be empty if using this. |
| aws_resource_tags.VREnv| no| internet-facing | internet-facing, internal|The scheme to use when creating the ELB. For a private VPC-visible ELB use 'internal'. |
| slack_channel_notify| | | |A list of security groups to apply to the elb |
| slack_token| | | | List of ports/protocols for this ELB to listen on (see [vars](defaults/main.yml)| 
| slack_username| no | / | |The destination for the HTTP or HTTPS request. | 
| aws_asg.name | no | | | ASG name|

Ansible modules
--------------
[slack](http://docs.ansible.com/ansible/slack_module.html)


Output variables
--------------

None

Example Playbook
----------------

   
    - hosts: localhost
      vars:
        aws_resource_tags: {
         'Name': 'slack-notify',
         'VREnv': 'PROD',
         'VRProject': 'slack-noify',
         'VRTeam': 'infra'}
        ec2_load_balancer: slack-notify-1762532888.us-east-1.elb.amazonaws.com
        slack_channel_notify: test_slack
        slack_token: YOUR-SLACK-TOKEN
        slack_username: deploy_bot
        
      roles:
        - { role: VivaReal.slack-notify }
   

License
-------

BSD

Author:
------------------

Giancarlo Rubio (<gianrubio@gmail.com>)