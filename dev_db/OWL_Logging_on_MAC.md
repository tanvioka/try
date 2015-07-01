
#### OWL Logging on Mac OSX

##### Logging:  

To watch logs locally on Mac OSX, you must add the following to your /etc/syslog.conf file:
	
> user.* &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /var/log/messages

Then run the following commands to restart the syslog service:

>  $ sudo launchctl unload /System/Library/LaunchDaemons/com.apple.syslogd.plist  

>  $ sudo launchctl load /System/Library/LaunchDaemons/com.apple.syslogd.plist

Now, when running the application, you can tail /var/log/messages as follows:   

> tail -f /var/log/message -f /var/log/apache2/error_log
