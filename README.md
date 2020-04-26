# splunk_playbook
This repo downloads and configures Splunk Forwarder Agent for Linux instances.
Before this forwarder to work you need to install Splunk Enterprises Server

Splunk Enterprises Server

Requirements;

1-Splunk Enterprises Server 8.0.3

2- Neccessary Packages;

wget
unzip
ansible

a)sudo yum install wget unzip ansible -y
wget -O splunk-8.0.3-a6754d8441bf-Linux-x86_64.tgz 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=linux&version=8.0.3&product=splunk&filename=splunk-8.0.3-a6754d8441bf-Linux-x86_64.tgz&wget=true'

b)Unzip downloaded file splunk-8.0.3-a6754d8441bf-Linux-x86_64.tgz and move the downloaded file to /opt directory
"tar xvzf splunk-8.0.3-a6754d8441bf-Linux-x86_64.tgz -C /opt"

c)go to /opt/splunk/bin run ./spunk start 

d)go to instance IP adress with management port :8000

e)login with admin:password

d)configure receving port to 9997


Splunk Forwarder Agent 8.0.3

Requirements;

1-Splunk Forwarder Agent 8.0.3

2- Neccessary Packages;

wget
unzip
ansible

a)sudo yum install wget unzip ansible -y
wget -O splunkforwarder-8.0.3-a6754d8441bf-Linux-x86_64.tgz 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=linux&version=8.0.3&product=universalforwarder&filename=splunkforwarder-8.0.3-a6754d8441bf-Linux-x86_64.tgz&wget=true'

b)Unzip downloaded file and move the downloaded file to /opt directory
"tar xvzf splunkforwarder-8.0.3-a6754d8441bf-Linux-x86_64.tgz -C /opt"

c)Go to /opt/splunk/bin directory in order to run splunk commands

d)Start Splunk Forwarder
      command: /opt/splunkforwarder/bin/splunk start --accept-license --no-prompt --admin-passwd changeme
  note: this command bypass the license agreement and starts the splunk forwarder

e)Set forward-server
      command: /opt/splunkforwarder/bin/splunk add forward-server 18.223.189.41:9997 -auth admin:changeme
  note: with this command we need to tell the forwarder where to forward the data to IP adress with given specific port number 
  
f)Add monitor
      command: /opt/splunkforwarder/bin/splunk add monitor /var/log/messages 
  note: with splunk add monitor command we specify what kind of data to monitor.
  
g)Enable Boot Start
      command: /opt/splunkforwarder/bin/splunk enable boot-start
  note: forwarder needs to be enable boot-start in order to work proparly. 
  
h)Restart Splunk forwarder
      command: /opt/splunkforwarder/bin/splunk restart
  note:splunk forwarder needs to be restarted in order to run with new configurations.

