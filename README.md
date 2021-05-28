## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event log and system metrics.
- _TODO: What does Filebeat watch for?_
- _TODO: What does Metricbeat record?_

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web 1    | Server   | 10.1.0.8   | Linux            |
| Web 2    | Server   | 10.1.0.6   | Linux            |
| Web 3    | Server   | 10.1.0.9   | Linux            |
| ELK      | ELKStack | 10.3.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | no             | 10.0.0.1 10.0.0.2    |
| Load Balancer |                 |                      |
| Web 1         | NO               |                      |
| Web 2         | NO               |                      |
| Web 3         | No              |             |





### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible can run from the command line

The playbook implements the following tasks:
- install docker.io
- install python3-pip
- install docker module

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker_ps](./Images/docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1 - 10.1.0.8
- Web 2 - 10.1.0.6
- Web 3 - 10.1.0.9

We have installed the following Beats on these machines:
- filebeat-7.4.0-amd64.deb

These Beats allow us to collect the following information from each machine:
- Sends information about log files of servers to Kibana. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Filebeat-configuration.yml  file to ELK_VM.
- Update the hosts file to include 
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?
```
`Sample Username: admin`
`---`
`- name: installing and launching filebeat`
`  hosts: webservers`
`  become: yes`
`  tasks:`

`  - name: download filebeat deb`
`    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb`

`  - name: install filebeat deb`
`    command: sudo dpkg -i filebeat-7.6.1-amd64.deb`

`  - name: drop in filebeat.yml`
 `   copy:`
  `    src: /etc/ansible/files/filebeat-config.yml`
   `   dest: /etc/filebeat/filebeat.yml`

`  - name: enable and configure system module`
`    command: filebeat modules enable system`

  ` - name: setup filebeat`
  `   command: filebeat setup`

  ` - name: start filebeat service`
  `   command: service filebeat start`

  ` - name: enable service filebeat on boot`
  `   systemd:`
  `     name: filebeat`
  `     enabled: yes`



```
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._