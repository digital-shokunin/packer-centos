These [packer](http://packer.io) templates are used to build "latest and greatest" [vagrant](http://vagrantup.com) boxes for [{new context}](http://www.newcontext.com) local development. The templates will build boxes for both VirtualBox and VMware Fusion, installing the latest set of vmtools respectively. They are to generate both minimal-OS (base) boxes in addition to boxes with Chef pre-installed.


## Pre-Built Boxes

If you don't want to rebuild, I've got a collection boxes built using these templates already available for use: 

### VirtualBox (4.3.4)

* [CentOS-6.4-x86_64](https://www.dropbox.com/s/ov6t1hqshy75bu8/centos64-base.box) - CentOS 6.4 (x86_64) 
* [CentOS-6.4-x86_64-chef](https://www.dropbox.com/s/vz7krnaiyo6nv4y/centos64-chef.box) - CentOS 6.4 (x86_64) + Chef 11.8.2 
* [CentOS-6.5-x86_64](https://www.dropbox.com/s/emsts40bxz5fejx/centos65-base.box) - CentOS 6.5 (x86_64) 
* [CentOS-6.4-x86_64-chef](https://www.dropbox.com/s/k4fkv0kplmuxxfe/centos65-chef.box) - CentOS 6.5 (x86_64) + Chef 11.8.2 


### VMware (6.0.2)

* [CentOS-6.4-x86_64](https://www.dropbox.com/s/pc38vrba611l936/centos64-base.box) - CentOS 6.4 (x86_64)
* [CentOS-6.4-x86_64-chef](https://www.dropbox.com/s/859oxvbqd824gun/centos64-chef.box) - CentOS 6.4 (x86_64) + Chef 11.8.2
* [CentOS-6.5-x86_64](https://www.dropbox.com/s/i33d9yh40a1xu9z/centos65-base.box) - CentOS 6.5 (x86_64)
* [CentOS-6.4-x86_64-chef](https://www.dropbox.com/s/tbuk5ts2txlxomp/centos65-chef.box) - CentOS 6.5 (x86_64) + Chef 11.8.2



## How do I use this?

If you want to rebuild these boxes for any reason, packer is very easy to use. First, install [packer](http://packer.io). On a Mac, it's easiest to install it via [Homebrew](http://brew.sh):

	$ brew install homebrew/binary/packer


Verify it installed properly:

	$ packer -v
	Packer v0.4.1


You'll obviously need a copy of this repository:

	$ git clone https://github.com/newcontext/packer-centos


Creation of base boxes is as straightforward as:

	$ packer build templates/centos64.json


This will build CentOS 6.4 base boxes for both Virtualbox and VMware. How about building only for virtualbox, you ask?:

	$ packer build -only=virtualbox templates/centos64.json


Building boxes with the latest Chef?:

	$ packer build -var "provisioner=chef" -var "provisioner_version=latest" templates/centos64.json


What if that last run fails to build a VMware box properly?:

	$ packer build -var "provisioner=chef" -var "provisioner_version=latest" -only=vmware templates/centos64.json


Need an older version of Chef installed?:

	$ packer build -var "provisioner=chef" -var "provisioner_version=11.6.2" templates/centos64.json

*IMPORTANT*: The version specified must still be avialable for download from the Chef website.


In all build scenarios, successfully packed boxes will be stored in _boxes/virtualbox/_ or _boxes/vmware/_.

