## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img width="469" alt="image" src="https://user-images.githubusercontent.com/88525158/148021914-d1b51c1e-4823-47b9-a82e-9dfae6e622cf.png">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  <img width="124" alt="image" src="https://user-images.githubusercontent.com/88525158/148022887-d9bfb607-3571-41ea-93d0-6d6aeba4d7ac.png">

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

- Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

- A jump box is a system on a network used to access and manage devices in a separate security zone. A jump server is a hardened and monitored device that spans two dissimilar security zones and provides a controlled means of access between them.

- Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

- Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash. Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as: Apache.

The configuration details of each machine may be found below.

| Name     | Function   | IP Address | Operating System |
|----------|----------  |------------|------------------|
| Jump Box | Gateway    | 10.0.0.12  | Linux            |
| Web 1    | Web Server | 10.0.0.10  | Linux            |
| Web 2    | Web Server | 10.0.0.11  | Linux            |
| Elk      | Elk Stack  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- Personal IP Address

Machines within the network can only be accessed by SSH.

- The ELK-Server is only accessible by SSH from the JumpBox and via web access from Personal IP Address.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses  |
|----------|---------------------|---------------------- |
| Jump Box | No                  | Personal IP Address   |
| DVWA-VMs | No                  |10.0.0.10 or 10.0.0.11 |
| Elk Stack| No                  |     10.1.0.4          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating the installation process is that we could deploy multiple servers easily and quickly without having to physically touch each server.

The playbook implements the following tasks:
- Install Docker
- Increase VM memory
- Download and configure elk docker container
- Set published ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="471" alt="image" src="https://user-images.githubusercontent.com/88525158/148024371-dd10f075-c862-4612-8534-5c39ec1db224.png">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web 1: 10.0.0.10
- Web 2: 10.0.0.11
- Elk: 10.1.0.4

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat monitors log files and locations and collects log events. (Filebeat: Lightweight, Log Analysis & Elasticsearch)

- Metricbeat records metrics and statistical data from the operating system. (Metricbeat: Lightweight Shipper for Metrics)

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the filebeat-config.yml file to metricbeat-config.yml to /etc/ansible.

- Update the configuration files to include the private IP of the ELK-Server to the ElasticSearch and Kibana sections of the configuration file.

- Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.

Which file is the playbook?

- install-elk.yml
- filebeat-playbook.yml
- metricbeat-playbook.yml

Where do you copy it?_

- etc/ansible

Which file do you update to make Ansible run the playbook on a specific machine? 

- /etc/ansible/hosts

How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

- /etc/ansible/hosts with the webserver IP address and the Elk Stack IP address.

Which URL do you navigate to in order to check that the ELK server is running?
- 40.83.139.116:5601/app/kibana

Specific commands the user will need to run to download the playbook, update the files, etc._

- ssh azureuser@JumpBox PrivateIP
- sudo docker container list -a-
- sudo docker start (Funny_Name)
- sudo docker attach (Funny_Name)
- cd /etc/ansible
- ansible-playbook elk-playbook.yml 
- cd /etc/ansible/
- ansible-playbook [filebeat or metricbeat]-playbook.yml 
- Open a new browser, navigate to (ELK-Server-publicIP:5601/app/kibana) 
