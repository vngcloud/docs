# Search logs

#### Using <a href="#searchlogs-cachsudung" id="searchlogs-cachsudung"></a>

In **area 2 - where you enter log search information** : we support you with 2 search methods: **Suggestion mode and Editor mode.**

* **Suggestion mode** (default): we will display suggestions for all the fields of the incoming logs for you to choose from (you should choose fields with the suffix keyword so we can always suggest the available value of the logs). field for you). The search will have the most accurate results when you enter the correct **Fields \<Operator> Value** syntax .

For example, to filter log records with HTTP method GET within the last 15 minutes, select query as http\_method.keyword = 'GET' and set time range to 15m..

<figure><img src="../../../../.gitbook/assets/image (33) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Editor mode** : by default when you search logs, we will enable **Suggestion mode** . To use Editor mode, select the icon **Edit**. When the screen displays **Search log entries with Editor mode**, you can start entering filters through Editor mode. The syntax for entering a query is similar to Suggestion mode: **Fields \<Operator> Value.** For example, if you enter http\_method.keyword = "GET", the system will search for all log records with field http\_method.keyword = "GET".

<figure><img src="../../../../.gitbook/assets/image (34) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

After selecting **Suggestion mode** or importing in **Editor mode** , you can:

* Press **Enter** or select the icon **Search** to perform a search for logs.
* Select this icon **Close** if you want to delete all entered/selected filter conditions.

***

#### Usage situations <a href="#searchlogs-tinhhuongsudung" id="searchlogs-tinhhuongsudung"></a>

* **Simple syntax (single query)**
  * **To search for logs, you need to select/enter according to the Fields \<Operator> Value** syntax . **In there:**
    * **Field** : list of fields in the log project you are selecting.
    * **Operator** : we provide you with the operations described in the table below:
    * **Value** : the value of the field is suggested or you enter yourself.

<table data-header-hidden><thead><tr><th width="136"></th><th width="238"></th><th></th></tr></thead><tbody><tr><td><p><strong>Math</strong></p><p><strong>(Operator)</strong></p></td><td><strong>Describe</strong></td><td><strong>Illustration</strong></td></tr><tr><td>=</td><td>equal some value</td><td>host = "ABC" - The system will find log records with field host = "ABC".</td></tr><tr><td>!=</td><td>not equal some value</td><td>host != "ABC" - The system will look for log records with field types other than "ABC".</td></tr><tr><td>:*</td><td>exists is any form</td><td>type.keyword :* - The system will find log records where the host field exists. (Existence means the host field appears in the log line, regardless of the value of the host field).</td></tr><tr><td>!:*</td><td>not exists</td><td>type.keyword !:* - The system will find log records that do not exist in the host field. (Non-existent means the host field does not appear in the log line).</td></tr><tr><td>&#x3C;</td><td>less than some value</td><td>@timestamp &#x3C; "1690772380191" - The system will find log records with timestamp field less than the value 1690772380191.</td></tr><tr><td>></td><td>greater than some value</td><td>@timestamp > "1690772380191" - The system will find log records with timestamp field greater than the value 1690772380191.</td></tr><tr><td>&#x3C;=</td><td>less than or equal to some value</td><td>@timestamp &#x3C;= "1690772380191" - The system will find log records with timestamp field less than or equal to the value 1690772380191.</td></tr><tr><td>>=</td><td>greater than equal to some value</td><td>@timestamp >= "1690772380191" - The system will find log records with timestamp field greater than or equal to the value 1690772380191.</td></tr></tbody></table>

* **Complex syntax (complex query with boolean operator)**
  * You can combine multiple Single queries into a Complex query using the syntax **Field \<Operator> Value \<AND/OR> Field \<Operator> Value... In which:**
    * **Field** : list of fields in the log project you are selecting.
    * **Operator** : we provide you with the operations described in the table above.
    * **Value** : the value of the field is suggested or you enter yourself.
    * **Boolean operator** : we provide you the concatenation operations described in the table below:

<table data-header-hidden><thead><tr><th width="162"></th><th width="215"></th><th></th></tr></thead><tbody><tr><td><p><strong>Concatenation operation</strong></p><p><strong>(Operator)</strong></p></td><td><strong>Describe</strong></td><td><strong>Illustration</strong></td></tr><tr><td>AND</td><td>equal some value</td><td>http_method.keyword = "POST" AND response_code.keyword = "404" - The system will look for log records with field http_method.keyword = "POST" and field response_code.keyword = "404."</td></tr><tr><td>OR</td><td>not equal some value</td><td>http_method.keyword = "POST" OR response_code.keyword = "404" - The system will look for log records with field http_method.keyword = "POST" or field response_code.keyword = "404."</td></tr></tbody></table>

<figure><img src="../../../../.gitbook/assets/image (35) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Query with for a piece of content**
  * You can search for a piece of content by entering GET directly into the search field. For example, if you enter the text GET, the system will search all log records in which any data field appears this string of characters.

<figure><img src="../../../../.gitbook/assets/image (36) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
