## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK Diagram](https://github.com/MichaelSotelo/ElkStackProject/blob/main/Diagrams/elk%20diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

## Playbook File
 
![Ansible Playbook File](https://github.com/MichaelSotelo/ElkStackProject/blob/main/Ansible/my-playbook.yml)
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

What aspect of security do load balancers protect? 

Load Balancers protect against denial of service attacks (DDoS) by analyzing traffic, a load balancer can determine which server receives the traffic. This prevents lone server overload by allowing traffic to be distributed evenly among the servers. A health probe can periodically check that a machine is working correctly prior to sending traffic. If it is not working correctly, the load balancer will then divert traffic from this server until it is corrected. A jump box limits the access that the public has to your virtual network because in order to access the other virtual machines, an individual needs the private IPs of the machines. A jumpbox allows greater control over access to a virtual network and its contents.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system performance.

The configuration details of each machine may be found below.

| Name     | Function      | IP Address | Operating System |
|----------|---------------|------------|------------------|
| Jump Box | Gateway       | 10.0.0.4   | Linux            |
| Web-1    | Host for container running DVWA| 10.0.0.5   | Linux            |
| Web-2    | Host for container running DVWA| 10.0.0.6   | Linux            |
| ELK      | Monitorin and  log aggregation for hosts|    10.1.0.4        |     Linux             |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
172.58.96.76

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes              | 172.58.96.76   |
| Web-1       |  No                   | Local Vnet                      |
| Web-2       |  No                   | Local Vnet                     |
| Elk        | Yes                     |    172.58.96.76                  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for repeatable configuration, and speeds up deployment of changes. Also, in the event this environment needs updating, this code could be used to update or when creating new environments.
The playbook implements the following tasks:

* Download/Install Docker on the ELK server
* Download/Install/Start ELK on a docker container on hosted on the ELK server
* Download/Install/Start filebeat on the docker container running on each web server, forwarding logs to the ELK server
* Download/Install/Start metricbeat on the docker container running on each web server, forwarding metrics to the ELK server

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker SS](https://github.com/MichaelSotelo/ElkStackProject/blob/main/Diagrams/docker%20container.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name     | Function      | IP Address | Operating System |
|----------|---------------|------------|------------------|
| Web-1    | Host for container running DVWA| 10.0.0.5   | Linux            |
| Web-2    | Host for container running DVWA| 10.0.0.6   | Linux            |

We have installed the following Beats on these machines:
filebeat

These Beats allow us to collect the following information from each machine:
Filebeat collects linux logs. Track user logon events, failed access attempts, service start/stop

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible.cfg file to /etc/ansible
- Update host file to include the hosts that the playbook should manage
- Run the playbook /Ansible/elk.yml and navigate to your ELK server on port tcp 5601 to ensure to check that the installation worked as expected
