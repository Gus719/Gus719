## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](   https://go.gliffy.com/go/html5/13651676 )

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _yml/config____ file may be used to install only certain pieces of it, such as Filebeat.

  - _._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
-  What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load balancers proect availability, traffic and security of the web. 
A jump box offers automation, increased security and access control to an internal network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
-  What does Filebeat watch for?_Filebeat monitors specific log file or locations, collects the logs and sends them to the selected destination.
-  What does Metricbeat record?_Metricbeat records statistics called metrics, which includes data such as CPU usage and machine uptime.

The configuration details of each machine may be found below.
CONTAINER ID   IMAGE          COMMAND                  CREATED      STATUS        PORTS                                                                              NAMES
08da891ff2bb   sebp/elk:761   "/usr/local/bin/star…"   6 days ago   Up 14 hours   0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk
azureuser@Elk:~$
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

 | Name          |  Function     | IP Address    | Operating System |
|---------------|---------------|---------------|------------------|
| Jump Box      |    Gateway    |    10.0.0.7   |       Linux      |
|     Web-1     | web server    |    10.0.0.8   |       Linux      |
|     Web-2     | web server    |    10.0.0.9   |       Linux      |
|      Elk      |   ELK server  |    10.1.0.4   |       Linux      |
| Load balancer | Load balancer | 20.213.37.214 |       Linux      |
|     Laptop    |     Access    |   73.237.X.X  |      Windows     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _73.237.37.230:5601

Machines within the network can only be accessed by my laptop through the Jump box.
-  Which machine did you allow to access your ELK VM? What was its IP address?_
JumpBoxProvisioner 10.0.0.7 

A summary of the access policies in place can be found in the table below.

 |   Name   | Publicly Accessible |  Allowed IP Addresses |
|:--------:|:-------------------:|:---------------------:|
| Jump Box |          no         | 73.237.37.230:port 22 |
|   Web-1  |          no         |        10.0.0.8       |
|   Web-2  |          no         |        10.0.0.9       |
|    ELK   |          no         |        10.1.0.4       |
|    LB    | no                  | 73.237.37,230:port 80 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-  What is the main advantage of automating configuration with Ansible?_
Ansible allows automated configurations as well as reducing human errors.

The playbook implements the following tasks:
-  In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- The ELK installation playbook:
Configured the ELK VM with Docker
Installed docker.io
Installed python3
Increased the virtual memory
Downloaded and launched the docker container

- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
CONTAINER ID   IMAGE          COMMAND                  CREATED      STATUS        PORTS                                                                              NAMES
08da891ff2bb   sebp/elk:761   "/usr/local/bin/star…"   6 days ago   Up 14 hours   0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk
azureuser@Elk:~$


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-  List the IP addresses of the machines you are monitoring_
Web-1:10.0.0.8
Web-2:10.0.0.9

We have installed the following Beats on these machines:
-  Specify which Beats you successfully installed_
Filebeat and Metricbeat on Web-1, Web-2, and ELK

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects log events such as country of origen for log in attemps.
Metricbeat monitors statistics such as CPU usage


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ~/etc/ansible/files/metricbeat.yml file to /etc/metricbeat/metricbeat-playbook.yml.
- Update the metricbeat.yml file to include 10.1.0.4:9200 as hosts in output.elasticsearch and 10.1.0.4:5601 as host in setup.kibana 
- Run the playbook, and navigate to http://10.1.0.4:5601/app/kibana to check that the installation worked as expected.

 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._