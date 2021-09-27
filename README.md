# Project-1
ELK Server setup.
The files in this repository were used to configure the network depicted below.

13-Elk-Stack-Project_Resources_README/README/CyberClass/Diagrams/Azure Virtual Network Project.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

-13-Elk-Stack-Project_Resources_README/README/CyberClass/Scripts/Ansible/Filebeat/filebeat-playbook.yml

This document contains the following details:

Description of the Topologu
Access Policies
ELK Configuration
Beats in Use
Machines Being Monitored
How to Use the Ansible Build
Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable and available, in addition to restricting traffic to the network.

Load balancers can defend an organization against denial-of-service (DDos) attacks. The advantage of having a jumpbox is being able to use a virtual machine that has hardended security and can manage other systems within your security sone or overal network.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

Filebeat monitors the log files or locations that you specify.
Metricbeat records the metrics and statistics from the operation system and from services running on the server.
The configuration details of each machine may be found below.

Name	Function	IP Address	Operating System
Jump Box	Gateway	10.0.0.4	Linux
Web-1	Webserver 1	10.0.0.5	Linux
Web-2	Webserver 2	10.0.0.6	Linux
Web-3	Webserver 3	10.0.0.7	Linux
Access Policies
The machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:

47.145.103.191
Machines within the network can only be accessed by the Jump Box virtual machine.

The Jump Box VM has access to the ELK VM. The IP address of the Jump Box VM is 10.0.0.4
A summary of the access policies in place can be found in the table below.

Name	Publicly Accessible	Allowed IP Addresses
Jump Box	No	47.145.103.191
Web-1	No	10.0.0.4
Web-2	No	10.0.0.4
Web-3	No	10.0.0.4
ELK	No	10.0.0.4
Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

Ansible allows IT administrators to automate their daily tasks and save a lot of time. That frees them to focus on efforts that help deliver more value to the business by spending time on more important tasks.
The playbook implements the following tasks:

Install Docker
Install python3-pip
Install Docker python module
Set the vm.max_map_count to 262144
Download and launch a docker elk container
The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

13-Elk-Stack-Project_Resources_README/README/CyberClass/Images/docker_ps_output.png

Target Machines & Beats
This ELK server is configured to monitor the following machines:

Web-1, 10.0.0.5
Web-2, 10.0.0.6
Web-3, 10.0.0.7
We have installed the following Beats on these machines:

Filebeat
Metricbeat
These Beats allow us to collect the following information from each machine:

Filebeat monitors the log files or locations that you specify, which we use to see what changes or messages the log files have received such as kill commands. Metricbeat records the metrics and statistics from the operation system and from services running on the server, which we could use to look at how much RAM or CPU usage was being used on the webservers at certain time.
Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

Copy the ansible.cfg file to /etc/ansible
add the machine, its IP, and ansible_python_interpreter=/usr/bin/python3 to the hosts in the ansible.cfg as shown below:
/etc/ansible/hosts
[webservers] 10.0.0.4 ansible_python_interpreter=/usr/bin/python3 10.0.0.5 ansible_python_interpreter=/usr/bin/python3 10.0.0.6 ansible_python_interpreter=/usr/bin/python3

[elk] 10.1.0.4 ansible_python_interpreter=/usr/bin/python3

Copy the install-elk.yml and filebeat-playbook.yml file to /etc/ansible.
Update the install-elk.yml and filebeat-playbook.yml file to include the machine you want use the playbooks on by changing the hosts name on the 3rd line.
Run the playbook, and navigate to http://[your.VM.IP]:5601/app/kibana to check that the installation worked as expected.
Commands to Use the Playbook
nano ansible.cfg
add the machine, its IP, and ansible_python_interpreter=/usr/bin/python3 to the hosts
Ctrl + x to exit file
in the folder that install-elk.yml is in, run: cp install-elk.yml /etc/ansible
nano install-elk.yml /etc/ansible
name: installing elk hosts: [your_machine]
Ctrl + x to exit file
ansible-playbook install-elk.yml
