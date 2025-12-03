# Windows

Before installing the agent on the operating systems we support below, you need to download the certificate according to the instructions at [Initialize Certificate](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-agent/khoi-tao-certificate) . The download file will contain the certificates used to authenticate with the vMonitor Logs system. Use this information with the instructions below to complete Agent for Log setup.

**Setting**

Determine the type of agent you want to install and follow that agent's instructions below:

Filebeat

<table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><ul><li>Download filebeat at <a href="https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.7.1-windows-x86_64.zip">https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.7.1-windows-x86_64.zip</a></li><li>Unzip the downloaded filebeat folder</li><li>Copy the files user.cer.pem, user.key.pem, VNG.trust.pem from the certificate folder to the extracted filebeat folder. Let's say below we have extracted filebeat into a folder<code>C:\filebeat-8.7.1-windows-x86_64</code></li><li>Manually run the command below with PowerShell</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>cd C:\filebeat-8.7.1-windows-x86_64
.\filebeat.exe -c .\filebeat.yml
</code></pre></td></tr></tbody></table><ul><li>In which: In the filebeat.yml file, we have set up the example in the download certificate folder as below to push the content of file C:\agent.log to the system.</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>filebeat.inputs:
- type: log
  paths:
    - C:\agent.log
output.kafka:
hosts: ["$BOOTSTRAP_SERVERS"]
topic: $TOPIC
partition.round_robin:
reachable_only: false
required_acks: 1
compression: gzip
max_message_bytes: 1000000
ssl.certificate_authorities:
- $PATH_FILE_VNG_TRUST_PEM
ssl.certificate: $PATH_FILE_USER_CER_PEM
ssl.key: $PATH_FILE_USER_KEY_PEM
ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
path: /var/log/filebeat
name: filebeat
keepfiles: 7
permissions: 0644
</code></pre></td></tr></tbody></table><p>In there:</p><ul><li>At <code>input</code>the path to the log file</li><li><p>At <code>output</code>, the variables you need to fill in are taken from the certificate download step above:</p><ul><li><code>$BOOTSTRAP_SERVERS, $TOPIC</code>taken from file <a href="http://info.md/">info.md</a></li><li><code>$PATH_FILE_VNG_TRUST_PEM,$PATH_FILE_USER_CER_PEM,$PATH_FILE_USER_KEY_PEM</code>is the path to the file VNG.trust.pem user.cer.pem user.key.pem</li></ul></li></ul><p>Install a service that runs in the background:</p><p>On powershell when entering the filebeat path</p><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>.\install-service-filebeat.ps1
</code></pre></td></tr></tbody></table><p>We recommend that you try running it manually first to identify the problem if there is any.</p></td></tr><tr><td></td></tr><tr><td><p>Copy</p><pre><code>cd C:\filebeat-8.7.1-windows-x86_64
.\filebeat.exe -c .\filebeat.yml
</code></pre></td></tr><tr><td></td></tr><tr><td><p>Copy</p><pre><code>filebeat.inputs:
- type: log
  paths:
    - C:\agent.log
output.kafka:
hosts: ["$BOOTSTRAP_SERVERS"]
topic: $TOPIC
partition.round_robin:
reachable_only: false
required_acks: 1
compression: gzip
max_message_bytes: 1000000
ssl.certificate_authorities:
- $PATH_FILE_VNG_TRUST_PEM
ssl.certificate: $PATH_FILE_USER_CER_PEM
ssl.key: $PATH_FILE_USER_KEY_PEM
ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
path: /var/log/filebeat
name: filebeat
keepfiles: 7
permissions: 0644
</code></pre></td></tr><tr><td></td></tr><tr><td><p>Copy</p><pre><code>.\install-service-filebeat.ps1
</code></pre></td></tr><tr><td><p>Copy</p><pre><code>cd C:\filebeat-8.7.1-windows-x86_64
.\filebeat.exe -c .\filebeat.yml
</code></pre></td></tr><tr><td><p>Copy</p><pre><code>filebeat.inputs:

type: log
paths:

C:\agent.log



output.kafka:
hosts: ["$BOOTSTRAP_SERVERS"]
topic: $TOPIC
partition.round_robin:
reachable_only: false
required_acks: 1
compression: gzip
max_message_bytes: 1000000
ssl.certificate_authorities:
- $PATH_FILE_VNG_TRUST_PEM
ssl.certificate: $PATH_FILE_USER_CER_PEM
ssl.key: $PATH_FILE_USER_KEY_PEM
ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
path: /var/log/filebeat
name: filebeat
keepfiles: 7
permissions: 0644
</code></pre></td></tr><tr><td><p>Copy</p><pre><code>.\install-service-filebeat.ps1
</code></pre></td></tr></tbody></table>
