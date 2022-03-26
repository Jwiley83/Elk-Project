## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!![image](https://user-images.githubusercontent.com/94330057/160218223-9e1779ae-ee9d-45d8-a830-8e5bda200ae3.png)

(Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook (.yml) file may be used to install only certain pieces of it, such as Filebeat.

  - my-playbook.yml
  - elk-playbook.yml
  -   filebeat-playbook.yml
  -   metricbeat-playbook.yml

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

- What aspect of security do load balancers protect?
- Load Balancers add security by rerouting live traffic from one server to another in the event of a DOS attack or if its offline.

- What is the advantage of a jump box?
- Jump Box provides security by restricting IP addresses and allowing one source to filter traffic through to another virtual machine that is private.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- What does Filebeat watch for?
- Filebeat monitors the log files, collect log events, and fowards them for indexing.

- What does Metricbeat record?
- Metricbeat takes the metrics and data then send the output to Elasticsearch.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name               | Function                 | IP Address | Operating System         |
|--------------------|--------------------------|------------|--------------------------|
| Jump Box           | Gateway                  | 10.0.0.4   | Linux (Ubuntu 18.04 LTS) |
| Web-1              | Web Server- Docker- DVWA | 10.0.0.5   | Linux (Ubuntu 18.04 LTS) |
| Web-2              | Web Server- Docker- DVWA | 10.0.0.11  | Linux (Ubuntu 18.04 LTS) |
| Web-3 (Elk Server) | Elk Stack                | 10.1.0.4   | Linux (Ubuntu 18.04 LTS) ||

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address

Machines within the network can only be accessed by SSH.
- The Elk-Server is only accessible by SSH from the Jump Box and via web access from the Personal IP Address

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible    | Personal IP Address                              |
|--------------------|------------------------|--------------------------------------------------|
| Jump Box           | No                     | Personal IP Address                              |
| Web-1              | Yes with Load Balancer | 20.125.37.135 Load Balancer Public IP 10.0.0.4   |
| Web-2              | Yes with Load Balancer | 20.125.37.135 Load Balancer Public IP 10.0.0.4   |
| Web-3 (Elk-Server) | No                     | SSH 10.1.0.4 Jump Box HTTP Port 5601 Personal IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The advantage of automating the installation process is that it could deploy multiple servers easily and quickly without having to physically touch each server.

The playbook implements the following tasks:
- Install Docker.io and pip3
- Increases Virtual Machine Memory
- Download and configure Elk Docker
- Set Published Ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!![image](https://user-images.githubusercontent.com/94330057/160215818-fde4199c-4691-48d8-8513-6887927b5429.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.11

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
-Filbeat watches for Log files/locations and collect log events.
-Metricbeat records metrics and statistical data from the operating system and from services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files.
- Update the configuration files to include the Private IP if the Elk-Server to ElasticSearch and Kibana sections of the Configuraion file.
- Run the playbook, and navigate to Elk-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.


- Which file is the playbook?
- elk-playbook.yml
- filebeat-playbook.yml
- metricbeat-playbook.yml

-  Where do you copy it?
-  /etc/ansible/
- 
- Which file do you update to make Ansible run the playbook on a specific machine? 
- /etc/ansible/hosts.cfg
-
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- /etc/ansible/hosts is where you want to install Filebeat on.

- Which URL do you navigate to in order to check that the ELK server is running?
- http://20.125.37.135:5601/app/kibana

