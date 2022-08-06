### Automated ELK Stack Deployment

  The files in this repository were used to configure the network depicted below.

  ![ELK Stack diagram](https://github.com/PriyankaTilavalli/PriyankaTilavalliELKProject1/blob/main/ELK%20Project%201/Diagrams/ELK%20Stack%20diagram.drawio.png)

  These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible files may be used to install only certain pieces of it, such as Filebeat.

  - Install-elk.yml
  - Filebeat-config.yml
  - Filebeat-Playbook.yml
  - Metricbeat-config.yml
  - Metricbeat-playbook.yml

  This document contains the following details:
  - Description of the Topology
  - Access Policies
  - ELK Configuration
    - Beats in Use
    - Machines Being Monitored
  - How to Use the Ansible Build
<br>
<br>

### Description of the Topology

  The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

  Load balancing ensures that the application will be highly functional, in addition to restricting high-traffic to the network.
  - The Load balancer ensures that work to process incoming traffic will be shared by both vulnerable wed servers. 
  - Having a jump box allows the system to be updated all at once as only a single system requires the update, keeping the service available with little to no downtime.

  Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jumpbox and system network.
  - Filebeat gathers information about the file system, and logs which files have changed and when. It then sends this information to be processed in Logstash or into  Elasticsearch for indexing. In Kibana it is used to visualize the data.
  - Metricbeat gathers information about the system it is installed on. This includes the system resources and services. Just like file be it send the information to Logstash or Elasticsearch.

  The configuration details of each machine may be found below.

  | Name       | Function        | IP Address | Operating System |
  |------------|-----------------|------------|------------------|
  | Jump Box   | Gateway         | 10.0.0.5   | Linux            |
  | Web-1      | Web Server      | 10.0.0.4   | Linux            |
  | Web-2      | Web Server      | 10.0.0.6   | Linux            |
  | Web-3      | Web Server      | 10.0.0.7   | Linux            |
  | ELK-Server | Data Monitoring | 10.1.0.4   | Linux            |
<br>
<br>

### Access Policies

  The machines on the internal network are not exposed to the public Internet. 

  Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 20.92.74.148

  Machines within the network can only be accessed by Web-1, Web-2 and Web-3 VMs they send traffic to the ELK-Server.
  - The only machine that has permission to access the Elk Server is the Jump Box, of which its IP address is 10.0.0.5.

  A summary of the access policies in place can be found in the table below.

  | Name       | Publicly Accessible | Allowed IP Addresses      |
  |------------|---------------------|---------------------------|
  | Jump Box   | Yes                 | 20.92.74.148 and 10.0.0.5 |
  | Web-1      | No                  | 10.0.0.4                  |
  | Web-2      | No                  | 10.0.0.6                  |
  | Web-3      | No                  | 10.0.0.7                  |
  | ELK-Server | Yes                 | 10.1.0.4                  |
<br>
<br>

### Elk Configuration

  Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because to install the Elk machine is that is automated the install. And in using Ansible we can easily install an program or image on multiple computers in a short amount of time, with the same configuration. Using Ansible also gave us a chance to learn a little of YML scripting, and some of the nuances of it, particularly the fact tabs are not allowed for indentation.

  The playbook implements the following tasks:
  - Install Docker.io and pip3.
  - Change VM Memory size of the ELK VM.
  - Download and Configure the ELK docker container.
  - Set Ports.

  The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

  ![Docker Screenshot]()
<br>
<br>

### Target Machines & Beats

  This ELK server is configured to monitor the following machines:
  - Web-1 10.0.0.4
  - Web-2 10.0.0.6
  - Web-3 10.0.0.7

  We have installed the following Beats on these machines:
  - Filebeat
  - Metricbeat

  These Beats allow us to collect the following information from each machine:
  - Filebeat: Filebeat detects changes to the filesystem. Specifically, we use it to collect Apache logs.
  - Metricbeat: Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics.
<br>
<br>

### Using the Playbook

  In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

  SSH into the control node and follow the steps below:
  - Copy the playbooks .yml file to Ansible Control Node.
  - Update the hosts file to include the service for both Filebeat and Metricbeat.
  - Run the playbook, and navigate to ELK-Server to check that the installation worked as expected.
  - To verify ELK is running in a web browser navigate to (http://"elk machines IP":5601). This is the address of Kibana.