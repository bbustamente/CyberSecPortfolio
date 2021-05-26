## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt-text](https://github.com/bbustamente/CyberSecPortfolio/blob/86272b8900ecc561608c4cf22f893b708bb5ed31/Diagrams/Untitled%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - (Ansible/)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
What aspect of security do load balancers protect? Availability, Web Traffic, Web Security What is the advantage of a jump box? Automation, Security, Network Segmentation, Access Control


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
What does Filebeat watch for?_Filebeat monitors the log files and collects log events, and sends to Elasticsearch or Logstash for indexing.
What does Metricbeat record?_Metricbeat takes the metrics and statistics that it collects and sends them to Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.6   | Linux            |
| Web-1    |Web Server| 10.0.0.4   | Linux            |
| Web-2    |Web Server| 10.0.0.5   | Linux            |
| ELK      |ELK Stack | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
My home IP Address
Machines within the network can only be accessed by Jumpbox.
Jumpbox 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My home IP           |
| Web-1    | no                  | 10.0.0.6             |
| Web-2    | no                  | 10.0.0.6             |
| ELK      | yes                 | 10.1.0.4/Home IP     |
| Load Balancer | Load Balancer  | MY home IP           |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?
Ansible lets you easily deploy apps

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.
- SSH to Jumpbox
- Install docker.io
- Install pthyon-pip
- Create playbooks
- SSH into ELK and test

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring_
10.0.0.4
10.0.0.5

We have installed the following Beats on these machines:
Specify which Beats you successfully installed
ELK, Web-1, Web-2 
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see.
Log Events, System Stats and Metrics are all collected. One example would be an Auditbeat that would collect the user activity like identity breaches and malicious behavior.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the /etc/ansible/files/filebeat-config.yml file to /etc/filebeat/filebeat-playbook.yml.
- Update the filebeat-config.yml file to include 
output.elasticsearch:
  #Array of hosts to connect to.
 hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme” 

 setup.kibana:
  host: "10.1.0.4:5601"
- Run the playbook, and navigate to Kibana / Logs : Add log data / System logs / 5:Module Status to check that the installation worked.

- Which file is the playbook? Where do you copy it? 
- .yml and to /files
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- The config.yml 
- Which URL do you navigate to in order to check that the ELK server is running?
sysadmin@10.1.0.4: curl Myhomeip:5601/app/kibana
