# Overview

This lab will guide you through the process of installing Puppet Enterprise.

You'll perform the following steps:

* Download Puppet Enterprise
* Open the required firewall ports
* Perform a Basic installation of Puppet Enterprise

# Steps

**<span style="text-decoration:underline;">Step 1: Download Puppet Enterprise</span>**



1. Login to your CentOS VM (CentOS VM referenced from <a href="https://puppet.com/docs/bolt/latest/plan_functions.html" target="_blank">PE requirements</a>). in the  section of .
2. If you are not logged in as the root account, elevate to root.
   ```
   sudo -i
   ```
3. You’ll be using wget to download the Puppet Enterprise tarball so you’ll need to install it first.
    ```
    yum install -y wget
    ```
1. Now, use the following commands to download the latest available version for Enterprise Linux 7 (CentOS/RedHat).
 
    ```
    PE_VERSION=$(curl -s http://versions.puppet.com.s3-website-us-west-2.amazonaws.com/ | tail -n1)
    PE_SOURCE=puppet-enterprise-${PE_VERSION}-el-7-x86_64
    DOWNLOAD_URL=https://s3.amazonaws.com/pe-builds/released/${PE_VERSION}/${PE_SOURCE}.tar.gz
    ```
    ```
    wget --progress=bar ${DOWNLOAD_URL}
    ```


2. Unpack the tar file.
   ```
   tar zxf ${PE_SOURCE}.tar.gz
   ```

**<span style="text-decoration:underline;">Step 2: Open the required firewall ports</span>**



1. Ensure the required firewall ports are open. If you’re not running a local firewall on the VM, you can skip this step. 
    ```
    systemctl start firewalld
    ```

    ```
    systemctl enable firewalld
    firewall-cmd --zone=public --add-port=22/tcp --permanent
    firewall-cmd --zone=public --add-port=443/tcp --permanent
    firewall-cmd --zone=public --add-port=4433/tcp --permanent
    firewall-cmd --zone=public --add-port=5432/tcp --permanent
    firewall-cmd --zone=public --add-port=8081/tcp --permanent
    firewall-cmd --zone=public --add-port=8140/tcp --permanent
    firewall-cmd --zone=public --add-port=8142/tcp --permanent
    firewall-cmd --zone=public --add-port=8143/tcp --permanent
    firewall-cmd --zone=public --add-port=8170/tcp --permanent
    firewall-cmd --reload

    ```

**<span style="text-decoration:underline;">Step 3: Perform a Basic installation of Puppet Enterprise</span>**



1. Let’s start the installation!
First, let’s make sure the system locale is set to English for the install.
    ```
    export LANG=en_US.UTF-8
    export LANGUAGE=en_US.UTF-8
    export LC_ALL=en_US.UTF-8
    ```


1. Next, run the installer.
    ```
    cd ${PE_SOURCE}
    ```
    ```
    ./puppet-enterprise-installer
    ```

1. At the prompt to “Proceed with the installation”, **type Y** and **press return**. 
   
   The installer will take about 8-10 minutes to complete.
2. By default, Puppet will use the system’s fully qualified domain name (FQDN) during installation, and a number of services will be configured to connect to endpoints on this FQDN. If DNS name resolution fails to resolve your FQDN to the system’s IP address, you’ll experience unstable behavior. Make sure there is an entry in `/etc/hosts` for your FQDN. The following command is a quick way to accomplish that after the installer finishes:
    ```
    echo "$(facter ipaddress) $(puppet config print certname) $(hostname)" >> /etc/hosts
    ```
1. Now that the installer has finished, let’s set the password for the main **admin** user.
    ```
    puppet infrastructure console_password
    ```
    Follow the instructions on screen to set your password.
1. Finally, you’ll need to run the puppet agent twice to finish up the installation. Run the puppet agent as follows, and repeat it once more when finished.
   ```
   puppet agent -t
   ```
1. You can now access the Puppet Enterprise Web Console at <span style="text-decoration:underline;">https://&lt;IP address or FQDN></span> and login with username **admin** and the password you set earlier.

This lab installs Puppet Enterprise with all default settings. It means that no admin password was set during installation, and that defaults were used to generate the SSL certificates for the Web Console and all other services. As a result, the generated certificate for the Web Console is valid for the FQDN of the machine. The certificates for the TCP 8140 and TCP 8142 endpoints, to which Puppet Agents connect, are valid for both the FQDN of the machine, as well as the short name: **puppet**.

If you want to control these options (and more) at install time, you can create an installation answer file, as described [here](https://puppet.com/docs/pe/2021.2/installing_pe.html#configuration_parameters_and_the_pe.conf_file). An example answer file that sets the admin password and defines the valid names for the SSL certificates, looks like this:

_**pe.conf**_


```
"console_admin_password": "P@ssw0rd"
"puppet_enterprise::puppet_master_host": "puppet-01.company.local"
"pe_install::puppet_master_dnsaltnames": ["puppet-01.company.local","puppet.company.local"]
