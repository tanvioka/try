## OWL Local Environment Setup Guide (BOXEN)

* [Generate SSH keys](#genarate_SSH) 
* [Fork Repos and Join the DandB Org](#fork_repo)
* [Configure OWL Local Application Configuration File](#config_OWL)
* Fork and Run Boxen
* Run Composer 
* Restart Apache and Test
* Setup PHPStorm
* Using Postman
* Database Access Setup (with SQuirreL SQL)
* Preparing to Use Bottle

You might also be interested in...

------------------------------------------------------------------------
#### <a name="genarate_SSH"></a>
#### Generate SSH Keys
Add SSH Key to GitHub. Go to https://help.github.com/articles/generating-ssh-keys/  
Submit your public key to the help desk to be added to Active Directory.   
Make a HelpDesk ticket at: https://dandbhelpdesk.zendesk.com/
#### <a name="fork_repo"></a>
#### Fork Repos and Join DandB Org
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
#### Configure OWL Local Application Configuration File  
Update /etc/apache2/extra/dev_db.include with <username> and <password> and ensure entries match existing file.  
[OWL Setup Guide - dev_db.include](https://dunandb.jira.com/wiki/display/OWL/OWL+Setup+Guide+-+dev_db.include)  
 
Fork and Run Boxen
Forking this repo will be handled above when accepted into DandB GitHub
Fork the following repo: https://github.com/taoistmath/USSBoxen
Open Terminal and run the following commands:
<team> can be any of the following: fowl, phoenix, helios, automation
(fowl includes phoenix, helios includes verified and mycredit, and automation includes helios and fowl)
sudo mkdir -p /opt/boxen       //Do not copy this line! You have to type it!
sudo chown ${USER}:staff /opt/boxen
git clone git@github.com:<github_username>/USSBoxen.git /opt/boxen/repo
cd /opt/boxen/repo
git remote add upstream git@github.com:taoistmath/USSBoxen.git
./script/boxen --no-fde        //This step will ask for sudo pw, github login, and github pw
source /opt/boxen/env.sh       //This step will load Boxen's environment
boxen --srcdir ~               //This step set your source directory to your home directory
source /opt/boxen/env.sh       //This step will reload Boxen's environment
./script/boxen --no-fde <team> //This step will set up apache files and clone your repos
Run Composer
Follow the directions here Using Composer with OWL.
Restart Apache and Test
sudo apachectl restart
visiting fowl.local/status should yield

Setup PHPStorm
OWL Setup Guide - PHPStorm
Using Postman
Postman is a Chrome extension that helps you be more efficient while working with APIs
Postman has been bookmarked in Chrome and is also available at chrome-extension://fdmmgilgnpjigdojojpjoooidkmcomcm/index.html
Now you can have a small, manageable, set of collections that work in each environment!
Note: the access tokens are attached and will expire, you can easily update them in Postman.
Database Access Setup (with SQuirreL SQL)
For most purposes, the database can be accessed in SQuirreL SQL without the need for a more complicated virtual machine setup.
Launch SQuirreL SQL.
In the Aliases pane, edit the 4 aliases and add your Active Directory credentials:

For Example:
Field	Value
Name	DEV dbcc_ecomm
Driver	jTDS SQL Server
URL	
jdbc:jtds:sqlserver://10.26.34.100:63695;DOMAIN=CREDIBILITY;
User Name	
your AD credentials
Password
Preparing to Use Bottle
For more information regarding Ship In A Bottle (SIAB) please see the following documentation:
Ship in a Bottle - Deployment Guide
cd ~/projects/salt-config
vagrant status
vagrant up saltmaster
 

You might also be interested in...
OWL Logging on Mac OSX
PHPStorm / PHP Storm Keys
tunnelblick (for vpn)
Alias Shortcuts - Improve Efficiency
iTerm2
Zshell


