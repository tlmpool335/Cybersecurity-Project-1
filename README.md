# Cybersecurity-Project-1
Showcase of creating and syncing repositories, creating readme, mark down, and git commands
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram] https://drive.google.com/file/d/1yHjs_iEnLhbx87v75RS9715pT_3CdNXr/view?usp=sharing

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - [Filebeat, Metricbeat, ELK playbooks](C:\Users\Tiia - School\Downloads\README\README)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- Load balancing ensures that the application will be highly available, in addition to restricting inbound traffic to the network. The load balancer ensures that work to process incoming traffic will be shared by both vunerable web servers. Access controls will ensure that only authorized users will be able to connect in the first place. The advantage of a jump box is that it allows you to access and manage several machines within a network even among different zones. This allows you to keep your network secure. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- Filebeat helps generate and organize log files to send to Logstash and Elasticsearch. Specfically, it logs information about the file system, including which files have changed and when. 
- Metricbeat collects machine metrics, such as uptime, cpu usage, and memory. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function | IP Address | Operating System  |
|----------------------|----------|------------|------------------ |
| Jump-Box-Provisioner |Gateway   | 10.0.0.5   |Linux(Ubuntu 18.04)|           
| Web-1 DVWA           |Web Server| 10.0.0.6   |Linux(Ubuntu 18.04)|
| Web-2 DVWA           |Web Server| 10.0.0.7   |Linux(Ubuntu 18.04)|
| TMELKVM ELK          |Monitoring| 10.0.0.4   |Linux(Ubuntu 18.04)|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Only the jumb box can accept connections from the Internet. Access to this machine is only allowed from the IP address: 66.41.249.189

Machines within the network can only be accessed by _____.
- Machines within the network can only be accessed by each other. Web-1 and Web-2 (The DVWA servers) send traffic to the ELK Server

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 66.41.249.189        |
| ELK      | No                  | 10.0.0.1-254         |
| Web-1    | No                  | 10.0.0.1-254         |
| Web-2    | NO                  | 10.0.0.1-254         |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configuration with Anisble is that is a quicker and more efficient way to deploy among numerous machines with less possible human error. 

The playbook implements the following tasks:
- Installs docker.io
- Instally python3
- Installs Docker Python module
- Increases virtual/use more memory
- Downloads and launches a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Docker PS output](~/Downloads/README/README/Images)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- The DVWA servers - Web-1 and Web-2 at  10.0.0.6 and 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat detects changes to the filesystem. Specifically, we use it to collect Apache logs
- Metricbeat detects changes in the system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook files to the Ansible Control Node:

$ cd /etc/ansible
$ mkdir files
# Clone Repository + IaC Files
$ git clone https://github.com/yourusername/project-1.git
# Move Playbooks and hosts file Into `/etc/ansible`
$ cp project-1/playbooks/* .
$ cp project-1/files/* ./files

- Update the hosts file to include web servers and elk server

$ cd /etc/ansible
$ cat > hosts <<EOF
[webservers]
10.0.0.5
10.0.0.6

[elk]
10.0.0.8
EOF
- Run the playbook, and navigate to curl http://10.0.0.7:5601 to check that the installation worked as expected.
$ cd /etc/ansible
$ ansible-playbook install_elk.yml elk
$ ansible-playbook install_filebeat.yml webservers
$ ansible-playbook install_metricbeat.yml webservers

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
