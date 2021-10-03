## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Images/Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the commands on the file may be used to install only certain pieces of it, such as Filebeat.

ELK.txt

This document contains the following details:
- Automated setup commands
- Configuration setup


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting access to the network.
Load balancers prevent denial of service attacks. The advantage of the jumpbox is providing a secure access to the system that can be accessed
from computers remotely.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat watches for log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing
- Metricbeat collects metric data from your target servers, this could be operating system metrics such as CPU or memory or data related to services running on the server.

The configuration details of each machine may be found below.

| Name    | Function          | IP       | Operating System |
|---------|-------------------|----------|------------------|
| Jumpbox | Gateway           | 10.0.0.4 | Linux            |
| Web1    | Host              | 10.0.0.5 | Linux            |
| Web2    | Host              | 10.0.0.6 | Linux            |
| ELKHost | Server Monitoring | 10.1.0.4 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
67.70.151.153

Machines within the network can only be accessed by SSH.
I allowed my Jumpbox to access my ELK VM, its public ip
is 13.82.58.235, and its private IP is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name    | Publicly Accessible | Allowed IP Address |
|---------|---------------------|--------------------|
| Jumpbox | Yes                 | 67.70.151.153      |
| Web1    | No                  | 10.1.0.4           |
| Web2    | No                  | 10.1.0.4           |
| ELKHost | No                  | 10.1.0.4           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
it allows for the quick and scalable configuration of systems


The playbook implements the following tasks:
- Install Docker
- Install pip3
- Install docker pyhton module
- Increase the virtual memory (Important otherwise it never works for some reason)
- Downlad and launch docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/snipsnap.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Both Metricbeat and filebeat are installed on 10.0.0.5 and 10.0.0.6

These Beats allow us to collect the following information from each machine:
- Metricbeat allows us to collect metric data such as CPU usage
- Filebeat allows us to collect log data such as audit logs, which can show which resources are being accessed

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ELK.txt file to a new playbook file in ~/ect/ansible/
- Update the ELK.yml file to include latest versions of any software being used
- Run the playbook, and navigate to  http://[your.VM.IP]:5601/app/kibana to check that the installation worked as expected.
