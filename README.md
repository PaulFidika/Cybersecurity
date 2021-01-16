## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://github.com/PaulFidika/Cybersecurity/blob/main/Images/RedTeamNetwork.png?raw=true)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA (Damn Vulnerable Web Application).

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

The configuration details of each machine may be found below.

| Name       | Function               | Private IP Address | Operating System |
|------------|------------------------|--------------------|------------------|
| Jump-Box   | Gateway to the network | 10.0.0.4           | Ubuntu           |
| Web-1      | DVWA Webserver         | 10.0.0.5           | Ubuntu           |
| Web-2      | DVWA Webserver         | 10.0.0.6           | Ubuntu           |
| Web-3      | DVWA Webserver         | 10.0.0.9           | Ubuntu           |
| ELK-server | Elastisearch           | 10.1.0.4           | Ubuntu           |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
154.27.124.40,
204.98.77.162,
174.97.167.135

Machines within the network can only be accessed by the Jumpbox Server.

A summary of the access policies in place can be found in the table below.

| Name       | Publicy Accessible | Allowed IP Addresses                                        |
|------------|--------------------|-------------------------------------------------------------|
| Jump Box   | No                 | 154.27.124.40, 204.98.77.162, 174.97.167.135                |
| Web-1      | No                 | 204.98.77.162, 23.99.221.241, 154.27.124.40, 174.97.167.135 |
| Web-2      | No                 | 204.98.77.162, 23.99.221.241, 154.27.124.40, 174.97.167.135 |
| Web-3      | No                 | 204.98.77.162, 23.99.221.241, 154.27.124.40, 174.97.167.135 |
| Elk-server | No                 | 154.27.124.40, 204.98.77.162, 172.17.0.2, 174.97.167.135    |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
it allows for easy scaling to more servers; identical new instances can be created and configured automatically.

The playbook implements the following tasks:
- Uses apt to install docker.io
- Uses apt to install python3-pip, which is a python package-management system
- Uses pip to install docker
- Sets a system memory configuration
- Uses docker to download and launch the ELK docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/Ansible_Installs_ELK.jpg)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.5
10.0.0.6
10.0.0.9

We have installed the following Beats on these machines:
Web-1
Web-2
Web-3

These Beats allow us to collect the following information from each machine:
Filebeat collects the websever's log files
Metricbeat collects metrics about the status of our webservers

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk-playbook.yml file to /etc/ansible/files/.

- Update the /etc/ansible/hosts file to include the private (local) IP addresses of the other machines on your network
- use the command 'nano /etc/ansible/hosts' to edit the file. Your groups should look like:
[webservers]
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3
10.0.0.9 ansible_python_interpreter=/usr/bin/python3

[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to http://<ip address>:5601/app/kibana to check that the installation worked as expected,
where <ip address> is the public-ip address of the server running your elk
- You can run this with the 'ansible-playbook /etc/ansible/files/install-elk-playbook.yml' command

