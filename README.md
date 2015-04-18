# vagrant.geowave
A Vagrant environment for deploying Geoserver.

Vagrant and Ansible must be installed.
=======
# Overview

This repository can be used to set up a virtual machine environment to deploy Geoserver using Vagrant. The virtual machine will include [Geoserver](http://geoserver.org), [Apache Tomcat 7](https://tomcat.apache.org/index.html), [Apache 2](http://httpd.apache.org), [Postgresql 9.4](http://www.postgresql.org), and [Postgis](http://postgis.net).

## Installation Requirements

In order to get started with this virtual machine, some software must be installed on the host machine and the host machine must support virtualization.

### Software

#### Vagrant
[Vagrant](https://www.vagrantup.com/) (version >= 1.7.2) is required on the host to manage the virtual machine. [Binaries](https://www.vagrantup.com/downloads.html) are available for most operating systems.

#### Ansible
[Ansible](http://www.ansible.com/home) (version >= 1.8.2) is required to handle configuration of the virtual machine. Ansible is officially supported for Mac OSX and Linux host environments, though it can be used with a [Windows host machine](http://www.azavea.com/blogs/labs/2014/10/running-vagrant-with-ansible-provisioning-on-windows/). There are multiple ways to [install Ansible](http://docs.ansible.com/intro_installation.html), choose the most appropriate one for your operating system.

#### VirtualBox
[VirtualBox](https://www.virtualbox.org/) is an open source virtual software package used to handle virtual machines. There are binaries [available](https://www.virtualbox.org/wiki/Downloads) for most operating systems.

Note: It is also possible to run the virtual machine using a [Kernel Based Virtual Machine](http://www.linux-kvm.org/page/Main_Page) on Linux. This can be done using the [Vagrant Libvirt Provider](https://github.com/pradels/vagrant-libvirt). Vagrant Libvirt is still under active development and there are additional requirements if KVM is used.

### Sytem Requirements
Your host machine should have at least 6GB of memory, a modern x86-64 processor, and virtualization support must be [enabled for the processor being used](http://virt-tools.org/learning/check-hardware-virt/).

## Getting Started

1. [Clone](http://git-scm.com/docs/git-clone) this repository.

   `git clone https://github.com/stumptownlabs/vagrant-geoserver.git`

   Note: If you wish to submit patches to this repository, you should consider [forking this repository](https://help.github.com/articles/fork-a-repo/).

2. Install required software listed above

3. Navigate into the directory created by cloning `vagrant.geowave`

4. Clone Geowave from your forked repository.

   At this point, the directories in the `vagrant-geoserver` directory should look like this.
    ```
    vagrant-geoserver
    ├── ansible
    ├── README.md
    └── Vagrantfile
	```

5. In the top level directory with the `Vagrantfile` bring up the virtual machine at the command line.

   `vagrant up`

   At this point Vagrant will start the virtual machine and begin provisioning it with Ansible. Depending on internet connection speeds, installation and downloading of all dependencies could take some time.

6. Once the machine finishes provisioning, you can verify that Accumulo and HDFS are running by navigating to their web UIs.
   - Geoserver: http://localhost:8080
   
## Attribution

Adapted from original work by Chris Brown @notthatbreezy geotrellis/vagrant.geotrellis

