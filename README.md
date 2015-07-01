## OWL Local Environment Setup Guide (BOXEN)

* [Generate SSH keys](#genarate_SSH) 
* [Fork Repos and Join the DandB Org](#fork_repo)
* [Configure OWL Local Application Configuration File](#config_OWL)
* [Fork and Run Boxen](#fork_boxen)
* [Run Composer](#run_composer) 
* [Restart Apache and Test](#restart_apache)
* [Setup PHPStorm](#setup_PHPStorm)
* [Using Postman](#postman)
* [Database Access Setup (with SQuirreL SQL)](#database_access_setup)
* [Preparing to Use Bottle](#preparing_to_use_bottle)

[You might also be interested in... ](#also_interested_in)

------------------------------------------------------------------------
#### <a name="genarate_SSH"></a>

#### 1. Generate SSH Keys
* Add SSH Key to GitHub. Go to https://help.github.com/articles/generating-ssh-keys/  
* Submit your public key to the help desk to be added to Active Directory.   
* Make a HelpDesk ticket at: https://dandbhelpdesk.zendesk.com/
#### <a name="fork_repo"></a>

#### 2. Fork Repos and Join DandB Org
* Generate OAuth token from GitHub:  
  * https://help.github.com/articles/creating-an-access-token-for-command-line-use/  
* Set Up Jenkins jobs: To be done by IMG
  * Visit https://ci.malibucoding.com/job/add_new_dev/  
  * Enter GitHub username, Teams, and Role  
  * For fOWL the teams will be 'PULL-ONLY, FOWL'  
  * Click Build  
* Visit https://ci.malibucoding.com/job/Accept_Org_Fork_New_Dev_Repos
  * Enter your GitHub username, OAuth Token (New Devs), and list of Repos you would like to fork.
  * For fOWL the repos you will need will be 'fowl, phoenix, salt-config, jenkins-jobs'
  * Click Build  

For information on how to setup and sync forked repos see :  
 * https://help.github.com/articles/configuring-a-remote-for-a-fork  
 * https://help.github.com/articles/syncing-a-fork  

#### <a name="config_OWL"></a>  
#### 3. Configure OWL Local Application Configuration File  
Update /etc/apache2/extra/dev_db.include with <username> and <password> and ensure entries match existing file.  
[OWL Setup Guide - dev_db.include](#setup_OWL)  
 
#### <a name="fork_boxen"></a>
 
#### 4. Fork and Run Boxen  

Forking this repo will be handled above when accepted into DandB GitHub  
Fork the following repo: https://github.com/taoistmath/USSBoxen  
Open Terminal and run the following commands:  
\<team\> can be any of the following: fowl, phoenix, helios, automation  
(fowl includes phoenix, helios includes verified and mycredit, and automation includes helios and fowl)

> sudo mkdir -p /opt/boxen &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//Do not copy this line! You have to type it!  
sudo chown ${USER}:staff        /opt/boxen  
git clone git@github.com:<github_username>/USSBoxen.git /opt/boxen/repo  
cd /opt/boxen/repo  
git remote add upstream git@github.com:taoistmath/USSBoxen.git  
./script/boxen --no-fde &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//This step will ask for sudo pw, github login, and github pw  
source /opt/boxen/env.sh &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//This step will load Boxen's environment  
boxen --srcdir ~  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//This step set your source directory to your home directory  
source /opt/boxen/env.sh &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//This step will reload Boxen's environment  
./script/boxen --no-fde <team> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//This step will set up apache files and clone your repos


#### <a name="run_composer"></a>

#### 5. Run Composer

###### Directions for Running Composer
 * Navigate to the root of the fOWL repo.  
 * If this is the first time you've pulled fOWL, run composer install.  
 * From time to time, you'll need to run composer update as libraries get updated.  
*Note: it may show warnings when running the install. This is most likely due to updates being available for the libraries, but have not been pulled yet.*

###### What is Composer? 
Composer is a PHP package manager. It allows your app to only contain the code that you're building within version control, and let outside libraries be added in when necessary. In addition, it provides autoloading of those libraries, making the process of adding things painless, simple, and easy.   
A good reference for packages we can add and install are listed below: 
 * https://packagist.org/

#### <a name="restart_apache"></a>

#### 6. Restart Apache and Test

`#####sudo apachectl restart`

visiting fowl.local/status should yield

#### <a name="setup_PHPStorm"></a>

#### 7. Setup PHPStorm

##### OWL Setup Guide - PHPStorm

* Running PHPUnit through PHPStorm requires PHPStorm 8
* In PHPStorm preferences assign PHP54 as your interpreter and provide the path to vendor in your include path:
* and setup PHPUnit config files. NOTE: You must change PHPUnit library to use the custom loader specified below:

#### <a name="postman"></a>


#### 8. Using Postman
* Postman is a Chrome extension that helps you be more efficient while working with APIs  
* Postman has been bookmarked in Chrome and is also available at chrome-extension://fdmmgilgnpjigdojojpjoooidkmcomcm/index.html  
* Now you can have a small, manageable, set of collections that work in each environment!
Note: the access tokens are attached and will expire, you can easily update them in Postman.

#### <a name="database_access_setup"></a>

#### 9. Database Access Setup (with SQuirreL SQL)  

 * For most purposes, the database can be accessed in SQuirreL SQL without the need for a more complicated virtual machine setup.  
 * Launch SQuirreL SQL.  
 * In the Aliases pane, edit the 4 aliases and add your Active Directory credentials:  
 

For Example:


| Field         | Value                                                             | 
| ------------- |:-----------------------------------------------------------------:| 
| Name          | DEV dbcc_ecomm                                                    | 
| Driver        | jTDS SQL Server                                                   |  
| URL           | jdbc:jtds:sqlserver://10.26.34.100:63695;DOMAIN=CREDIBILITY;      |  
| Username      |  your AD credentials                                              |  
| Password      | your AD credentials                                               |  


#### <a name="preparing_to_use_bottle"></a>

##### 10. Preparing to Use Bottle  
For more information regarding Ship In A Bottle (SIAB) please see the following documentation:  
[Ship in a Bottle - Deployment Guide](#ship_a_bottle)

`cd ~/projects/salt-config  
vagrant status  
vagrant up saltmaster`
 
#### <a name="also_interested_in"></a>

#### 9. You might also be interested in...  
* [OWL Logging on Mac OSX](#OWL_logging_MAC)  
PHPStorm / PHP Storm Keys  
tunnelblick (for vpn)  
Alias Shortcuts - Improve Efficiency  
iTerm2  
Zshell



-----------------------------------------------------------------------
#### <a name="setup_OWL"></a>
#### OWL Setup Guide - dev_db.include  

`dev_db.include`
______________

 #=== Environment for DEVELOPMENT website
SetEnv  dandb_env  qa
 
#### Required Environment variables below.  

SetEnv  api_env  dev  
SetEnv  SLIM_MODE development  
SetEnv  linked_server_name:   LNK_SRV_PHX.dbcc_ecomm  
SetEnv  owl_db_host:          10.24.34.100:63695  
SetEnv  owl_dbsvc_host:       10.24.34.100:63695  
SetEnv  owl_beo_master_host:  10.24.34.100:63662  
SetEnv  owl_db_name:          dbcc_ecomm  
SetEnv  owl_db_user:          CREDIBILITY\\ \<username\>  
SetEnv  owl_db_pass:          <font color="green"><\<password\> <\font>  
SetEnv  es_admin_user:        es_admin  
SetEnv  es_admin_password:    Dandb123  
SetEnv  alibaba_des_key:      64531111  
SetEnv  alibaba_key:          645311  
SetEnv  alibaba_secret:       SPiX5emH98q

#### IP Restriction configs  
SetEnv  ip_list_malibu       38.122.108.88/30  
SetEnv  ip_list_vpn          10.42/16  
SetEnv  ip_list_alibaba      119.38.217.0/24  

SetEnv owl_es_host1          10.26.125.50  
SetEnv owl_es_host2          10.26.125.40  
SetEnv owl_es_port           80  
SetEnv owl_es_index          verify_index  
SetEnv owl_xaction_host      10.24.34.20

#### # === Put production GA account below  
SetEnv  dandb_ga_acct  UA-19892859-2  
SetEnv  bizdir_ga_acct  UA-19892859-3  
SetEnv JSONRPCAPIHOST qa.malibucoding.com

#  
#### # === Database connection info  
SetEnvIf Host "^(dev|qa).shamrock" db_type=mssql  
SetEnvIf Host "^(dev|qa).shamrock" db_host=10.26.34.100  
SetEnvIf Host "^(dev|qa).shamrock" db_name=shamrockdb_qa  
SetEnvIf Host "^(dev|qa).shamrock" db_user=shamrockuser  
SetEnvIf Host "^(dev|qa).shamrock" db_pass=DbCC@D@ndB!  

#  
#### === PHX Encr. Keys  
SetEnv encryption_key iSOrzgVSht5jStfy0AKBcg  
SetEnv encryption_iv MWFiM2Q4ZjZkMmUyYTdmZA  
SetEnv owl_s3_key        AKIAI57YM2BNLHDBNAUA  
SetEnv  owl_s3_secret    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  

#### These values can be anything, as they are not used locally  
SetEnv urbanairship_key 1  
SetEnv urbanairship_secret 1


--------------------------------------------------------------------------

`TODO: Pulled from the BOXEN Setup Guide. Need to combined this with the above.`   

#### === Environment for OWL DEVELOPMENT website  

SetEnv  dandb_env  qa  
SetEnv  dandb_env  dev  

#### Required Environment variables below.  

SetEnv  api_env dev  
SetEnv  SLIM_MODE development  
SetEnv  linked_server_name  LNK_SRV_PHX.dbcc_ecomm  

SetEnv  owl_db_host         10.24.34.100:63695  
SetEnv  owl_db_name         dbcc_ecomm  
SetEnv  owl_db_user         CREDIBILITY\\ \<username\>  
SetEnv  owl_db_pass         \<password\>  

SetEnv  owl_beo_master_host 10.24.34.100:63695  
SetEnv  owl_dwalerts_host   10.24.34.100:63662  
SetEnv  owl_dbsvc_host      10.24.34.100:63695  

SetEnv  es_admin_user       es_admin  
SetEnv  es_admin_password   Dandb123  

SetEnv  alibaba_des_key     64531111  
SetEnv  alibaba_key         645311  
SetEnv  alibaba_secret      SPiX5emH98q  

SetEnv  ip_list_malibu      38.122.108.88/30  
SetEnv  ip_list_vpn         10.42/16  
SetEnv  ip_list_alibaba     119.38.217.0/24  
SetEnv  ip_list_yext        54.208.79.152,54.208.190.198,64.74.243.96/27,74.201.136.192/26,152.179.207.6,206.71.246.50,206.71.250.80/29,202.124.144.66,202.124.144.228  

SetEnv  owl_es_host1        10.26.125.50  
SetEnv  owl_es_host2        10.26.125.40  
SetEnv  owl_es_port         80  
SetEnv  owl_es_index        verify_index  
SetEnv owl_xaction_host     10.24.34.20  

SetEnv  salesforce_password  Pass@123LrxEmu73mTdZlBLwlxDn8rYV4  

SetEnv yext_api_key 5e4d3c2b1a  

SetEnvIf Host "^(dev|qa).shamrock" db_type=mssql  
SetEnvIf Host "^(dev|qa).shamrock" db_host=10.26.34.10  
SetEnvIf Host "^(dev|qa).shamrock" db_name=shamrockdb_qa  
SetEnvIf Host "^(dev|qa).shamrock" db_user=shamrockuser  
SetEnvIf Host "^(dev|qa).shamrock" db_pass=DbCC@D@ndB!  

SetEnv owl_s3_secret      0TN/nTZTC76F0N8OVaDMHxYxKYeO6HYSI38woSnD  
SetEnv owl_s3_key         AKIAI57YM2BNLHDBNAUA


--------------------------------------------------------------------------------
#### <a name="ship_a_bottle"></a>
#### Ship in a Bottle - Deployment Guide


#### Summary  
This guide serves to assist in explaining what is Ship In A Bottle (SIAB), how to deploy it, how to deploy your applications to SIAB, and some common troubleshooting techniques that are inherently related to dealing with SysAdmin responsibilities.

##### What is Ship In A Bottle?  

* At a high level, SIAB combines several existing technologies to help programmatically deploy an environment onto your physical machine where you can then deploy your applications. 
* In short, SIAB gets you, as close as reasonably possible, the environment that makes up Production. 
* Today, this includes: front end (nginx), load balancer (HAproxy), nfs, queue (hornetQ), PHP Application server, Java Application server, and Java Utility server. 
* You will still be connecting to the QA database on AWS.
* More in-depth, SIAB leverages Salt-stack, VirtualBox, Vagrant, and various shell scripts to wire everything up.

##### What is Salt-stack?  

Salt, in a nutshell, relies on remote execution. Deployment of salt includes a "master", and one or more "minions". The minions and master establish a relationship that allows the master to execute commands remotely on the minion.  

On top of this remote execution foundation, Salt allows the SysAdmin team to maintain configuration of various server types, e.g., load balancer, Java and PHP application servers. These configurations are version controlled. Like other programming languages, writing Salt configs requires specialized knowledge. The configurations allow for SysAdmin to configure a new server programmatically, reducing errors related to the manual configuration process.  

> * The following command will send the command "state.highstate" to the server named "php".  
* This basically tells the "php" server to pull configurations from master, and configure itself.
root@saltmaster$ salt php state.highstate


##### What is VirtualBox? 

Modern computer systems are so powerful that most of the time, it is underutilized. Try launching "Activity Monitor", click on the CPU tab, and take note the "Idle" value.

# Image

Virtualization was developed to better take advantage of these idle resources. VirtualBox is an application that allows you to create, or "provision", virtual computers within your physical computers. VirtualBox creates "containers" for your virtual computers to live. By running multiple virtual machines on your physical, or host, machine, you are better utilizing those idle resources.  
In addition to a GUI application, VirtualBox also comes with a set of command-line utilities that allow for the ability to programmatically provision virtual machines. This is where Vagrant comes into play.

##### What is Vagrant?  

Essentially, Vagrant is a command-line Ruby application that parses a set of configurations, leverages those VirtualBox command-line utilities, to provision virtual machines for you! There's no need to go to the GUI to do this. The configurations have already been created for you.

##### All Together Now!  

The combination of Vagrant and Salt-stack configurations allow for the systematic and programmatic provisioning of a Production like environment on your physical machine. All together now, this is Bottle!

##### Expectations & Assumptions  
Joining DandB, one of the fundamental expectations of you is to become a full stack developer. What does this mean? It means that you are not only expected to understand the programming languages required to develop web applications, you will also eventually need to understand various database optimization techniques, as well as support the underlying infrastructure that your applications rely on. You'll have to learn some DBA/DBE knowledge. For Bottle, you'll have to learn some Linux SysAdmin knowledge too.

##### Prerequisites  

* Github account and access to dandb/salt-config  
* Understand how to clone repositories  
* TunnelBlick installed for VPN access  
* Valid VPN account to connect to the database  
* Install  
  * ~~brew (http://brew.sh/)~~  
  * VirtualBox (4.2.18) - (OSX - http://download.virtualbox.org/virtualbox/4.2.18/VirtualBox-4.2.18-88780-OSX.dmg)  
    * Also here: //Technology File Share/software/VirtualBox/OS X  
  * VirtualBox Extensions (4.2.18)-http://download.virtualbox.org/virtualbox/4.2.18/Oracle_VM_VirtualBox_Extension_Pack-4.2.18-88780.vbox-extpack  
    * Also here: //Technology File Share/software/VirtualBox/OS X  
  * Vagrant (1.2.7) - (OSX - http://files.vagrantup.com/packages/7ec0ee1d00a916f80b109a298bab08e391945243/Vagrant-1.2.7.dmg)  
    * Also here: //Technology File Share/software/vagrant
 

#### Deployment Steps  

#####Configuring Your Hosts Environment  
Modify your /etc/hosts file and add the following entries.

 > 184.72.43.112   config  
192.168.56.110  bottle.malibucoding.com  
192.168.56.111  mycr-bottle.malibucoding.com  
192.168.56.112  api-bottle.malibucoding.com  
192.168.56.120  cms-bottle.malibucoding.com  
192.168.56.185  tar-bottle.malibucoding.com  
192.168.56.175  jehp-bottle.malibucoding.com

##### Fork it  

Fork your own copy of saltconfig  
* Go here https://github.com/dandb/salt-config  
* Click "Fork" on the top right of the page   
* Fork it to yourself

##### Pull The Code  

Now clone the forked repo by either copying/pasting the git clone URL into terminal or   
Use the command below and edit it so that you are using your own forked repo.

> `dev@local$ git clone git@github.com:<your-repo>/salt-config.git`

##### Pre-Do-Work-Son!

> You will ALWAYS need to be at the directory with Vagrantfile   
> dev@local$ cd /<path to>/salt-config/
 
> This will give you a list of commands to reference   
> dev@local$ vagrant help

Once inside this directory, there are several commands that you can use to bring various parts of your local Bottle environment up or down.

##### Vagrant Commands  

**Vagrant status**  
This lists all of the available pre-configured machines within the Bottle environment. The column on the left are the names of virtual machines which you will reference with various vagrant commands. The column on the right indicates the virtual machine's current state.

> dev@local$ vagrant status  
Current machine states:    
saltmaster &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; not created (virtualbox)  
front &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;not created (virtualbox)  
lb   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; not created (virtualbox)  
nfs  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; not created (virtualbox)  
php  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; not created (virtualbox)  
phoenix    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; not created (virtualbox)  
phoenixutils&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;not created (virtualbox)  
queue &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;not created (virtualbox)  
mmonit  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                  not created (virtualbox)  
solr                      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;not created (virtualbox)  
logs                 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;     not created (virtualbox)  
openvpn               &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    not created (virtualbox)  
This environment represents multiple VMs. The VMs are all listed  
above with their current state. For more information about a specific VM, run `vagrant status NAME`. 

**vagrant up**  
> This will either create a new, or fire up an existing virtual machine. In this example, we're creating the front end server.
> dev@local$ vagrant up front  

> TIP: You can reference serveral machines with the 'vagrant up' command. Note they are SPACE separated.
> dev@local$ vagrant up front lb nfs queue php phoenix phoenixutils  

> TIP/WARNING: Running the following command alone will fire up ALL of your virtual machines. This is not advised unless you know what you're doing.
> dev@local$ vagrant up

**vagrant ssh \<virtual machine name\>**  

This SSH you into the virtual machine. Vagrant has configured a special network adapter that makes it possible for vagrant to talk to your virtual machine to allow this to happen. Note, if you ever SSH into the "external" IP address with the user vagrant, the password is also vagrant.  

**vagrant suspend**  

Rather than shutting your virtual machines down with "vagrant halt", you can suspend them, and put them in the "saved" state. This is basically standby. TIP: You should suspend them in reverse order.  

**vagrant destroy**  

This will shutdown and destroy your virtual machine. Completely.

##### Salt-Minion Commands From Inside Minion Virtual Machines  
These commands are ONLY called from salt-minions. You DON'T need to call this command from "saltmaster".  


**salt-call -l debug state.highstate**
>  * In this example, we have already "vagrant ssh nfs". From the terminal on "nfs", we have also "sudo -i".  
 * Note: You will need to do this for all minions you SSH into: "sudo -i".  
 * The following command basically tells the salt-minion on "nfs" to pull configurations down from "saltmaster".  
 * You will see a LONG series of logging statements that "walk" you through the process as salt-minion is configuring this server.  
 * You will also see errors (in red) that are not pertinent. This list is not inclusive, but ignore errors relating to: New Relic, Munin and monit.  
 * The "-l debug" flag basically tells salt-minion to be more verbose.  
 * "state.highstate" is a Salt specific command.  
 root@nfs$ salt-call -l debug state.highstate
 
 
##### Salt-Master Commands From Inside Saltmaster Virtual Machine 

These commands are ONLY called from within "saltmaster".
> From your local laptop  
dev@local$ vagrant ssh saltmaster  
vagrant@saltmaster$ sudo -i  
root@saltmaster$

#Image

**salt-key**  

The communication between master and minions need a secure way to communicate. Part of this process is establishing a key on master. The commands help you list and troubleshoot. A valid key allows you to also execute remote calls on minions.

> This will list ALL of the keys  
root@saltmaster$ salt-key
# Image

Sometimes you need to delete the keys when you aren't able to "communicate" with a particular minion from the server via Salt
> This deletes a key. Sometimes you will need to do this if communication between master and minion doesn't seem to be working.
> root@saltmaster$ salt-key -d <virtual machine name>  

>After deleting the key from the server, you will need to restart the minion on the client. Two ways to do this.
> root@nfs$ service salt-minion restart  

>OR just restart the server altogether
> root@nfs$ shutdown -r now  

>When the server comes backup, try the following command.  
>In this example, you're basically send the command 'hostname' to the virtual machine 'nfs' from 'saltmaster'.  

root@saltmaster$ salt -L nfs cmd.run 'hostname'
# Image

##### Do-Work-Son!  
The following sections are in a specific order. You should follow them in this order.  
* ...in knowing the order and understanding how everything works, you can omit front and lb. stick to nfs and php, and make sure your local hosts file is correctly pointing to the PHP app server, NOT the front, which shouldn't exist.  
* up stuff in a given order  
* highstate stuff  
* turn off firewall
 
##### Helpful tips

* ORDER of state.highstate.  
* salt key  
* salt -L nfs,php cmd.run 'hostname'  
* service iptables off  
* vagrant up. sudo -i.
  * turn off filewall
  * test script
  * tip on why suspend them in reverse order. there are dependencies of up...on NFS and queue.....  
* Shortened Installation Guide  
* See README file at https://github.com/dandb/salt-config/tree/release-next/work_servers

----------------------------------------------------------------

#### <a name="OWL_logging_MAC"></a>
#### OWL Logging on Mac OSX

##### Logging:  

To watch logs locally on Mac OSX, you must add the following to your /etc/syslog.conf file:

` user.*                                          /var/log/messages`

Then run the following commands to restart the syslog service:

> $ sudo launchctl unload /System/Library/LaunchDaemons/com.apple.syslogd.plist
> $ sudo launchctl load /System/Library/LaunchDaemons/com.apple.syslogd.plist

Now, when running the application, you can tail /var/log/messages as follows:

> tail -f /var/log/message -f /var/log/apache2/error_log
