# Debian/ Ubuntu

Before installing the agent on the operating systems we support below, you need to download the certificate according to the instructions at [Initialize Certificate](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-agent/khoi-tao-certificate) . Information on setting up the agent is in the readme file, and the instruction scripts are also in the downloaded certificate file. Use this information with the instructions below to complete Agent for Log setup.

**Setting**

Determine the type of agent you want to install and follow that agent's instructions below:

FilebeatLogstash

If using a script prepared in the download folder, run the command

```
sudo chmod +x filebeat.sh
sudo ./filebeat.sh <path-to-file-log>
```

If installing manually, run the command

```
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.7.1-amd64.deb
sudo dpkg -i filebeat-8.7.1-amd64.deb
```

***

Next you need to configure agent log. The configuration files below have been prepared by us in the script when downloading the certificate. The description below helps readers imagine what it would be like if we created a manual.

**Configuration**

FilebeatLogstash

The configuration file `/etc/filebeat/filebeat.yml.`below will retrieve all logs in the file `/var/log/app.log`and push it to vMonitor Platform:

```
filebeat.inputs:
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
```

* In there:
  * At `input`the path to the log file
  * At `output`, the variables you need to fill in are taken from the certificate download step above:
    * `$BOOTSTRAP_SERVERS, $TOPIC`taken from file [info.md](http://info.md/)
    * `$PATH_FILE_VNG_TRUST_PEM,$PATH_FILE_USER_CER_PEM,$PATH_FILE_USER_KEY_PEM`is the path to the file VNG.trust.pem user.cer.pem user.key.pem
* Read more advanced configurations at[![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fwww.elastic.co%2Ffavicon-16x16.png\&width=300\&dpr=4\&quality=100\&sign=2f0b66d1\&sv=1)Configure Filebeat | Filebeat Reference \[8.8\] | Elastic](https://www.elastic.co/guide/en/beats/filebeat/current/configuring-howto-filebeat.html)

***

**Administration**

If installed manually, by default the agent log after installation will **not** automatically turn on, you should check the start and enable (start automatically with the machine) for them.

FilebeatLogstash

<table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><ul><li>Start</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl start filebeat
</code></pre></td></tr></tbody></table><ul><li>Enable</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl enable filebeat
</code></pre></td></tr></tbody></table><ul><li>Stop</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl stop filebeat
</code></pre></td></tr></tbody></table><ul><li>Reload</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl reload filebeat
</code></pre></td></tr></tbody></table><ul><li>Restart</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl restart filebeat
</code></pre></td></tr></tbody></table><ul><li>Observe</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>systemctl status filebeat
journalctl -f --unit filebeat
tail -f /var/log/filebeat
</code></pre></td></tr></tbody></table><ul><li>Uninstall</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>tapt remove --purge filebeat
</code></pre></td></tr></tbody></table></td></tr><tr><td><p></p><pre><code>systemctl start filebeat
</code></pre></td></tr><tr><td><p></p><pre><code>systemctl enable filebeat
</code></pre></td></tr><tr><td><p></p><pre><code>systemctl stop filebeat
</code></pre></td></tr><tr><td><p></p><pre><code>systemctl reload filebeat
</code></pre></td></tr><tr><td><p></p><pre><code>systemctl restart filebeat
</code></pre></td></tr><tr><td><p></p><pre><code>systemctl status filebeat
journalctl -f --unit filebeat
tail -f /var/log/filebeat
</code></pre></td></tr><tr><td><p></p><pre><code>tapt remove --purge filebeat
</code></pre></td></tr></tbody></table>
