# Install Log Agent on OS

**Prepare to connect and install the agent**

* If you have a full connection to the internet, this is the best way to avoid errors when installing the agent.
* If you have to install through a proxy or firewall. Open the policy to allow connections to the following addresses:

<table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code># filebeat / logstash 
https://artifacts.elastic.co
# fluentd 
https://toolbelt.treasuredata.com 
https://packages.treasuredata.com
# fluentbit
https://packages.fluentbit.io
# vector
https://repositories.timber.io
</code></pre></td></tr></tbody></table>

* If you have to install completely offline, we recommend downloading filebeat. Other agents such as fluentbit, fluentd, logstash, etc. may need additional complex dependencies. Download filebeat to your device at:

<table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code># debian, ubuntu
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.6.0-amd64.deb
# fedora, centos
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.6.0-x86_64.rpm
# windows
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.7.0-windows-x86_64.msi
</code></pre></td></tr></tbody></table>

* After loading the agent, this connection can be closed. You still need to maintain a log push connection.
