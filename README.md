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

#### 1. Generate SSH Keys
Add SSH Key to GitHub. Go to https://help.github.com/articles/generating-ssh-keys/  
Submit your public key to the help desk to be added to Active Directory.   
Make a HelpDesk ticket at: https://dandbhelpdesk.zendesk.com/
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
 
#### 4. Fork and Run Boxen  

Forking this repo will be handled above when accepted into DandB GitHub  
Fork the following repo: https://github.com/taoistmath/USSBoxen  
Open Terminal and run the following commands:  
\<team\> can be any of the following: fowl, phoenix, helios, automation  
(fowl includes phoenix, helios includes verified and mycredit, and automation includes helios and fowl)

> sudo mkdir -p /opt/boxen                     //Do not copy this line! You have to type it!  
sudo chown ${USER}:staff        /opt/boxen  
git clone git@github.com:<github_username>/USSBoxen.git /opt/boxen/repo  
cd /opt/boxen/repo  
git remote add upstream git@github.com:taoistmath/USSBoxen.git  
./script/boxen --no-fde                        //This step will ask for sudo pw, github login, and github pw  
source /opt/boxen/env.sh                       //This step will load Boxen's environment  
boxen --srcdir ~                               //This step set your source directory to your home directory  
source /opt/boxen/env.sh                       //This step will reload Boxen's environment  
./script/boxen --no-fde <team>                 //This step will set up apache files and clone your repos

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
