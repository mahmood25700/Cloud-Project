## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![netwok diagram](https://user-images.githubusercontent.com/85577662/133496576-00db5b2b-c3e0-40b6-9654-8ed8dc6bb4c8.png)


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

The main purpose of this network is to expose a load-balanced and monitored instance of webserver, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancing will protect from the denial of service attack as it will help to divert the traffic and to distribute the load.
  Moreover, It helps with the intrusion prevention by restricting access to the servers holding the application.
  A jump box provides a controlled access to the servers/VMs holding the applications and helps with the management of these hosts

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file and system metric.
-Filebeat watches for the changes in the files in the locations that we specify or the log files and then collects and send the data to logstash/elasticsearch.
 Metricbeat collects the metric data from the services and the operating system and sends it to logstash/elasticsearch

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name          |   Function | IP Address  | Operating System |
|----------     |  ----------|------------ |------------------|
| Jump Box      |  Gateway   |172.31.2.40  |  Linux           |
| Webserver1    |  Server    |172.31.22.10 |  Linux           |
| Webserver2    |  Server    |172.31.14.229|  Linux           |  
| Webserver3    |  Server    |172.31.21.65 |  Linux           |
| ELK server    | Log server |172.31.42.92 |  Linux           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address

Machines within the network can only be accessed by SSH.
The only machine that is able to connect to the Elk-Server (172.31.42.92) is via JumpBox from Private IP (172.31.2.40)_

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|---------- |---------------------|----------------------|
| Jump Box  |       yes           |   18.221.86.31       |
| Webserver1|       no            |   172.31.2.40        |
| Webserver2|       no            |   172.31.2.40        |
| Webserver3|       no            |   172.31.2.40        |
| ELK sever |       no            |   172.31.2.40        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
 .In case we need to configure more machines,we can just run the ansible playbook instead of going to every machine and configuring individually.
  The playbook implements the following tasks:
 .Install docker.io
 .Install PIP
 .Install docker python module
 .Download and Install a Docker elk container
 .run command to increase the memory

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Image docer ps](https://user-images.githubusercontent.com/85577662/133484474-0c9b2c93-b3a1-40c7-9e6a-10f71afaca02.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 Web server1 172.31.22.10
 web server2 172.31.14.229
 Web server3 172.31.21.65

We have installed the following Beats on these machines:
 .Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
  .Filebeat watches for the changes in the files in the locations that we specify or the log files and then collects and send the data to logstash/elasticsearch for example the    modifications in a file.
  . Metricbeat collects the metric data from the services and the operating system and sends it to logstash/elasticsearch such as Apache service

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml and metricbeat-playbook.yml files to /etc/ansible.
- Update the file t/etc/ansible/hosts to include the ip address of the machine under webservers
- Run the playbook, and navigate to 18.221.151.85:5601/app/kibana to check that the installation worked as expected.

