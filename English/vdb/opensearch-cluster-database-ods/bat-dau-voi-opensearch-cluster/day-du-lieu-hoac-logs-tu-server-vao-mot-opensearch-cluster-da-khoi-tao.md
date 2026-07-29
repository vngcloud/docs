# Push data or event logs from Logstash into an OpenSearch Cluster

## Prerequisites

Suppose you have successfully initialized an OpenSearch Cluster with the following parameters:

Next, proceed to push sample data into OpenSearch Dashboards or push event logs from Logstash into OpenSearch.

## **Push sample data into OpenSearch Dashboards**

Sample data will help you get familiar with OpenSearch Dashboards and test data visualization capabilities.

#### **Step 1: Download sample data**

Run the following command to download sample data:

```bash
curl -O https://raw.githubusercontent.com/opensearch-project/documentation-website/2.19/assets/examples/ecommerce-field_mappings.json
curl -O https://raw.githubusercontent.com/opensearch-project/documentation-website/2.19/assets/examples/ecommerce.ndjson
```

#### **Step 2: Create index and push data into OpenSearch**

Run the following command to create an index and push data to OpenSearch:

```bash
# 2. Create index and data.
curl -H "Content-Type: application/json" -X PUT "https://<<OpenSearch_ReceiveLogs_Endpoint>>/ecommerce" -k -H "Authorization: Basic $(echo -n 'master-user:<<Master_User_Password>>' | base64)" --data-binary "@ecommerce-field_mappings.json"
curl -H "Content-Type: application/json" -X PUT "https://<<OpenSearch_ReceiveLogs_Endpoint>>/ecommerce/_bulk" -k -H "Authorization: Basic $(echo -n 'master-user:<<Master_User_Password>>' | base64)" --data-binary "@ecommerce.ndjson"
```

You can get the `OpenSearch_ReceiveLogs_Endpoint` information from the vDB Portal and replace `<<Master_User_Password>>` with the master account password you previously created.

Example:

```bash
# 2. Create index and data.
curl -H "Content-Type: application/json" -X PUT "https://open-search-dem-53461-5cfxl-hcm03.vdb-opensearch.vngcloud.vn:9200/ecommerce" -k -H "Authorization: Basic $(echo -n 'master-user:123456789aA@' | base64)" --data-binary "@ecommerce-field_mappings.json"
curl -H "Content-Type: application/json" -X PUT "https://open-search-dem-53461-5cfxl-hcm03.vdb-opensearch.vngcloud.vn:9200/ecommerce/_bulk" -k -H "Authorization: Basic $(echo -n 'master-user:123456789aA@' | base64)" --data-binary "@ecommerce.ndjson"
```

[<br>](https://liemnt5-cidr-11430-2ue3z-hcm03.vdb-opensearch.vngcloud.tech)The result will display as follows:

```bash
curl -H "Content-Type: application/json" -X PUT "https://open-search-dem-53461-5cfxl-hcm03.vdb-opensearch.vngcloud.vn:9200/ecommerce" -k -H "Authorization: Basic $(echo -n 'master-user:123456789aA@' | base64)" --data-binary "@ecommerce-field_mappings.json"
{"acknowledged":true,"shards_acknowledged":true,"index":"ecommerce"}

curl -H "Content-Type: application/json" -X PUT "https://open-search-dem-53461-5cfxl-hcm03.vdb-opensearch.vngcloud.vn:9200/ecommerce/_bulk" -k -H "Authorization: Basic $(echo -n 'master-user:123456789aA@' | base64)" --data-binary "@ecommerce.ndjson"
{"took":4579,"errors":false,"items":[{"index":{"_index":"ecommerce","_id":"0","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":0,"_primary_term":1,"status":201}},{"index":{"_index":"ecommerce","_id":"1","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":1,"_primary_term":1,"status":201}},{"index":{"_index":"ecommerce","_id":"2","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":2,"_primary_term":1,"status":201}},{"index":{"_index":"ecommerce","_id":"3","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":3,"_primary_term":1,"status":201}},{"index":{"_index":"ecommerce","_id":"4","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":4,"_primary_term":1,"status":201}},{"index":{"_index":"ecommerce","_id":"5","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":5,"_primary_term":1,"status":201}},{"index":{"_index":"ecommerce","_id":"6","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":6,"_primary_term":1,"status":201}},{"index":{"_index":"ecommerce","_id":"7","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":7,"_primary_term":1,"status":201}},{"index":{"_index":"ecommerce","_id":"8","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":8,"_primary_term":1,"status":2...
....
```

**Step 3: Check data on OpenSearch Dashboards**

1. Access and log in to **OpenSearch Dashboards**
2. Go to **Management**, select **Dashboard Management**

<figure><img src="../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

3. Select **Index patterns**, then select **Create index pattern**

<figure><img src="../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

4. Enter **Index pattern name**, for example `ecommerce*` then select **Next step**

<figure><img src="../../../.gitbook/assets/image (378) (1).png" alt=""><figcaption></figcaption></figure>

5. Access **Discover** to view the sample data.

<figure><img src="../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## **Push event logs from Logstash into OpenSearch**

If you want to collect and push event logs from Logstash into OpenSearch, follow these steps:

#### **Step 1: Install Logstash (if not already installed)**

On Ubuntu/Debian:

```bash
sudo apt update && sudo apt install logstash
```

On CentOS/RHEL:

```bash
sudo yum install logstash
```

#### **Step 2: Configure Logstash to send logs to OpenSearch**

Create a configuration file for Logstash, for example:

```bash
sudo nano /etc/logstash/conf.d/logstash.conf
```

Add the following content:

```editorconfig
input {
    file {
        path => "/var/log/syslog"
        start_position => "beginning"
        sincedb_path => "/dev/null"
    }
}

filter {
    mutate {
        add_field => { "host" => "%{host}" }
    }
}

output {
    opensearch {
        hosts => ["OpenSearch_ReceiveLogs_Endpoint"]
        index => "logstash-logs"
        user => "master-user"
        password => "Your_MasterUser_Password"
        ssl => false
    }
}
```

Replace:

* `OpenSearch_ReceiveLogs_Endpoint` with your OpenSearch Receive Logs Endpoint from the vDB Portal.
* `Your_MasterUser_Password` with the master account password you previously created.

#### **Step 3: Start Logstash**

After configuration is complete, start Logstash to begin sending logs:

```bash
sudo systemctl start logstash
```

#### **Step 4: Check data in OpenSearch**

You can check logs using the OpenSearch API:

```bash
curl -X GET "https://OpenSearch_ReceiveLogs_Endpoint/logstash-logs/_search?pretty" -k -H "Authorization: Basic $(echo -n 'master-user:Your_MasterUser_Password' | base64)"
```

Example:

```bash
curl -X GET "https://open-search-dem-53461-5cfxl-hcm03.vdb-opensearch.vngcloud.vn:9200/logstash-logs/_search?pretty" -k -H "Authorization: Basic $(echo -n 'master-user:123456789aA@' | base64)"
```

If logs appear, it means Logstash has successfully sent data to OpenSearch.

#### **Step 5: View logs on OpenSearch Dashboards**

1. Access and log in to **OpenSearch Dashboards**
2. Go to **Management**, select **Dashboard Management**

<figure><img src="../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

3. Select **Index patterns**, then select **Create index pattern**

<figure><img src="../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

4. Enter **Index pattern name**, for example `logstash-logs*` then select **Next step**

<figure><img src="../../../.gitbook/assets/image (360).png" alt=""><figcaption></figcaption></figure>

5. Finally, access **Discover** to view the logs.
