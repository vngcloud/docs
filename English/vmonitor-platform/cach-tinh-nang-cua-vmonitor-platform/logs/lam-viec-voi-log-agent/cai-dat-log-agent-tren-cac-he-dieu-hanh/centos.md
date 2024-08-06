# CentOS

Before installing the agent on the operating systems we support below, you need to download the certificate according to the instructions at [Initialize Certificate](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-agent/khoi-tao-certificate) . Information on setting up the agent is in the readme file, and the instruction scripts are also in the downloaded certificate file. Use this information with the instructions below to complete Agent for Log setup.

**Setting**

Determine the type of agent you want to install and follow that agent's instructions below:

FilebeatLogstash

* If using a script prepared in the download folder, run the command

| <p></p><pre><code>sudo chmod +x filebeat.sh
sudo ./filebeat.sh &#x3C;path-to-file-log>
</code></pre> |
| ---------------------------------------------------------------------------------------------------- |

* If installing manually, run the command

| <p></p><pre><code>Tải tệp tin rpm: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.7.1-x86_64.rpm
Install filebeat: sudo rpm -vi filebeat-8.7.1-x86_64.rpm
</code></pre> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Next you need to configure agent log. The configuration files below have been prepared by us in the script when downloading the certificate. The description below helps readers imagine what it would be like if we created a manual.

**Configuration**

Filebeat

| <ul><li>File <code>/etc/filebeat/filebeat.yml</code>. The configuration below will retrieve all logs in the file <code>/var/log/app.log</code>and push them to vMonitor Platform:</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p></p><pre><code>filebeat.inputs:
- type: log
  paths:
    - /var/log/app.log

output.kafka:
  hosts: ["$BOOTSTRAP_SERVERS"]
  topic: "$TOPIC"
  partition.round_robin:
    reachable_only: false
  required_acks: 1
  compression: gzip
  max_message_bytes: 1000000
  ssl.certificate_authorities:
    - $PATH_FILE_VNG_TRUST_PEM
  ssl.certificate: "$PATH_FILE_USER_CER_PEM"
  ssl.key: "$PATH_FILE_USER_KEY_PEM"
  ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
  path: /var/log/filebeat
  name: filebeat
  keepfiles: 7
  permissions: 0644
</code></pre></td></tr></tbody></table><ul><li><p>In which In input the path to the log file</p><p>In output , the variables you need to fill in are taken from the certificate loading step above:</p><ul><li><code>$BOOTSTRAP_SERVERS, $TOPIC</code>taken from file <a href="http://info.md/">info.md</a></li><li><code>$PATH_FILE_VNG_TRUST_PEM, $PATH_FILE_USER_CER_PEM, $PATH_FILE_USER_KEY_PEM</code>is the path to the file VNG.trust.pem user.cer.pem user.key.pem</li></ul></li><li>Read more advanced configurations at<a href="https://www.elastic.co/guide/en/beats/filebeat/current/configuring-howto-filebeat.html"><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fwww.elastic.co%2Ffavicon-16x16.png&#x26;width=300&#x26;dpr=4&#x26;quality=100&#x26;sign=2f0b66d1&#x26;sv=1" alt="">Configure Filebeat | Filebeat Reference [8.8] | Elastic</a></li></ul> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p></p><pre><code>filebeat.inputs:
- type: log
  paths:
    - /var/log/app.log

output.kafka:
  hosts: ["$BOOTSTRAP_SERVERS"]
  topic: "$TOPIC"
  partition.round_robin:
    reachable_only: false
  required_acks: 1
  compression: gzip
  max_message_bytes: 1000000
  ssl.certificate_authorities:
    - $PATH_FILE_VNG_TRUST_PEM
  ssl.certificate: "$PATH_FILE_USER_CER_PEM"
  ssl.key: "$PATH_FILE_USER_KEY_PEM"
  ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
  path: /var/log/filebeat
  name: filebeat
  keepfiles: 7
  permissions: 0644
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| <p></p><pre><code>filebeat.inputs:
- type: log
  paths:
    - /var/log/app.log

output.kafka:
  hosts: ["$BOOTSTRAP_SERVERS"]
  topic: "$TOPIC"
  partition.round_robin:
    reachable_only: false
  required_acks: 1
  compression: gzip
  max_message_bytes: 1000000
  ssl.certificate_authorities:
    - $PATH_FILE_VNG_TRUST_PEM
  ssl.certificate: "$PATH_FILE_USER_CER_PEM"
  ssl.key: "$PATH_FILE_USER_KEY_PEM"
  ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
  path: /var/log/filebeat
  name: filebeat
  keepfiles: 7
  permissions: 0644
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

***

**Administration**

Filebeat

| <ul><li>Start</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl start logstash
</code></pre></td></tr></tbody></table><ul><li>Enable</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl enable logstash
</code></pre></td></tr></tbody></table><ul><li>Stop</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl stop logstash
</code></pre></td></tr></tbody></table><ul><li>Reload</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl reload logstash
</code></pre></td></tr></tbody></table><ul><li>Restart</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl restart logstash
</code></pre></td></tr></tbody></table><ul><li>Observe</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl status logstash
journalctl -f --unit logstash
tail -f /var/log/logstash
</code></pre></td></tr></tbody></table><ul><li>Uninstall</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>yum remove logstash
</code></pre></td></tr></tbody></table> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p></p><pre><code>systemctl start logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| <p></p><pre><code>systemctl enable logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| <p></p><pre><code>systemctl stop logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <p></p><pre><code>systemctl reload logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| <p></p><pre><code>systemctl restart logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| <p></p><pre><code>systemctl status logstash
journalctl -f --unit logstash
tail -f /var/log/logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| <p></p><pre><code>yum remove logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| <p></p><pre><code>systemctl start logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| <p></p><pre><code>systemctl enable logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| <p></p><pre><code>systemctl stop logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <p></p><pre><code>systemctl reload logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| <p></p><pre><code>systemctl restart logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| <p></p><pre><code>systemctl status logstash
journalctl -f --unit logstash
tail -f /var/log/logstash
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
