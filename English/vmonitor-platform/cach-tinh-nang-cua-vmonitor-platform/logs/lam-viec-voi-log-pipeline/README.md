# Working with Log pipeline

## Overview <a href="#lamviecvoilogpipeline-tongquan" id="lamviecvoilogpipeline-tongquan"></a>

Log Pipeline is a feature that allows you to parse or enrich data from unstructured, meaningless data (raw log) into structured, meaningful log data (eg Json format). Log data will be run through a series of Processor Groups and Processors. If that log meets the filter conditions in Processor Group and Processor, Processor will be executed on those logs sequentially until finished.

**Ingredient**

* Log Pipeline: contains Processor Groups that allow parsing or enriching data from unstructured, meaningless data (raw log) into structured, meaningful log data (eg Json format)
* Processor Group: allows you to specify where to get log data (source log project), where to store parsed data (destination log project) and which logs will be parsed when the filter is satisfied
* Processor: are libraries that help you parse and enrich data, located in the Processor Group.

***

## **The model describes Log Pipeline** <a href="#mo-hinh-mo-ta-log-pipeline" id="mo-hinh-mo-ta-log-pipeline"></a>

**Log Pipeline 1** : the most basic model has only 1 source log project and 1 destination log project with the information below, for the need that raw logs only contain 1 type of log data and you only want to parse to 1 destination. log project

* Source Log Project: is the place to store raw logs, unstructured data that you need to parse
* Destination Log Project: is the place to store structured logs, data that has been parsed into structure after running through the Log Pipeline system.
* Log Pipeline contains only 1 Processor Group with the Filter being source:nginx, meaning that logs with a source:nginx field will only run through the Processor Group system for parsing.
* Processor Group contains 3 Processors to parse the log into structured data and save it to the destination log project.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fna9MtTEniVMq7QfaXeHS%252Fimage.png%3Falt%3Dmedia%26token%3Dd0c10bbb-4d94-4b73-98d4-94e821b6cdea&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4fdb6060&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Log Pipeline 2** : more complex model has 1 source log project but the data is parsed into 2 destination log projects with information as below, for the need that your raw logs contain many different types of log data and you want to parse and store in many different destination log projects

* Source Log Project: is the place to store raw logs, unstructured data that you need to parse
* Destination Log Project: is the place where structured logs are stored, the data has been parsed into structured form after running through the Log Pipeline system. There are 2 destination log projects to receive different logs. For example, destination log project 1 receives nginx logs data has been parsed, destination log project 2 receives parsed apache logs data
* Log Pipeline contains 2 Processor Groups with Filters source:nginx and source:apache. Corresponding log lines that match the Group's Filter will be parsed accordingly to that Group.
* Processor Group: there are 2 corresponding Processor Groups to properly parse logs and store them in 2 different destination log projects.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FehjFL5yIuSwiT7byVzuh%252Fimage.png%3Falt%3Dmedia%26token%3Dca40647e-9401-4e79-9b76-2856cd8c08cf&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1b58a924&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

## Log pipeline limited scope <a href="#lamviecvoilogpipeline-phamvigioihanlogpipeline" id="lamviecvoilogpipeline-phamvigioihanlogpipeline"></a>

**Log pipeline naming rules**

The following rules apply to Log pipeline naming in vMonitor Platform:

* The Log pipeline name must be between 1 (minimum) and 63 (maximum) characters long.
* Log pipeline names can only include lowercase letters (a-z,), numbers (0-9), hyphens (-).
* Log pipeline names must begin with a letter and end with a letter or a number.
* The Log pipeline name should not contain sensitive information (eg IP address, account name, login password,...).
* The Log pipeline name must be unique within a GreenNode account until that Log pipeline is deleted.

**Processor group naming rules**

The following rules apply to Processor group naming in vMonitor Platform:

* Processor group name must be from 1 (minimum) to 63 (maximum) characters.
* Processor group names can only include lowercase letters (az,), numbers (0-9), hyphens (-).
* Processor group names must begin with a letter and end with a letter or a number.
* The Processor group name should not contain sensitive information (eg IP address, account name, login password,...).
* The Processor group name must be unique within a GreenNode account until that Processor group is deleted.

**Processor naming rules**

The following rules apply to Processor naming in vMonitor Platform:

* Processor name must be from 1 (minimum) to 63 (maximum) characters long.
* Processor names can only include lowercase letters (az,), numbers (0-9), hyphens (-).
* Processor names must begin with a letter and end with a letter or a number.
* Processor name should not contain sensitive information (eg IP address, account name, login password,...).
* Processor name must be unique within a GreenNode account until that Processor is deleted.

***

## Initialize Log pipeline <a href="#lamviecvoilogpipeline-khoitaologpipeline" id="lamviecvoilogpipeline-khoitaologpipeline"></a>

To create a log pipeline, follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor/) .
2. **Select the Log** folder , then select the **Log pipeline** menu .
3. Select **Create a Log pipeline** .
4. Enter **Pipeline name** . The pipeline name must comply with our rules described above.
5. Enter **Pipeline description** if available.
6. Select **Create.**

***

## Edit Log pipeline <a href="#lamviecvoilogpipeline-chinhsualogpipeline" id="lamviecvoilogpipeline-chinhsualogpipeline"></a>

To edit a log pipeline, follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select the Log folder **.**
3. Select **Log pipeline.**
4. In the list of existing log pipelines, at **the Log pipeline** you want to edit, select ![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FNYVs1TBqc044WNqQ0sbv%252Fimage.png%3Falt%3Dmedia%26token%3D94dbb161-89f1-486a-b0d7-4db0b6d8aa62\&width=32\&dpr=4\&quality=100\&sign=71d78aa4\&sv=1).
5. Select **Edit pipeline** .
6. Edit the parameters for **the Log pipeline** as you desire. You can edit all information fields in a Log pipeline configuration. This editing is similar to when you create a new Log pipeline according to the instructions above.
7. Select **Save.**

***

## Delete Log pipeline <a href="#lamviecvoilogpipeline-xoalogpipeline" id="lamviecvoilogpipeline-xoalogpipeline"></a>

When you no longer need to use a custom Log pipeline, you can delete the Log pipeline from the system according to the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select the Log folder **.**
3. At **the Log pipeline** you want to delete, select![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FKzv1Impf4FlmWXpgefNh%252Fimage.png%3Falt%3Dmedia%26token%3Dcfcd9532-f7bd-435d-9c4f-5027ad6291ac\&width=31\&dpr=4\&quality=100\&sign=8af1a2bd\&sv=1)
4. Select **Delete** .
5. At the Log pipeline deletion confirmation screen, select **Delete** .

After you successfully delete, your Log pipeline will be completely deleted from our system. You cannot restore a deleted Log pipeline, so be careful when using this feature.
