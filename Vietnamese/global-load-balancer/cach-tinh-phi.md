# Cách tính phí

GLB được tính giá dựa trên số lượng Connection và lượng Data. Đối với người dùng trả trước, hệ thống sẽ thực hiện hold credit dựa trên usage hiện tại cho 3 ngày kế tiếp, với người dùng trả sau sẽ thực hiện thanh toán vào đầu tháng kế tiếp.&#x20;

Cụ thể:

## **Tính phí dựa trên số Connection**

* **Công thức:**\
  `Tổng (Số connection tối đa mỗi giờ - Miễn phí) từ đầu tháng đến nay / 720`
  * Nếu kết quả < 100 → Làm tròn lên **100**.
  * Nếu kết quả ≥ 100 → Giữ nguyên.
* **Ví dụ:**
  * **Hạn mức miễn phí:** 4.000 connection.
  * **Ngày 1:** Dùng 10.000 connection → `(10.000 - 4.000) / 720 ≈ 8.33` → Làm tròn thành **100**.
  * **Ngày 30:** Tổng 30 ngày → `(10.000 - 4.000) × 30 / 720 = 250` → Giữ nguyên **250**.

***

## **Tính phí dựa trên lưu lượng dữ liệu (Data)**

* **Công thức:**\
  `Tổng (Lưu lượng tối đa mỗi ngày - Hạn mức miễn phí) từ đầu tháng đến nay`
  * Nếu kết quả âm → Làm tròn thành **0**.
* **Ví dụ:**
  * **Hạn mức miễn phí:**
    * Traffic trong nước (Domestic): 500GB
    * Traffic quốc tế (International): 50GB
  * **Ngày 1:**
    * Dùng 50GB (trong nước) → `50 - 500 = -450` → Làm tròn thành **0**.
    * Dùng 5GB (quốc tế) → `5 - 50 = -45` → Làm tròn thành **0**.
  * **Ngày 11:**
    * Dùng 550GB (trong nước) → `550 - 500 = 50` → Tính **50GB**.
    * Dùng 55GB (quốc tế) → `55 - 50 = 5` → Tính **5GB**.

#### **Lưu ý quan trọng:**

* Khi phát sinh phí, hệ thống sẽ tính toán và **cộng dồn vào hold** (tạm giữ) cho những ngày tiếp theo.
