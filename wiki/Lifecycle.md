Cho phép thiết lập rule hành xử khi object kết thúc vòng đời. 

![](images/storage/image2020-6-8_15-24-34.png)


# Lifecyle gồm 2 loại rules là:  

*  **Transition rule:** Di chuyển object giữa các class. 
    *  **Days after creation:**  Rule sẽ xác định các object đạt đủ điều kiện về số ngày tính từ lúc object được upload lên và chuyển từ Standard (Gold) sang vColdcstorage class. 
    *  **Day after last seen** : Rule sẽ chuyển object từ  **Standard (Gold)**  sang  **Silver**  nếu **lần cuối cùng object được truy cập**  bởi end-user thỏa điều kiện. 

    
*  **Expiration rule:**  Rule sẽ xác định các object đạt đủ điều kiện về số ngày tính từ lúc object được upload lên / hoặc kể từ ngày object được chuyển sang class mới và xóa các object này. 

Tùy theo use-case mà bạn có thể thiết lập cả 2 rule cho 1 Lifecycle hoặc chỉ 1.


# Phạm vi áp dụng:
Lifecycle rule sẽ chỉ hoạt động trên 1 container

Lifecycle rule sẽ hoạt động trên các object / folder thỏa điều kiện đặt ra gồm:

-         **Prefix :**  Tiền tố , ký tự đầu của object bạn muốn rule sẽ áp dụng. Mỗi lifecycle rule sẽ chỉ được chọn 1 prefix duy nhất.


* Nhập prefix của object để xác định phạm vi object bị tác động bởi rule.
* Nhập “ / “ để áp dụng rule cho toàn bộ object trong container
* Nhập “/<tên folder>” để áp dụng rule cho toàn bộ object trong 1 folder

![](images/storage/image2020-6-8_15-25-18.png)


# Action
Lifecycle rule sẽ chạy 1 lần mỗi ngày, theo thứ tự transition rule sẽ chạy trước rồi đến expiration rule.



*****

[[category.storage-team]] 
[[category.confluence]] 
