# readme.md
**Title:** ELK Stack Project 

**Task:** Build a log management platform using the open-source Elasticsearch, LogStash, Kibana ("ELK") Stack tools. 

**Document Contents:** 
- Criteria
- Summary
- Functionality
- Design
  - Topology
  - Access Policies
  - ELK Configuration
  - Target Machines and Beats
- Tech Stack

**Criteria:** 
- Set up a virtual private cloud network.
- Protect the cloud network with a firewall.
- Deploy a virtual computer(s) to the cloud network that will be a JumpBox and Provisioner.
- Access the entire VNet from the jump box.
- Install and run containers using Docker.
- Set up Ansible connections to VMs inside the VNet.
- Write Ansible playbooks to configure VMs.
- Create a load balancer on the Azure platform.
- Create a firewall and load balancer rules to allow traffic to the correct virtual machines.
- Verify redundancy by turning off one or more virtual machines used in the infrastructure.
- Deploying containers using Ansible and Docker.
- Deploying Filebeat using Ansible.
- Deploying the ELK stack on a server.
- Diagramming networks and creating a README.

**Summary of the ELK Stack:** 
The ELK Stack is comprised of **E**lasticSearch, **L**ogStash, and **K**ibana. ElasticSearch is used for collecting and centrally storing logs, LogStash is used for indexing, processing, and storing logs, and Kibana is a web interface used for visualizing the logged data in real-time. Centralizing log data allows for easy searches, early detection, and isolation of IT issues, as well as troubleshooting applications and servers. In more advanced instances, ELK stack can be used for web analytics and data that provides actionable information for a business. In addition, Beats will be added to the ELK stack. Beats allow us to collect the various information. In particular, Filebeat monitors logs files of a machine and ships that log data, in order to centralize the information. This log data can include logons, or other file system information. While, Metricbeat is set up to ship machine metrics like CPU usage, memory, and file system information, to a centralized location.

**Design:** 

Topology:
The files in this repository were used to configure the network depicted below.

![Image](/images/Topology.JPG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML files may be used to install only certain pieces of it, such as Filebeat.

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
 
Load balancing ensures that the application will be highly accessible and responsive, in addition to restricting traffic to the network.

Load Balancers automatically distribute the "load" of the traffic between servers. Load Balancers are situated between clients and servers and can greatly increase security and performance.
Load Balancers protect the availability of assets, by distributing traffic between servers, the Load Balancer is ensuring that no one server is overloaded by traffic, which then, in turn, ensures that the server's applications and websites are responsible and available for users. Specifically, Load Balancers protect from DOS attacks.
The advantages of a Jump Box are that they are a connection point for administrators, it is a secure computer that is used to be the first connection point before connecting to the other components of a Network and/or carrying out administrative tasks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.

The configuration details of each machine may be found below.
 
```html
| Name     | Function         | IP Address               | Operating System |
|----------|------------------|------------              |------------------|
| Jump Box | Gateway          | 10.0.0.4                 | Linux            |
| Web1     | Server           | 10.0.0.7/52.143.104.97   | Linux            |
| Web2     | Server           | 10.0.0.8/52.143.104.97   | Linux            |
| Web3     | Server           | 10.0.0.9/52.143.104.97   | Linux            |
| ELK VM   | Configuration VM | 10.1.0.4                 | Linux            |

```


Access Policies: 

The machines on the internal network are not exposed to the public Internet.
 
Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the Host Machine. 

Machines within the network can only be accessed through the ansible container, via the JumpBox.

The ELK VM specifically is only accessible through SSH and port 22 via the JumpBox VM and through port 5601 from the Host Machine. 

A summary of the access policies in place can be found in the table below.
 
```html
| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 99.155.244.198       |
| Web1     | No                  | 10.0.0.4             |
| Web2     | No                  | 10.0.0.4             |
| Web3     | No                  | 10.0.0.4             |
| ELK VM   | Yes                 | 99.155.244.198       |
 

```

ELK Configuration: 

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because configuration with Ansible include that all actions are carried out on the command line via SSH, it greatly simplifies configuration and set up because using Ansible allows administrators to ensure that the configuration of the infrastructure is identical where it needs to be, and it can be run from one machine and then pushed to thousands-- meaning that it is incredibly powerful in centralizing the management and set up of machines.

The ELK playbook implements the following tasks:
- Install Contain
- Install Docker
- Install Python
- Add Python to Docker
- Start Docker
- Specify the amount of memory to be used
- Download and start Elk container -- Specify ports and restart policy
The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.


![Image](https://www.dropbox.com/s/s5kux32tjntbka1/rJHPJ-Igv_H1JWVQLgD.jpeg?dl=1)

Target Machines and Beats:

This ELK server is configured to monitor the following machines:
- Web 1 - 10.0.0.7
- Web 2 - 10.0.0.8
- Web 3 - 10.0.0.9
 
We have installed the following Beats on these machines:
- Filebeat 
- Metricbeat 
Using the Playbook: 

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
 
SSH into the control node and follow the steps below:
- Update the filebeat.yml file to include elk server private IP to the document where specified. 
- Run the playbook, and navigate to the Kibana page to check that the installation worked as expected.\
- Copy the filebeat.yml file to /etc/ansible/roles
- By configuring the host.yml file, this is a way of maintaining different IP addresses and names of different machines, this then allows for specifying which machine to install the ELK server on is specified in the playbook. 
- To navigate to the ELK server, in order to check that is running, is:
  - http://[ELK.VM.PUBLIC.IP]:5601/app/kibana 
**Tech Stack:**

```html
| Program    | Version |
|------------|---------|
| Docker     | 19.03.6 |
| Ansible    | 2.9.2   |
| Filebeat   | 7.4.0   |
| Metricbeat | 7.4.0   |

```








