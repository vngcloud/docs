# Argument Intergration with Terreform

{% hint style="info" %}
**Nội dung**

* [Arguments tranfer from Terreform](https://docs.vngcloud.vn/display/VSERVERENG/Argument+Intergration+with+Terreform#ArgumentIntergrationwithTerreform-ArgumentstranferfromTerreform)
* [Attributes transfer to Terreform](https://docs.vngcloud.vn/display/VSERVERENG/Argument+Intergration+with+Terreform#ArgumentIntergrationwithTerreform-AttributestransfertoTerreform)
{% endhint %}

## **Arguments tranfer from Terreform** <a href="#argumentintergrationwithterreform-argumentstranferfromterreform" id="argumentintergrationwithterreform-argumentstranferfromterreform"></a>

***

#### Example Usage <a href="#argumentintergrationwithterreform-exampleusage" id="argumentintergrationwithterreform-exampleusage"></a>

| `resource "vngcloud_vserver_server"` `"server"{    project_id = "pro-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    name = "example-server"    encryption_volume = false    flavor_id = "flav-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    image_id = "img-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    network_id = "net-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    root_disk_size = 20    root_disk_type_id = "vtype-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    ssh_key = "ssh-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    security_group = ["secg-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"]    subnet_id = "sub-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}` |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### Arguments Reference <a href="#argumentintergrationwithterreform-argumentsreference" id="argumentintergrationwithterreform-argumentsreference"></a>

<table data-header-hidden><thead><tr><th width="107"></th><th></th><th></th><th width="117"></th><th width="131"></th><th></th></tr></thead><tbody><tr><td>No.</td><td>Arguments</td><td>Required</td><td>Data Type</td><td>Description</td><td>Example Data</td></tr><tr><td>1</td><td><em>project_id</em></td><td>REQUIRED</td><td>STRING</td><td>ID of the Project.</td><td><pre><code>pro-462803f3-6858-466f-bf05-df2b33faa360
</code></pre></td></tr><tr><td>2</td><td><em>name</em></td><td>REQUIRED</td><td>STRING</td><td>Name of Server.</td><td><pre><code>example-server-name
</code></pre></td></tr><tr><td>3</td><td><em>encryption_volume</em></td><td>REQUIRED</td><td>BOOLEAN</td><td>Is Server use encryption volume?</td><td><pre><code>False
</code></pre></td></tr><tr><td>4</td><td><em>flavor_id</em></td><td>REQUIRED</td><td>STRING</td><td>ID of the Flavor.</td><td><pre><code>flav-e2028a81-cc75-47e4-8af1-9eef2f857f84
</code></pre></td></tr><tr><td>5</td><td><em>image_id</em></td><td>REQUIRED</td><td>STRING</td><td>ID of the Image.</td><td><pre><code>img-b5bf635e-0456-4765-b493-31d5fcfc05aa
</code></pre></td></tr><tr><td>6</td><td><em>network_id</em></td><td>REQUIRED</td><td>STRING</td><td>ID of Network.</td><td><pre><code>net-961d6867-b65a-40ac-879e-d84e4dc768e0
</code></pre></td></tr><tr><td>7</td><td><em>root_disk_size</em></td><td>REQUIRED</td><td>NUMBER</td><td>Size of boot volume.</td><td><pre><code>20
</code></pre></td></tr><tr><td>8</td><td><em>root_disk_type_id</em></td><td>REQUIRED</td><td>STRING</td><td>ID of boot volume type.</td><td><pre><code>vtype-bacd68a4-8758-4fb6-a739-b047665e05d5
</code></pre></td></tr><tr><td>9</td><td><em>ssh_key</em></td><td>OPTIONAL</td><td>STRING</td><td>ID of SSH key.</td><td><pre><code>ssh-7bd70c56-1f05-4989-a0f0-cc3496b62001
</code></pre></td></tr><tr><td>10</td><td><em>security_group</em></td><td>OPTIONAL</td><td>STRING</td><td>ID of Security Group.</td><td><pre><code>secg-3b12a078-b862-43b5-a56b-d7fc4429e535
</code></pre></td></tr><tr><td>11</td><td><em>subnet_id</em></td><td>REQUIRED</td><td>STRING</td><td>ID of the subnet.</td><td><pre><code>sub-c1ebba8f-baa8-434c-beb7-2916199bb812
</code></pre></td></tr><tr><td>12</td><td>host_group_id</td><td>OPTIONAL</td><td>STRING</td><td>ID of Host Group.</td><td>/</td></tr><tr><td>13</td><td>action</td><td>OPTIONAL</td><td>STRING</td><td>Action with Server. It can be: stop, start; reboot.</td><td>start</td></tr><tr><td>14</td><td>attach_floating</td><td>OPTIONAL</td><td>BOOLEAN</td><td>Is Server attach a floating IP?</td><td>True</td></tr><tr><td>15</td><td>expire_password</td><td>OPTIONAL</td><td>BOOLEAN</td><td>Skip change password: false, else: true.</td><td>False</td></tr><tr><td>16</td><td>os_licence</td><td>OPTIONAL</td><td>BOOLEAN</td><td>License of OS.</td><td>True</td></tr><tr><td>17</td><td>root_disk_encryption_type</td><td>OPTIONAL</td><td>STRING</td><td>Type encryption of boot volume.</td><td>/</td></tr><tr><td>18</td><td>source_type</td><td>OPTIONAL</td><td>STRING</td><td>Type of Source.</td><td>/</td></tr><tr><td>19</td><td>user_name</td><td>OPTIONAL</td><td>STRING</td><td>Name of User.</td><td>usernamestackops</td></tr><tr><td>20</td><td>user_password</td><td>OPTIONAL</td><td>STRING</td><td>Password of User.</td><td>VngGCloud3030</td></tr><tr><td>21</td><td>server_group</td><td>OPTIONAL</td><td>STRING</td><td>ID của Server Group.</td><td>/</td></tr><tr><td>22</td><td>user_data</td><td>OPTIONAL</td><td>STRING</td><td>User_data to provide when launching the server.</td><td>${data.template_cloudinit_config.user_data.rendered}</td></tr><tr><td>23</td><td>user_data_base64_encode</td><td>OPTIONAL</td><td>BOOLEAN</td><td>Can be used instead of user_data to pass base64-encoded binary data directly. Use this instead of user_data whenever the value is not a valid UTF-8 string.</td><td>True</td></tr></tbody></table>

Importance

* When a resource is expired and status be Terminated, if User would like to renew a resource, **User must to implement Renew in User Portal when using Terreform**, due to Terreform does not have the ability to renew.&#x20;

## Attributes transfer to Terreform <a href="#argumentintergrationwithterreform-attributestransfertoterreform" id="argumentintergrationwithterreform-attributestransfertoterreform"></a>

***

When VNG Cloud System has recorded all arguments above from Terreform, the following attributes are exported:&#x20;

* **id** STRING : ID of this Server
* **external\_interfaces:** (List of Map of String) List of Network external interface. It included:
  * **external\_interfaces** STRING
  * **floating\_ip** STRING
  * **interface\_type**STRING
  * **mac** STRING
  * **network\_uuid** STRING
  * **port\_uuid** STRING
  * **status** STRING
  * **subnet\_uuid** STRING
  * **type** STRING
* **internal\_interfaces:** (List of Map of String) List of Network external interface. It included:&#x20;
  * **external\_interfaces** STRING
  * **floating\_ip** STRING
  * **interface\_type** STRING
  * **mac** STRING
  * **network\_uuid** STRING
  * **port\_uuid** STRING
  * **status** STRING
  * **subnet\_uuid** STRING
  * **type** STRING
