
### Alias Shortcuts - Improve Efficiency  

Place the following inside of your ~/.bash_aliases file in order improve your developing speed.  

#### bash-completion  

Not an alias, but auto complete (tab) everything, not just files/folders (requires Homebrew):  
> $ brew install bash-completion  

Don't forget to follow the instructions and add the necessary lines to your ~/.bash_profile . Most commands will start autocompleting, but to get git to join the party, install a new, shiny, non-apple version of git:  
> $ brew install git  

#### Aliases

alias sc='echo -e "\nMy shortcuts: \n"; cat ~/.bash_aliases | grep alias; echo -e "\n"'  
alias editbp='edit ~/.bash_profile && source ~/.bash_profile'  
alias editba='edit ~/.bash_aliases && source ~/.bash_aliases'  
alias loadbp='source ~/.bash_profile'  
alias zf='/Users/nkatz/ZendFramework/bin/zf.sh'  
alias ll='ls -la | grep "^d" && ls -la | grep -v "^d"'  
alias tailelog='tail -f /var/log/apache2/error_log'  
alias tailalog='tail -f /var/log/apache2/access_log'  
alias salt-config="cd ~/Sites/salt-config"  
alias editaconf='sudo vi /etc/apache2/httpd.conf'  
alias editdbinclude='vi /etc/apache2/extra/dev_db.include'  
alias checkconfig="sudo apachectl configtest"    
alias dropcache="rm -f ~/Sites/helios/www/application/cache/zend_cache* ~/Sites/helios/www/application/cache/minify/minify* ~/Sites/helios/www/application/activity-feed-cache/zend_cache*"  
alias javaserver="gotoreg && java -jar selenium-server-standalone-2.31.0.jar"  
alias gotoreg="cd ~/Sites/helios/tools/regression"  
alias gotohel="cd ~/Sites/helios"  
alias gotocms="cd ~/Sites/cms"  
alias gotomycr="cd ~/Sites/mycredit"  
alias updatehel="gotohel && gco master && git pull && gplo master"  
alias updatemycr="gotomycr && gco master && git pull && gplo master"  
alias updatecms="gotocms && gco master && git pull && gplo master"  
alias updateall="updatehel && updatemycr && updatecms"  
alias gpso="git push origin"  
alias gplo="git pull origin"  
alias gpl="git pull"  
alias uncommit="git reset --soft HEAD^"  
alias gs="git status"  
alias liquibase="~/Desktop/liquibase/liquibase"  
alias updatehelb="updatehel && gco dev && gplo dev && gco qa && gplo qa && gco stg && gplo stg"  
alias updatemycrb="updatemycr && gco dev && gplo dev && gco qa && gplo qa && gco stg && gplo stg &&"  
alias updatecmsb="updatecms && gco dev && gplo dev && gco qa && gplo qa && gco stg && gplo stg &&"  
alias updateallb="updatehelb && updatemycrb && updatecmsb &&"  
alias rmb="git branch -D"  
alias gcp="git gc && git prune origin"  
alias stubson="sudo sed -i .bak -e '/^ *ProxyPass[^/]*\/[^j]/s/^/#/g' -e 's/#\( *Alias \)/\1/' /etc/apache2/extra/httpd-vhosts.conf && sudo apachectl restart"  
alias stubsoff="sudo sed -i .bak -e '/^ *Alias/s/^/#/g' -e 's/#\( *ProxyPass[^/]*\/[^j]\)/\1/' /etc/apache2/extra/httpd-vhosts.conf && sudo apachectl restart"  
alias gm="git merge --no-ff"

------------------------------------------------------------------------------------------------------

#### Notes  

**sc** - Shows you a list of all shortcut aliases  
**editbp** - edit .bash_profile and reload; makes it easy to add new shortcuts on the fly  
**loadbp** - reload .bash_profile  
**tailelog** - tail error log  
**tailalog** - tail access log  
**editaconf** - edit apache conf file  
**editdbinclude** - edit your dev_db.include config file  
**dropcache** - drop zend cache from helios   
**javaserver** - begins standalone selenium server for running regression tests  
**gotoreg** - goes to the regression directory (helios) where you can run functional tests  
**gotohel** - goes to helios directory  
**gotocms** - goes to cms directory  
**gotomycr** - goes to my credit directory  
**updatehel** - Pulls from remote server and updates master branch on helios     
**updatemycr** - Pulls from remote server and updates master branch on mycredit  
**updatecms** - Pulls from remote server and updates master branch on cms  
**updateall** - Pulls from remote server and updates master branch on all repos  
**uncommit** - retract latest commit in case you forgot to add a file or made a typo  
**updatehelb** - updates helios master, dev, qa, and stg branches  
**updatemycrb** - updates mycredit master, dev, qa, and stg branches  
**updatecmsb** - updates cms master, dev, qa, and stg branches  
**updateallb** - updates all repos' master, dev, qa, and stg branches  
**rmb** - deletes a branch (must not be currently checked out)  
**gcp** - garbage collect and prunes
