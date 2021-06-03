# Cloud Security: An Automated ELK-Stack-Project
Configuring an ELK stack server in order to set up a cloud monitoring system.


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured below. Alternatively, select portions of the README file may be used to install only certain pieces of it, such as Filebeat.
  (/Ansible/ansibleplaybook_filebeat.txt)







This document contains the following details:
- Description of the Topology 
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build





















# Description of the Topology
 
 
 ![image](https://user-images.githubusercontent.com/74993121/120721930-6e51f180-c494-11eb-8ab3-fcf2bead621f.png)

 
 

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network. Additionally, the load balancer makes sure that no single server has too much traffic to handle, and it works to process incoming traffic that will be shared by both vulnerable web servers. The Access controls will ensure that only authorized users (ourselves) will be able to connect in the first place.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network and watch system metrics, such as CPU usage; attempted SSH logins; sudo escalation failures; etc. 










The configuration details of each machine may be found below.

| Name         | Function           | IP Address | OS    |   
| Jump Box     | Gateway            | 10.0.0.4   | Linux |   
| DVWA1        | Web Server         | 10.0.0.5   | Linux |   
| DVWA2        | Web Server         | 10.0.0.6   | Linux |   
| Redundant VM | Redundancy Testing | 10.0.0.8   | Linux |   
| ELK-Server        | Monitoring        | 10.1.0.4 | Linux |   



Additionally, Azure has provisioned a load balancer in front of all machines except for the Jump Box. The Load Balancer’s targets are organized by the following Availability Zones: 

-	Availability Zone 1: DVWA 1 + DVWA 2
-	Availability Zone 2: ELK



# Access Policies
The machines on the internal network are not exposed to the public Internet. 

Only the JUMPBOX machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

-  64.72.118.76 
Machines within the network can only be accessed by each other!
- The DVWA1 and DVWA2 VMs send traffic to the ELK Server


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 64.72.118.76   |
|    ELK      |      No               |     10.0.0.1-254                 |
|    DVWA 1      |       No              |          10.0.0.1-254            |
|    DVWA 2      |         No            |         10.0.0.1-254             |






# Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves A LOT of time for IT administrators and allows simplification of complex tasks. This increases efficiency while freeing up more time.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- installs docker.io
- installs python3-pip
- installs docker, which is the Docker Python pip module
- downloads and runs containers
- ELK container gets installed and the web server is up and running  

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/Successful Elk ansible playbook.png




 # Target Machines & Beats
This ELK server is configured to monitor the following machines:
- DVWA 1 at 10.0.0.5
- DVWA 2 at 10.0.0.6 


We have installed the following Beats on these machines:
- Filebeat
- Metricbeat
- Packetbeat 

These Beats allow us to collect the following information from each machine:
-	Filebeat: Filebeat detects changes to the filesystem. Specifically, we use it to collect Apache logs.
-	 Metricbeat: Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics.
-	Packetbeat: Packetbeat collects packets that pass through the NIC, similar to Wireshark. We use it to generate a trace of all activity that takes place on the network, in case later forensic analysis should be warranted.



# Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. We use the jump box for this purpose. 

To use the playbooks, we must perform the following steps: 
	- Copy the playbooks to the Ansible Control Node
	- Run each playbook on the appropriate targets 


The easiest way to copy the playbooks is to use Git:


![image](https://user-images.githubusercontent.com/74993121/120722096-bf61e580-c494-11eb-9481-03d1b0ed23c4.png)



This copies the playbook files to the correct place.
Next, you must create a hosts file to specify which VMs to run each playbook on. Run the commands below:


![image](https://user-images.githubusercontent.com/74993121/120722113-cd176b00-c494-11eb-90ad-681139c45d5e.png)



After this, the commands below run the playbook:


![image](https://user-images.githubusercontent.com/74993121/120722139-dc96b400-c494-11eb-8310-2171b1e27d13.png)



- Run the playbook, and navigate to ____ to check that the installation worked as expected.
To verify success, wait five minutes to give ELK time to start up.
Then, run: curl http://10.0.0.8:5601. This is the address of Kibana. If the installation succeeded, this command should print HTML to the console.

