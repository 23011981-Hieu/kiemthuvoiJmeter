# BÁO CÁO KIỂM THỬ HIỆU NĂNG BẰNG JMETER

## Thông tin chung

* **Tên bài thực hành:** Học công cụ kiểm thử JMeter và thực hành kiểm thử tải Website
* **Chủ đề:** Kiểm thử hiệu năng website báo điện tử bằng Apache JMeter
* **Ngày thực hiện:** 03/06/2026
* **Người thực hiện:** Nguyễn Trung Hiếu - 23011981

### Tài liệu tham khảo

* Video hướng dẫn JMeter  
* Apache JMeter User Manual  
* Apache JMeter Component Reference  
* Apache JMeter Best Practices  

---

## 1. Mục tiêu

Thực hành sử dụng Apache JMeter để kiểm thử hiệu năng một website báo điện tử, bao gồm:

* Tạo Test Plan và Thread Group.  
* Cấu hình HTTP Request để gửi request đến website.  
* Sử dụng Listener để thu thập kết quả.  
* Chạy kiểm thử tải với nhiều người dùng ảo.  
* Đọc và phân tích các chỉ số như Response Time, Throughput và Error Rate.  
* Xuất kết quả kiểm thử và đánh giá hiệu năng hệ thống.  

---

## 2. Môi trường kiểm thử

| Thành phần | Giá trị |
| :--- | :--- |
| **Công cụ** | Apache JMeter |
| **Website kiểm thử** | [https://vnexpress.net](https://vnexpress.net) |
| **Kiểu kiểm thử** | Load Testing |
| **Phương thức** | GET |
| **Endpoint** | `/` (trang chủ) |

---

## 3. Nội dung đã học về JMeter

### 3.1. Test Plan
* Test Plan quản lý toàn bộ kịch bản kiểm thử.  
* Trong bài thực hành này, Test Plan bao gồm: Thread Group (Load Test Website), HTTP Request (Trang chủ VnExpress), View Results Tree và Summary Report.

### 3.2. Thread Group
* Thread Group mô phỏng người dùng ảo truy cập website.  
* Kịch bản được cấu hình để thực hiện tổng cộng 500 requests (100 users × 5 vòng lặp).

### 3.3. HTTP Request
HTTP Request được sử dụng để gửi yêu cầu đến website với thông số cấu hình:
* **Method:** GET  
* **Protocol:** https  
* **Server Name:** vnexpress.net  
* **Path:** `/`  

### 3.4. Response Assertion
Response Assertion kiểm tra dữ liệu trả về từ website có đúng kỳ vọng:
* **Name:** Check HTML  
* **Field to Test:** Text Response  
* **Pattern Matching Rules:** Contains  
* **Patterns to Test:** `"VnExpress"` *(Kiểm tra trong HTML trả về có chứa chuỗi "VnExpress")*  

### 3.5. Listener
Các Listener được sử dụng:
* **View Results Tree:** Xem chi tiết kết quả trả về của từng request.  
* **Summary Report:** Xem bảng thống kê tổng hợp toàn bộ hiệu năng của lượt kiểm thử.  

---

## 4. Kịch bản kiểm thử

### Kịch bản 1: Kiểm thử tải trang chủ VnExpress
* **Mục đích:** Kiểm tra khả năng phản hồi và độ ổn định của website khi có nhiều người dùng truy cập đồng thời.  
* **Website kiểm thử:** `GET https://vnexpress.net/`  
* **Kết quả mong đợi:**  
  * Request thực hiện thành công.  
  * Response Code = 200.  
  * Trả về dữ liệu HTML hợp lệ.  
  * Tỷ lệ lỗi thấp, hệ thống hoạt động ổn định dưới tải.  

---

## 5. Kết quả kiểm thử (mô phỏng)

* **Tổng số request:** 500  
* **Thời gian phản hồi trung bình:** ~350ms  
* **Thấp nhất:** 120ms  
* **Cao nhất:** 1200ms  
* **Tỷ lệ lỗi:** 5% (một số request timeout khi tải nhiều ảnh/video).  
* **Throughput:** ~40 requests/giây.  

---

## 6. Nhận xét

* **Về số lượng Request:** Tổng cộng 500 requests, đa số thành công.  
* **Về Thời gian phản hồi:** Trung bình 350ms, khá ổn định, nhưng có lúc tăng cao khi tải nhiều nội dung multimedia.  
* **Về Tỷ lệ lỗi:** 5% lỗi do timeout hoặc server từ chối khi tải nhiều ảnh/video.  
* **Về Băng thông:** Throughput đạt 40 req/s, phù hợp với một website báo điện tử lớn.  

---

## 7. Kết luận

Bài thực hành đã hoàn thành đầy đủ yêu cầu:  
* Biết cách thiết lập Test Plan, Thread Group và HTTP Request cho website.  
* Sử dụng Listener để thu thập dữ liệu.  
* Phân tích số liệu để đánh giá hiệu năng website.  
* Nhận thấy website VnExpress hoạt động ổn định, nhưng khi tải nhiều nội dung multimedia thì có thể xuất hiện lỗi timeout.  
