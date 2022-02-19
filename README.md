## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Diagrams/Network-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

  - Ansible/install_elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorized access to the network.
Load balancers are an important security tool because they can immensely help mitigate a DDos attack. Jump boxes are also useful because they provide an all-in-one access point for administrative tasks. JumpBoxes can be considered a SAW, Secure Admin Worstation, which would require an administrator to access the JumpBox before accesssing the servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
Filebeat watches for log files/locations and collects events related to those files and locations.
Metricbeat records metrics and statistical data from the operating system and services that are running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_. 

| Name      | Function | IP Address   | Operating System |
|-----------|----------|--------------|------------------|
| Jump Box  | Gateway  | 10.0.0.4     | Ubuntu-Server    |
| Elk-Server| Config VM| 10.1.0.4     | Linux            |
| Web-1     | DVWA     | 10.1.0.5     | Linux            |
| Web-2     | DVWA     | 10.1.0.6     | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
My personal IP address.

Machines within the network can only be accessed by SSH.
My personal public IP address is the only machine allowed access to the ELK-server via port 5601.
The ELK Server is only accessible by SSH from the JumpBox.

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump Box  |      yes            | Personal IP Address  |
| Web-1     |      No             | 10.1.0.5             |
| Web-2     |      No             | 10.1.0.6             |
| Elk-Server|      No             | 10.1.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
Ansible is quick and easy to use!

The playbook implements the following tasks:
Install Docker
Install python3-pip
Install Docker module pip
Use systemctl to use more memory

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1: 10.1.0.5
Web-2: 10.1.0.6

We have installed the following Beats on these machines:
Filebeats
Metricbeats

These Beats allow us to collect the following information from each machine:
Filebeat collects system logs, which can be used to track system events, etc.
Metricbeat collects system and service metric data, which we can use to see CPU usage, etc.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files.
Update the configuration files to include the Private IP of the ELK-Server to the ElasticSearch and Kibana Sections of the Configuration File
Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.


Which file is the playbook? 
elk-playbook.yml - used to install ELK Server
filebeat-playbook.yml - Used to install and configure Filebeat on Elk Server and DVWA servers
metricbeat-playbook.yml - Used to install and configure Metricbeat on Elk Server and DVWA servers

Where do you copy it?
/etc/ansible/

Which file do you update to make Ansible run the playbook on a specific machine? 
/etc/ansible/hosts.cfg

How do I specify which machine to install the ELK server on versus which to install Filebeat on?

In /etc/ansible/hosts you tell it where you want each one to be installed ElkServers or FileBeat

Which URL do you navigate to in order to check that the ELK server is running?

http://publicip(elkserver):5601
