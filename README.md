# Cloud-Project
This is my cloud project for week 13
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network diagram](https://user-images.githubusercontent.com/85577662/133835831-366db891-b4a2-4193-b28b-74e66bf132d7.png)


These files have been tested and used to generate a live ELK deployment on AWS. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yaml,metricbeat-playbook.yaml,-elk-playbook.yaml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

- The main purpose of this network is to expose a load-balanced and monitored instance of webserver, the D*mn Vulnerable Web Application.

- Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

- Load balancing will protect from the denial of service attack as it will help to divert the traffic and to distribute the load.
  Moreover, It helps with the intrusion prevention by restricting access to the servers holding the application.
  
  A jump box provides a controlled access to the servers/VMs holding the applications and helps with the management of these hosts

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file and system metric.
- Filebeat watches for the changes in the files in the locations that we specify or the log files and then collects and send the data to logstash/elasticsearch.
- Metricbeat collects the metric data from the services and the operating system and sends it to logstash/elasticsearch.

The configuration details of each machine may be found below.

| Name          |   Function | IP Address  | Operating System |
|----------     |  ----------|------------ |------------------|
| Jump Box      |  Gateway   |10.0.0.21    |  Linux           |
| Webserver1    |  Server    |10.0.0.125   |  Linux           |
| Webserver2    |  Server    |10.0.0.18    |  Linux           |  
| Webserver3    |  Server    |10.0.0.247   |  Linux           |
| ELK server    | Log server |10.0.0.157   |  Linux           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address

Machines within the network can only be accessed by SSH.
The only machine that is able to connect to the Elk-Server (10.0.0.157) is via JumpBox from Private IP (10.0.0.21)_

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|---------- |---------------------|----------------------|
| Jump Box  |       yes           |   3.143.1.224       |
| Webserver1|       no            |   10.0.0.21          |
| Webserver2|       no            |   10.0.0.21          |
| Webserver3|       no            |   10.0.0.21          |
| ELK sever |       no            |   10.0.0.21          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
 -In case we need to configure more machines,we can just run the ansible playbook instead of going to every machine and configuring individually.
  The playbook implements the following tasks:
 -Install docker.io
 -Install PIP
 -Install docker python module
 -Download and Install a Docker elk container
 -run command to increase the memory

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Image docer ps](https://user-images.githubusercontent.com/85577662/133484474-0c9b2c93-b3a1-40c7-9e6a-10f71afaca02.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 Web server1 10.0.0.125
 web server2 10.0.0.18
 Web server3 10.0.0.247

We have installed the following Beats on these machines:
 -Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
  -Filebeat watches for the changes in the files in the locations that we specify or the log files and then collects and send the data to logstash/elasticsearch for example the    modifications in a file.
 -Metricbeat collects the metric data from the services and the operating system and sends it to logstash/elasticsearch such as Apache service

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml and metricbeat-playbook.yml files to /etc/ansible.
- Update the file t/etc/ansible/hosts to include the ip address of the machine under webservers
- Run the playbook, and navigate to 3.142.40.184:5601/app/kibana to check that the installation worked as expected.

### Bonus
 I used AWS CloudFormation template to create and manage a Virtual Private Cloud (VPC), complete with subnets, NATting, route tables, ElasticIPAddress,InternetGateway, SecurityGroup, then it will Create ec2 instances tagging as jumpbox hosting Docker container and Ansibel, three ec2 instant tagging as webserver and another ec2 instant tagging 
as elk server.use CloudFormation allows us to create a "stack" in one step This is faster, repeatable, and more consistent than manually creating our network via the management 
console or CLI. We can check our template into source control and use it any time we like for any purpose we want. 
  
 
