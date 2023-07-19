FABRIC Interaction and Resources

Section 1: Get Started

Signing up for a FABRIC account (For detailed view click on the heading)
a. Navigate to the FABRIC portal at https://portal.fabric-testbed.net/.
Make sure you accept the cookie policy. Skipping the cookie policy will prevent you from enrolling.
Then click the “Sign up” button in the upper right corner of the browser window. This will take you to the FABRIC Sign Up workflow. Currently, FABRIC requires that you use your institutional login to login to FABRIC using a system called CI Logon.
b. The next step is to authenticate using CILogon. This step requires logging in with your institutional ID and password.
c. After successfully logging in with CILogon, you will be taken to the self-sign up workflow.
d. The system will send you an email asking for you to verify your email address. Click the link in your email. At this point, the FABRIC admins have been notified of your request. You need to wait until a FABRIC admin approves your request.
e. After receiving the FABRIC approval email, you can access FABRIC. Please return to the FABRIC portal and login. Login with your institutional ID and password.
Creating or Joining a Project (For detailed view click on the heading)
a. Creating a Project:
Only users that have been granted the role of a Project Lead can create new projects and add members into them. When creating a new project, it is important to think through its purpose and its membership as FABRIC permissions are granted on a per-project basis. Also, it is important to fill out a description for the project as those are public by default (searchable by other FABRIC users). You can select your project not to be public using checkmarks in the project ‘Basic Information’ tab.
b. Joining a Project:
Before you can use the testbed, you must join an active project. A project owner must add you to a project.
A Project Lead or a Project Owner can add new Owners and Members by first navigating to the project via Experiments/Projects & Slices or User Profile/My Roles & Projects. Using the search box, you can find the user you want to add (minimum 4 consecutive letters of email or name are required for search) and click ‘Add’ next to their name.
Generating SSH Configuration and SSH Keys (For detailed view click on the heading)
a. Creating an SSH client configuration file
To use FABRIC bastion host, you must create an SSH configuration file (regardless of whether you are working from Jupyter Hub or from your laptop or desktop).
Make sure you know your FABRIC bastion username prior to proceeding and you have generated your bastion keypair and are in possession of the private key file.
yaml
Copy code
UserKnownHostsFile /dev/null
StrictHostKeyChecking no
ServerAliveInterval 120

Host bastion.fabric-testbed.net
    User <FABRIC_BASTION_USERNAME>
    ForwardAgent yes
    Hostname %h
    IdentityFile <FABRIC_BASTION_PRIVATE_KEY_LOCATION>
    IdentitiesOnly yes

Host * !bastion.fabric-testbed.net
    ProxyJump <FABRIC_BASTION_USERNAME>@bastion.fabric-testbed.net:22
In the template above, replace the things between < > with your own values.
After you’ve done it, you can ssh to your sliver simply as ssh -F ~/work/fabric_config/ssh_config -i <private sliver key file> centos@1.2.3.4 from Jupyter Hub or ssh -F ~/.ssh/fabric_ssh_config -i <private sliver key file> centos@1.2.3.4 from your own laptop.
b. Using SSH to access your VMs
At this point, you should be ready to access your FABRIC VM slivers using the bastion host(s) from Jupyter Hub as:
ruby
Copy code
$ ssh -F ~/work/fabric_config/ssh_config -i <private *sliver* key file> ubuntu@11.22.33.44
or from your laptop:
ruby
Copy code
$ ssh -F ~/.ssh/fabric_ssh_config -i <private *sliver* key file> ubuntu@11.22.33.44
where 11.22.33.44 is the IP address communicated to you by FABRIC control framework. It can be an IPv4 or an IPv6 address – the bastion hosts will take care of necessary translations. Presumably, you used the matching public sliver key file when creating the slice via FABRIC API.
Creating your first experiment in Jupyter Hub (For detailed view click on the heading)
a. The easiest way to create experiments on FABRIC is using JupyterHub. You can create your private JupyterHub environment by logging into the FABRIC portal and clicking Links->JupyterHub
b. Login with your institutional ID and password. When you log in for the first time, a private JupyterHub environment will be built for you.
c. Your JupyterHub environment is a private container that includes a file system where you can store your FABRIC experiment notebooks. By default, FABRIC includes a set of example notebooks that demonstrate the use of the FABRIC Python API.
Creating your first slice in the Portal (For detailed view click on the heading)
a. You need to choose a project first from the Experiments page -> Projects & Slices tab. Your rights of FABRIC resources when creating a slice depend on this project’s permissions.
b. If you don’t have any slice in this selected project yet, you will see the callout message below. Click the button "Create Slice in Portal" will lead you to the portal slice builder page; Click the button "Create Slice in JupyterHub" will lead you to the JupyterHub login interface.
c. If you have slices in this selected project, you will see the slices table with filter and search. Click on the "Create Slice" button will lead you to the portal slice builder page.
Section 2: List of Assignments

