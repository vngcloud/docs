# Processor

## Overview <a href="#tong-quan" id="tong-quan"></a>

Processor: are libraries that help you parse and enrich data, located in the Processor Group.

***

## Initialize Processor <a href="#khoi-tao-processor" id="khoi-tao-processor"></a>

To create a processor, follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor/) .
2. **Select the Log** folder , then select the **Log pipeline** menu .
3. Select an existing **Log pipeline .**
4. In the existing **Processor group** and configured Source and Destination Log project according to your data parser wishes, select **Create a processor.**
5. **At the Processor information** entry :
   * Enter **Processor name** . The Processor name must comply with our regulations, for details refer to Log Pipeline Limit Scope.
   * Select **Processor type** . We provide you with 6 types of processor types including:
     * [Grok Parser](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor/grok-parser)
     * [JSON Parser](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor/json-parser)
     * [CSV Parser](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor/csv-parser)
     * [Field Remapper](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor/field-remapper)
     * [Date Parser](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor/date-parser)
     * [GEO IP Parser](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor/geo-ip-parser)
     * [User-agent Parser](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor/user-agent-parser)
   * Enter **Filter** for log if any. You can enter filter conditions for the log in one of two ways: **Suggestion mode** or **Editor mode** . How to use these two methods and switch back and forth between the two methods has been described in the features above. For more information, please see [Search logs](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-search/search-logs) .

**6. In the Parsing rule** entry , for each Processor type you choose, follow the specific instructions on each page below.

7\. Select **Create** .

***

## Edit Processors <a href="#chinh-sua-processor" id="chinh-sua-processor"></a>

To edit the Processor in the Log pipeline, follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select the Log folder **.**
3. Select **Log pipeline.**
4. In the list of available log pipelines, select **the Log pipeline** containing **the Processor group and the Processor** you want to edit.
5. At **the Processor** you want to edit, select![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FMQ6QdlqgkT8oE22YzAEh%252Fimage.png%3Falt%3Dmedia%26token%3Dc564e937-9786-4ded-97e2-a6ef698d2127\&width=31\&dpr=4\&quality=100\&sign=95153762\&sv=1)
6. Select **Edit processor** .
7. Edit the parameters for **the Processor** you desire. You can edit all information fields in a Processor configuration. This editing is similar to when you create a new Processor according to the instructions above.
8. Select **Save.**

***

## Delete processor <a href="#xoa-processor" id="xoa-processor"></a>

When you no longer need to use a custom Processor, you can remove the Processor from the system according to the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select the Log folder **.**
3. Select **the Log pipeline** containing the Processor group and the Processor you want to delete.
4. Select **Processor.**
5. At **the Processor** you want to delete, select![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FSSfstn8k2Rk0xkY0yyKF%252Fimage.png%3Falt%3Dmedia%26token%3Deefed5c9-5e52-44a6-8b5e-9cf65cfd0212\&width=31\&dpr=4\&quality=100\&sign=b9dfecbf\&sv=1)
6. Select **Delete** .
7. At the Processor deletion confirmation screen, select **Delete** .

After you successfully delete, your Processor will be completely deleted from our system. You cannot restore a deleted Processor, so please be careful when using this feature.
