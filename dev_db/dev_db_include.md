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