Title	Description
Exploring IPV6	This module gives students an opportunity to experiment with IPv6 and examine the differences between it and IPv4.
Exploring Queues	This module explores the effects of queues on packet loss and delay using UDP traffic.
IPV4 routing	In this module, you will learn how to set up static routing with the route command.
OSPF	This module explores the OSPF routing protocol and how it dynamically routes around downed links.
Ping	Assignment details for the Ping module.
RTT and Window Size on TCP	This module allows students to experiment with how RTT and TCP window size affect TCP throughput.
TCP Traffic	This module gives students experience generating and analyzing TCP flows.
Traffic Analysis	This module introduces some key tools for network traffic analysis.
TrafficGeneration	This module introduces students to the principles of traffic generation using Tmix, a tool for generating realistic network traffic from captured packet headers.
Webserver	This module gives students hands-on experience installing and interacting with a web server.
Section 3: FABRIC Interaction and Resources

3.1 FABRIC has three ways of interacting with it:
Portal:
Manage projects
SSH keys
API tokens
Create or visualize slice topologies
Jupyter Hub:
Create Notebooks
Create Virtual Environment
Run experiments
Favourable Kernel options
We strongly recommend starting your FABRIC experiments with Jupyter Notebooks
Use FABRIC APIs:
Run from experimenter laptop or desktop
Libraries are available for download from PyPi
For more details click here: Knowledge-Base

3.2 The types of resources FABRIC offers are:
FPGA
Disk (GB)
Support for P4 switches
RAM (GB)
GPU
NVME
Cores
SmartNIC
SharedNIC
For detailed Testbed Resource Summary click here: Resources

3.3 Resources are Mapped into VMs:
FABRIC provides Virtual machines of different sizes (up to 64 cores, 384G RAM) with directly attached PCI devices
VMs can be placed at the sites of your choice and interconnected by a rich set of on-demand Layer 2 and Layer 3 network services
VMs are arranged in network topologies.
VMs can have large storage volumes attached to them
VMs or slivers are arranged in slices representing individual experiment topologies. Slices can be created, modified, and deleted.
Slices have a finite lifetime, but can typically be extended before they expire
FABRIC Slices can connect to other testbeds or facilities using Facility Ports
3.4 Slice States
There are 6 types of states for a slice.

For Configuring slices, wait until the Slice is in either StableOK or StableError to access resources.
For StableError slices, the specific failure can be found by looking at each specific Sliver.
Slice will go to Closing state and then transits to Dead when the user triggers a delete or the requested resources are not available.

State	Introduction
Nascent	Indicates a new slice which has just been created
Configuring	Indicates a slice which has slivers being ticketing/ticketed at the Broker or redeeming at the Site
StableOK	Indicates a slice which has slivers either in Active or Closed state
StableError	Indicates a slice which has slivers either in Active, Closed, or Failed state
ModifyOK	Indicates a slice which was modified successfully and has slivers in Active or Closed state
ModifyError	Indicates a slice which was modified partially successfully and has slivers in Active, Closed, or Failed state
