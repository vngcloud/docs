# Install Log Agent on Docker

Before installing the agent on the operating systems we support below, you need to download the certificate according to the instructions at [Initialize Certificate](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-agent/khoi-tao-certificate) . Information on setting up the agent is in the readme file, and the instruction scripts are also in the downloaded certificate file. Use this information with the instructions below to complete Agent for Log setup.

**Setting**

FilebeatLogstash

* Download images

| <p>Copy</p><pre><code>docker pull docker.elastic.co/beats/filebeat:8.7.0
</code></pre> |
| -------------------------------------------------------------------------------------- |

***

* [Download the certificate](https://vngctech.atlassian.net/wiki/spaces/VP/pages/847970312) to get user authentication information
* If using the prepared script in the download folder, run the command:
  * In the setup example below, we will mount `/var/log/app.log`an agent installed using docker to push logs to the system

| <p>Copy</p><pre><code>docker compose up -d -f docker-compose.yml
</code></pre> |
| ------------------------------------------------------------------------------ |

The configuration files below have been prepared by us in the script when downloading the certificate. The description below helps readers imagine what it would be like if we created a manual.

**Configuration**

| <ul><li>File<code>docker-compose.yml</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>version: "3"
services:
  filebeat-agent-vmonitor:
    image: docker.elastic.co/beats/filebeat:8.7.0
    container_name: filebeat-agent-vmonitor
    restart: always
    env_file:
      - container.env
    volumes:
      -  $PWD/filebeat.yml:/usr/share/filebeat/filebeat.yml
      -  $PWD/VNG.trust.pem:/usr/share/filebeat/VNG.trust:rw
      -  $PWD/user.cer.pem:/usr/share/filebeat/user.cer.pem:rw
      -  $PWD/user.key.pem:/usr/share/filebeat/user.key.pem:rw
      -  /var/log/app.log:/var/log/app.log:ro
      -  /var/log/filebeat/:/var/log/filebeat/
    logging:
      driver: "json-file"
      options:
        max-size: "50m"
    deploy:
      resources:
         limits:
           cpus: '1'
           memory: 2G
</code></pre></td></tr></tbody></table><ul><li>File <code>filebeat.yml</code>. The configuration below will retrieve all logs written to file <code>/var/log/app.log</code>for vMonitor Platform:</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>filebeat.inputs:
- type: log
  paths:
    - /var/log/app.log

output.kafka:
  hosts: ${BOOTSTRAP_SERVERS}
  topic: ${TOPIC}
  partition.round_robin:
    reachable_only: false
  required_acks: 1
  compression: gzip
  max_message_bytes: 1000000
  ssl.certificate_authorities:
    - /usr/share/filebeat/VNG.trust
  ssl.certificate: /usr/share/filebeat/user.cer.pem
  ssl.key: /usr/share/filebeat/user.key.pem
  ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
  path: /var/log/filebeat
  name: filebeat
  keepfiles: 7
  permissions: 0644
</code></pre></td></tr></tbody></table><ul><li>Note: the $ variables <code>BOOTSTRAP_SERVERS, $TOPIC</code>above are already in <code>container.env</code>the file in the downloaded certificate folder.</li></ul> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Copy</p><pre><code>version: "3"
services:
  filebeat-agent-vmonitor:
    image: docker.elastic.co/beats/filebeat:8.7.0
    container_name: filebeat-agent-vmonitor
    restart: always
    env_file:
      - container.env
    volumes:
      -  $PWD/filebeat.yml:/usr/share/filebeat/filebeat.yml
      -  $PWD/VNG.trust.pem:/usr/share/filebeat/VNG.trust:rw
      -  $PWD/user.cer.pem:/usr/share/filebeat/user.cer.pem:rw
      -  $PWD/user.key.pem:/usr/share/filebeat/user.key.pem:rw
      -  /var/log/app.log:/var/log/app.log:ro
      -  /var/log/filebeat/:/var/log/filebeat/
    logging:
      driver: "json-file"
      options:
        max-size: "50m"
    deploy:
      resources:
         limits:
           cpus: '1'
           memory: 2G
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <p>Copy</p><pre><code>filebeat.inputs:
- type: log
  paths:
    - /var/log/app.log

output.kafka:
  hosts: ${BOOTSTRAP_SERVERS}
  topic: ${TOPIC}
  partition.round_robin:
    reachable_only: false
  required_acks: 1
  compression: gzip
  max_message_bytes: 1000000
  ssl.certificate_authorities:
    - /usr/share/filebeat/VNG.trust
  ssl.certificate: /usr/share/filebeat/user.cer.pem
  ssl.key: /usr/share/filebeat/user.key.pem
  ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
  path: /var/log/filebeat
  name: filebeat
  keepfiles: 7
  permissions: 0644
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| <p>Copy</p><pre><code>version: "3"
services:
  filebeat-agent-vmonitor:
    image: docker.elastic.co/beats/filebeat:8.7.0
    container_name: filebeat-agent-vmonitor
    restart: always
    env_file:
      - container.env
    volumes:
      -  $PWD/filebeat.yml:/usr/share/filebeat/filebeat.yml
      -  $PWD/VNG.trust.pem:/usr/share/filebeat/VNG.trust:rw
      -  $PWD/user.cer.pem:/usr/share/filebeat/user.cer.pem:rw
      -  $PWD/user.key.pem:/usr/share/filebeat/user.key.pem:rw
      -  /var/log/app.log:/var/log/app.log:ro
      -  /var/log/filebeat/:/var/log/filebeat/
    logging:
      driver: "json-file"
      options:
        max-size: "50m"
    deploy:
      resources:
         limits:
           cpus: '1'
           memory: 2G
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <p>Copy</p><pre><code>filebeat.inputs:
- type: log
  paths:
    - /var/log/app.log

output.kafka:
  hosts: ${BOOTSTRAP_SERVERS}
  topic: ${TOPIC}
  partition.round_robin:
    reachable_only: false
  required_acks: 1
  compression: gzip
  max_message_bytes: 1000000
  ssl.certificate_authorities:
    - /usr/share/filebeat/VNG.trust
  ssl.certificate: /usr/share/filebeat/user.cer.pem
  ssl.key: /usr/share/filebeat/user.key.pem
  ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
  path: /var/log/filebeat
  name: filebeat
  keepfiles: 7
  permissions: 0644
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

***

**Administration**

FilebeatLogstash

| <ul><li>Stop</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>docker stop filebeat
</code></pre></td></tr></tbody></table><ul><li>Reload</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>docker kill --signal=HUP filebeat
</code></pre></td></tr></tbody></table><ul><li>Restart</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>docker restart filebeat
</code></pre></td></tr></tbody></table><ul><li>Observe</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>docker logs --tail 100 -f filebeat
</code></pre></td></tr></tbody></table><ul><li>Uninstall</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>docker rm filebeat
</code></pre></td></tr></tbody></table> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Copy</p><pre><code>docker stop filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| <p>Copy</p><pre><code>docker kill --signal=HUP filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| <p>Copy</p><pre><code>docker restart filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| <p>Copy</p><pre><code>docker logs --tail 100 -f filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <p>Copy</p><pre><code>docker rm filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <p>Copy</p><pre><code>docker stop filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| <p>Copy</p><pre><code>docker kill --signal=HUP filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| <p>Copy</p><pre><code>docker restart filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| <p>Copy</p><pre><code>docker logs --tail 100 -f filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <p>Copy</p><pre><code>docker rm filebeat
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

***

Before performing agent installation on the operating systems we support below, you need to [Initialize Certificate](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-agent/khoi-tao-certificate) . The setup agent instructions are in the readme file, the script instructions are also in the downloaded certificate file. Use this information with the instructions below to complete Agent for Log setup.
