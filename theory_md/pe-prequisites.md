<div class="tocoutline">

### Table of Contents

<div class="toc">

- [Overview](#overview)
- [Prequisities](#prequisities)
- [Requirements](#requirements)
    - [Puppet Enterprise](#1-puppet-enterprise)
      - [CPU, memory and storage](#cpu-memory-and-storage)
      - [Operating system](#operating-system)
      - [Networking](#networking)
    - [Version Control Requirements](#2-version-control-requirements)
      - [Gitlab for Lab usage](#gitlab-for-lab-usage)
    - [Lab node Requirements](#3-lab-node-requirements)
      - [Operating system](#operating-system-1)
      - [CPU, memory and storage](#cpu-memory-and-storage-1)
      - [Networking](#networking-1)

</div>

</div>

# Overview

This page explains what’s needed for installing and using Puppet Enterprise in a lab environment.

# Prequisities

You’ll need a few things to complete the PE guide labs:

- 1x VM (running Centos 7) to host the Puppet Enterprise instance.
- 1x VM running Gitlab Community Edition or a compatible git based source control system.
- 1x VM that can be managed by Puppet Enterprise for lab purposes.

# Requirements
## 1. Puppet Enterprise 

In its simplest form, you’ll only need 1 server for Puppet Enterprise. This is called a <a href="https://puppet.com/docs/pe/latest/choosing_an_architecture.html#standard-installation" target="_blank">Standard installation</a>. Puppet refers to the central Puppet Enterprise server as the "Primary Puppet Server".

#### CPU, memory and storage

For a lab environment, the minimum requirements will suffice for a trial installation:

* 2 or more CPU cores (4 is recommended)
* 8GB of RAM
* 60GB of total disk space

More detailed system requirements are documented <a href="https://puppet.com/docs/pe/latest/hardware_requirements.html" target="_blank">here</a>.

#### Operating system

Puppet Enterprise can be installed on 3 different Linux platforms, as described <a href="https://puppet.com/docs/pe/latest/supported_operating_systems.html#supported_operating_systems_and_devices__puppet_master_platforms" target="_blank">here</a>. Puppet supports versions of Enterprise Linux (RedHat, CentOS, etc), SLES and Ubuntu as an agent or primary server platform. In general, if the OS platform versions are currently supported by their respective vendors, Puppet will also support the platform. However, we'd recommend that you review the link referenced above for up to date compatibility information.

For the entirety of this guide, we will use CentOS 7.8 (Minimal Install) as our OS of choice for Puppet Enterprise. As commands in the lab are specific to this OS, we would recommend you use the same OS (or RedHat 7.8).

#### Networking

Puppet exposes a number of endpoints, some of which your servers will need to be able to access to allow the agent to be able to connect to Puppet Enterprise. <a href="https://puppet.com/docs/pe/latest/system_configuration.html#firewall_standard" target="_blank">This diagram</a> shows all the ports that are required to be open and available for a standard installation as well as a detailed explanation of their functions within Puppet Enterprise.

We've also provided a high level overview of those ports and their key functions below:

| Source       | Target            |  Port         |    Reason                                                    |
| -----------  | -----------       |-------------    |-----------                                                   |
| Agents       | Primary Server | TCP 8140      | Retrieval of configuration code                              |
| Agents       | Primary Server | TCP 8142      | Listen for Tasks/Plans or ad-hoc Puppet runs to execute      |
| Primary Server     | Primary Server Replica | TCP 5432      | Used to replicate DB data between the primary server and replica  	                                |
| Git Server   | Primary Server | TCP 8170      | Webhook to trigger PE to retrieve updated configuration code |
| IT Admin/Git Server      | Primary Server | TCP 22      | SSH access for pulling code from the git server and logging into the Puppet server vm                                    |
| IT Admin     | Primary Server | TCP 443       | Access to the PE web console                                 |
| IT Admin     | Primary Server | TCP 4433      | API endpoint for Node groups                                 |
| IT Admin     | Primary Server | TCP 8081      | API endpoint for PuppetDB                                    |
| IT Admin     | Primary Server | TCP 8143      | The Orchestrator client uses this port to communicate with orchestration services running on the primary server                                   |


Please ensure any firewalls allow these types of communication.

>  Replica configuration is not part of this guide.


## 2. Version Control Requirements
In the <a href="https://kinners00.github.io/puppet-enterprise-guide/labs/lab-set-up-the-control-repo.html" target="_blank">Set up the control repo lab</a> later in the guide, you’ll create a central repository for all your configuration and automation content. In Puppet jargon, this is called a control repo. To house this repository, you should use a version control system such as Gitlab, Github, BitBucket or Azure DevOps. 

> The guide will assume you are using Gitlab Community Edition server

You may use another version control system for the labs in this guide however, you will need to substitute some of the configuration steps for your chosen source control provider. 


#### Gitlab for Lab usage

If you don’t have a version control system available, we would recommend you use an onprem instance running Gitlab community edition. 

To set up:

* Spin up a VM running CentOS 
* Perform steps 1-3 on <a href="https://about.gitlab.com/install/?version=ce#centos-7" target="_blank">this page</a> (for CentOS7) or <a href="https://about.gitlab.com/install/?version=ce#centos-8" target="_blank">this page</a> (for CentOS 8) to install Gitlab.

## 3. Lab node Requirements

#### Operating system

Most modern operating systems support the Puppet agent however, full details on Puppet agent platform support can be found <a href="https://puppet.com/docs/pe/latest/supported_operating_systems.html#supported_operating_systems_and_devices-supported-agent-platforms" target="_blank">here</a>

#### CPU, memory and storage

The Puppet agent is fairly lightweight, so there are no strict requirements on VM spec - as long as the VM is sized appropriately to it’s desired function, it should work just fine. For example, if you want to spin up a webserver to manage with Puppet, the VM will generally only need enough capacity to run the webserver when under load, with a small buffer of free compute and memory for Puppet and other tasks.

#### Networking

The two main ports that your lab VM should have opened are TCP8140 and TCP8142 to allow for communication between the Primary Puppet server and agent.

#### Linux
If your lab node is Linux based, you'll need open port 22 to allow for SSH access to complete some labs.

| Source       | Target             | Port          | Reason                                                                      |
| -----------  | -----------        |-----------    |-----------                                                                  |
| Agents       | Primary Server     | TCP 8140      | Retrieval of configuration code                                             |
| Agents       | Primary Server     | TCP 8142      | Listen for Tasks/Plans or ad-hoc Puppet runs to execute                     |
| IT Admin     | Linux Agents       | TCP 22        | SSH access used to log into the your lab node during several lab exercises  |


#### Windows
If your lab node is Windows based, you'll need open port 3389 to allow for RDP access to complete some labs.


| Source       | Target             | Port          | Reason                                                                      |
| -----------  | -----------        |-----------    |-----------                                                                  |
| Agents       | Primary Server     | TCP 8140      | Retrieval of configuration code                                             |
| Agents       | Primary Server     | TCP 8142      | Listen for Tasks/Plans or ad-hoc Puppet runs to execute                     |
| IT Admin     | Windows Agents     | TCP 3389      | RDP access used to log into the your lab node during several lab exercises  |
