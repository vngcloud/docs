# Thông số tích hợp với Terreform

\
Nội dung

* [Những thông số truyền từ Terreform ](thong-so-tich-hop-voi-terreform.md#thongsotichhopvoiterreform-nhungthongsotruyentuterreform)
* [Những thuộc tính truyền cho Terreform](thong-so-tich-hop-voi-terreform.md#thongsotichhopvoiterreform-nhungthuoctinhtruyenchoterreform)

## Những thông số truyền từ Terreform  <a href="#thongsotichhopvoiterreform-nhungthongsotruyentuterreform" id="thongsotichhopvoiterreform-nhungthongsotruyentuterreform"></a>

***

### Mẫu truyền ví dụ <a href="#thongsotichhopvoiterreform-mautruyenvidu" id="thongsotichhopvoiterreform-mautruyenvidu"></a>

| resource "vngcloud\_vserver\_server" "server"{    project\_id = "pro-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    name = "example-server"    encryption\_volume = false    flavor\_id = "flav-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    image\_id = "img-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    network\_id = "net-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    root\_disk\_size = 20    root\_disk\_type\_id = "vtype-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    ssh\_key = "ssh-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"    security\_group = \["secg-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"]    subnet\_id = "sub-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"} |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### Các tham số (Arguments) <a href="#thongsotichhopvoiterreform-cacthamso-arguments" id="thongsotichhopvoiterreform-cacthamso-arguments"></a>

<table data-header-hidden data-full-width="true"><thead><tr><th width="74"></th><th width="112"></th><th width="116"></th><th width="114"></th><th width="200"></th><th></th></tr></thead><tbody><tr><td><strong>No.</strong></td><td><strong>Thông số</strong></td><td><strong>Bắt buộc</strong></td><td><strong>Loại dữ liệu</strong></td><td><strong>Mô tả</strong></td><td><strong>Dữ liệu mẫu</strong></td></tr><tr><td>1</td><td><em>project_id</em></td><td><mark style="background-color:red;">BẮT BUỘC</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của Project.</td><td>pro-462803f3-6858-466f-bf05-df2b33faa360</td></tr><tr><td>2</td><td><em>name</em></td><td><mark style="background-color:red;">BẮT BUỘC</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Tên của Server.</td><td>example-server-name</td></tr><tr><td>3</td><td><em>encryption_volume</em></td><td><mark style="background-color:red;">BẮT BUỘC</mark></td><td><mark style="background-color:orange;">BOOLEAN</mark></td><td>Server có dùng các Volume mã hóa hay không?</td><td>False</td></tr><tr><td>4</td><td><em>flavor_id</em></td><td><mark style="background-color:red;">BẮT BUỘC</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của Flavor.</td><td>flav-e2028a81-cc75-47e4-8af1-9eef2f857f84</td></tr><tr><td>5</td><td><em>image_id</em></td><td><mark style="background-color:red;">BẮT BUỘC</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của Image.</td><td>img-b5bf635e-0456-4765-b493-31d5fcfc05aa</td></tr><tr><td>6</td><td><em>network_id</em></td><td><mark style="background-color:red;">BẮT BUỘC</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của Network.</td><td>net-961d6867-b65a-40ac-879e-d84e4dc768e0</td></tr><tr><td>7</td><td><em>root_disk_size</em></td><td><mark style="background-color:red;">BẮT BUỘC</mark></td><td><mark style="background-color:blue;">NUMBER</mark></td><td>Kích thước của boot volume.</td><td>20</td></tr><tr><td>8</td><td><em>root_disk_type_id</em></td><td><mark style="background-color:red;">BẮT BUỘC</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của loại boot volume.</td><td>vtype-bacd68a4-8758-4fb6-a739-b047665e05d5</td></tr><tr><td>9</td><td><em>ssh_key</em></td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của SSH key.</td><td>ssh-7bd70c56-1f05-4989-a0f0-cc3496b62001</td></tr><tr><td>10</td><td><em>security_group</em></td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của Security group.</td><td>secg-3b12a078-b862-43b5-a56b-d7fc4429e535</td></tr><tr><td>11</td><td><em>subnet_id</em></td><td><mark style="background-color:red;">BẮT BUỘC</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của subnet.</td><td>sub-c1ebba8f-baa8-434c-beb7-2916199bb812</td></tr><tr><td>12</td><td>host_group_id</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của Host Group.</td><td>/</td></tr><tr><td>13</td><td>action</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Những hành động với Server. Các hành động đó có thể là: stop; start; reboot.</td><td>start</td></tr><tr><td>14</td><td>attach_floating</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:orange;">BOOLEAN</mark></td><td>Server có được gắn floating IP không?</td><td>True</td></tr><tr><td>15</td><td>expire_password</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:orange;">BOOLEAN</mark></td><td>Bỏ qua thay đổi password thì false, nếu không thì true.</td><td>False</td></tr><tr><td>16</td><td>os_licence</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:orange;">BOOLEAN</mark></td><td>Bản quyền của Hệ điều hành OS.</td><td>True</td></tr><tr><td>17</td><td>root_disk_encryption_type</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Kiểu mã hóa của boot volume.</td><td>/</td></tr><tr><td>18</td><td>source_type</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Loại Source.</td><td>/</td></tr><tr><td>19</td><td>user_name</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Tên của User.</td><td>usernamestackops</td></tr><tr><td>20</td><td>user_password</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mật khẩu của USer.</td><td>VngGCloud3030</td></tr><tr><td>21</td><td>server_group</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>Mã của Server Group.</td><td>/</td></tr><tr><td>22</td><td>user_data</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:green;">STRING</mark></td><td>User_data được cung cấp khi kích hoạt sử dụng server.</td><td>${data.template_cloudinit_config.user_data.rendered}</td></tr><tr><td>23</td><td>user_data_base64_encode</td><td><mark style="background-color:purple;">TÙY CHỌN</mark></td><td><mark style="background-color:orange;">BOOLEAN</mark></td><td>Có được sử dụng trực tiếp mã hóa dữ liệu nhị phân base64 thay  vì user_data thường không? Việc sử dụng này thay cho User_data bất cứ khi nào  giá trị không phải là chuỗi UTF-8 hợp lệ.</td><td>True</td></tr></tbody></table>

{% hint style="info" %}
**Lưu ý**

Khi Server đã hết hạn và trạng thái là Kết thúc (Terminated). Nếu User muốn gia hạn (renew) tài nguyên (resource) thì **User phải vào User Portal để gia hạn nếu sử dụngTerreform**, vì Terreform không có chức năng gia hạn.
{% endhint %}

## **Những thuộc tính truyền cho Terreform** <a href="#thongsotichhopvoiterreform-nhungthuoctinhtruyenchoterreform" id="thongsotichhopvoiterreform-nhungthuoctinhtruyenchoterreform"></a>

***

Sau khi VNG Cloud ghi nhận các thông số truyền từ Terreform, sẽ có những thuộc tính sau được xuất ra cho Terreform cho user sử dụng:

* **id** STRING : Mã định danh của Server này;
* **external\_interfaces:** Danh sách các thông tin của Network External:
  * **external\_interfaces** STRING;
  * **floating\_ip** STRING;
  * **interface\_type**STRING;
  * **mac** STRING;
  * **network\_uuid** STRING;
  * **port\_uuid** STRING;
  * **status** STRING;
  * **subnet\_uuid** STRING;
  * **type** STRING;
* **internal\_interfaces:** Danh sách các thông tin của Network External:&#x20;
  * **external\_interfaces** STRING;
  * **floating\_ip** STRING;
  * **interface\_type** STRING;
  * **mac** STRING;
  * **network\_uuid** STRING;
  * **port\_uuid** STRING;
  * **status** STRING;
  * **subnet\_uuid** STRING;
  * **type** STRING./.

\
