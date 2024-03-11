# Thông số tích hợp với Terreform

\
Nội dung

* [Những thông số truyền từ Terreform ](https://docs.vngcloud.vn/pages/viewpage.action?pageId=73760855#Th%C3%B4ngs%E1%BB%91t%C3%ADchh%E1%BB%A3pv%E1%BB%9BiTerreform-Nh%E1%BB%AFngth%C3%B4ngs%E1%BB%91truy%E1%BB%81nt%E1%BB%ABTerreform)
* [Những thuộc tính truyền cho Terreform](https://docs.vngcloud.vn/pages/viewpage.action?pageId=73760855#Th%C3%B4ngs%E1%BB%91t%C3%ADchh%E1%BB%A3pv%E1%BB%9BiTerreform-Nh%E1%BB%AFngthu%E1%BB%99ct%C3%ADnhtruy%E1%BB%81nchoTerreform)

## **Những thông số truyền từ Terreform**  <a href="#thongsotichhopvoiterreform-nhungthongsotruyentuterreform" id="thongsotichhopvoiterreform-nhungthongsotruyentuterreform"></a>

***

#### Mẫu truyền ví dụ <a href="#thongsotichhopvoiterreform-mautruyenvidu" id="thongsotichhopvoiterreform-mautruyenvidu"></a>

| `resource "vngcloud_vserver_server"` `"server"{    project_id = "pro-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    name = "example-server"    encryption_volume = false    flavor_id = "flav-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    image_id = "img-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    network_id = "net-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    root_disk_size = 20    root_disk_type_id = "vtype-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    ssh_key = "ssh-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    security_group = ["secg-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"]    subnet_id = "sub-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}` |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### Các tham số (Arguments) <a href="#thongsotichhopvoiterreform-cacthamso-arguments" id="thongsotichhopvoiterreform-cacthamso-arguments"></a>

<table data-header-hidden><thead><tr><th width="76"></th><th width="117"></th><th></th><th width="120"></th><th width="177"></th><th></th></tr></thead><tbody><tr><td>No.</td><td>Thông số</td><td>Bắt buộc</td><td>Loại dữ liệu</td><td>Mô tả</td><td>Dữ liệu mẫu</td></tr><tr><td>1</td><td><em>project_id</em></td><td>BẮT BUỘC</td><td>STRING</td><td>Mã của Project.</td><td><pre><code>pro-462803f3-6858-466f-bf05-df2b33faa360
</code></pre></td></tr><tr><td>2</td><td><em>name</em></td><td>BẮT BUỘC</td><td>STRING</td><td>Tên của Server.</td><td><pre><code>example-server-name
</code></pre></td></tr><tr><td>3</td><td><em>encryption_volume</em></td><td>BẮT BUỘC</td><td>BOOLEAN</td><td>Server có dùng các Volume mã hóa hay không?</td><td><pre><code>False
</code></pre></td></tr><tr><td>4</td><td><em>flavor_id</em></td><td>BẮT BUỘC</td><td>STRING</td><td>Mã của Flavor.</td><td><pre><code>flav-e2028a81-cc75-47e4-8af1-9eef2f857f84
</code></pre></td></tr><tr><td>5</td><td><em>image_id</em></td><td>BẮT BUỘC</td><td>STRING</td><td>Mã của Image.</td><td><pre><code>img-b5bf635e-0456-4765-b493-31d5fcfc05aa
</code></pre></td></tr><tr><td>6</td><td><em>network_id</em></td><td>BẮT BUỘC</td><td>STRING</td><td>Mã của Network.</td><td><pre><code>net-961d6867-b65a-40ac-879e-d84e4dc768e0
</code></pre></td></tr><tr><td>7</td><td><em>root_disk_size</em></td><td>BẮT BUỘC</td><td>NUMBER</td><td>Kích thước của boot volume.</td><td><pre><code>20
</code></pre></td></tr><tr><td>8</td><td><em>root_disk_type_id</em></td><td>BẮT BUỘC</td><td>STRING</td><td>Mã của loại boot volume.</td><td><pre><code>vtype-bacd68a4-8758-4fb6-a739-b047665e05d5
</code></pre></td></tr><tr><td>9</td><td><em>ssh_key</em></td><td>TÙY CHỌN</td><td>STRING</td><td>Mã của SSH key.</td><td><pre><code>ssh-7bd70c56-1f05-4989-a0f0-cc3496b62001
</code></pre></td></tr><tr><td>10</td><td><em>security_group</em></td><td>TÙY CHỌN</td><td>STRING</td><td>Mã của Security group.</td><td><pre><code>secg-3b12a078-b862-43b5-a56b-d7fc4429e535
</code></pre></td></tr><tr><td>11</td><td><em>subnet_id</em></td><td>BẮT BUỘC</td><td>STRING</td><td>Mã của subnet.</td><td><pre><code>sub-c1ebba8f-baa8-434c-beb7-2916199bb812
</code></pre></td></tr><tr><td>12</td><td>host_group_id</td><td>TÙY CHỌN</td><td>STRING</td><td>Mã của Host Group.</td><td>/</td></tr><tr><td>13</td><td>action</td><td>TÙY CHỌN</td><td>STRING</td><td>Những hành động với Server. Các hành động đó có thể là: stop; start; reboot.</td><td>start</td></tr><tr><td>14</td><td>attach_floating</td><td>TÙY CHỌN</td><td>BOOLEAN</td><td>Server có được gắn floating IP không?</td><td>True</td></tr><tr><td>15</td><td>expire_password</td><td>TÙY CHỌN</td><td>BOOLEAN</td><td>Bỏ qua thay đổi password thì false, nếu không thì true.</td><td>False</td></tr><tr><td>16</td><td>os_licence</td><td>TÙY CHỌN</td><td>BOOLEAN</td><td>Bản quyền của Hệ điều hành OS.</td><td>True</td></tr><tr><td>17</td><td>root_disk_encryption_type</td><td>TÙY CHỌN</td><td>STRING</td><td>Kiểu mã hóa của boot volume.</td><td>/</td></tr><tr><td>18</td><td>source_type</td><td>TÙY CHỌN</td><td>STRING</td><td>Loại Source.</td><td>/</td></tr><tr><td>19</td><td>user_name</td><td>TÙY CHỌN</td><td>STRING</td><td>Tên của User.</td><td>usernamestackops</td></tr><tr><td>20</td><td>user_password</td><td>TÙY CHỌN</td><td>STRING</td><td>Mật khẩu của USer.</td><td>VngGCloud3030</td></tr><tr><td>21</td><td>server_group</td><td>TÙY CHỌN</td><td>STRING</td><td>Mã của Server Group.</td><td>/</td></tr><tr><td>22</td><td>user_data</td><td>TÙY CHỌN</td><td>STRING</td><td>User_data được cung cấp khi kích hoạt sử dụng server.</td><td>${data.template_cloudinit_config.user_data.rendered}</td></tr><tr><td>23</td><td>user_data_base64_encode</td><td>TÙY CHỌN</td><td>BOOLEAN</td><td>Có được sử dụng trực tiếp mã hóa dữ liệu nhị phân base64 thay  vì user_data thường không? Việc sử dụng này thay cho User_data bất cứ khi nào  giá trị không phải là chuỗi UTF-8 hợp lệ.</td><td>True</td></tr></tbody></table>

{% hint style="info" %}
**Lưu ý**

Khi Server đã hết hạn và trạng thái là Kết thúc (Terminated). Nếu User muốn gia hạn (renew) tài nguyên (resource) thì **User phải vào User Portal để gia hạn nếu sử dụngTerreform**, vì Terreform không có chức năng gia hạn.
{% endhint %}

## **Những thuộc tính truyền cho Terreform** <a href="#thongsotichhopvoiterreform-nhungthuoctinhtruyenchoterreform" id="thongsotichhopvoiterreform-nhungthuoctinhtruyenchoterreform"></a>

***

Sau khi VNG Cloud ghi nhận các thông số truyền từ Terreform, sẽ có những thuộc tính sau được xuất ra cho Terreform cho user sử dụng:

* **id** STRING : Mã định danh của Server này;
* **external\_interfaces:** Danh sách các thông tin của Network External:
  * **external\_interfaces** STRING
  * **floating\_ip** STRING
  * **interface\_type**STRING
  * **mac** STRING
  * **network\_uuid** STRING
  * **port\_uuid** STRING
  * **status** STRING
  * **subnet\_uuid** STRING
  * **type** STRING
* **internal\_interfaces:** Danh sách các thông tin của Network External:&#x20;
  * **external\_interfaces** STRING
  * **floating\_ip** STRING
  * **interface\_type** STRING
  * **mac** STRING
  * **network\_uuid** STRING
  * **port\_uuid** STRING
  * **status** STRING
  * **subnet\_uuid** STRING
  * **type** STRING

\
