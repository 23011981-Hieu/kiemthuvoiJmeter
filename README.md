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

| Thành phần           | Giá trị               |
| :------------------- | :-------------------- |
| **Công cụ**          | Apache JMeter         |
| **Website kiểm thử** | https://vnexpress.net |
| **Kiểu kiểm thử**    | Load Testing          |
| **Phương thức**      | GET                   |
| **Endpoint**         | `/` (trang chủ)       |

![Giao diện JMeter](images/anh-2-1.png)

*Hình 2.1. Giao diện làm việc của Apache JMeter.*

---

## 3. Nội dung đã học về JMeter

### 3.1. Test Plan

Test Plan quản lý toàn bộ kịch bản kiểm thử.

Trong bài thực hành này, Test Plan bao gồm: Thread Group (Load Test Website), HTTP Request (Trang chủ VnExpress), View Results Tree và Summary Report.

![Test Plan](images/anh-3-1.png)

*Hình 3.1. Cấu trúc Test Plan sử dụng trong bài thực hành.*

### 3.2. Thread Group

Thread Group mô phỏng người dùng ảo truy cập website.

Kịch bản được cấu hình để thực hiện tổng cộng 500 requests (100 users × 5 vòng lặp).

![Thread Group](images/anh-3-2.png)

*Hình 3.2. Cấu hình Thread Group mô phỏng 100 người dùng.*

### 3.3. HTTP Request

HTTP Request được sử dụng để gửi yêu cầu đến website với thông số cấu hình:

* **Method:** GET
* **Protocol:** https
* **Server Name:** vnexpress.net
* **Path:** /

![HTTP Request](images/anh-3-3.png)

*Hình 3.3. Cấu hình HTTP Request gửi yêu cầu đến trang chủ VnExpress.*

### 3.4. Response Assertion

Response Assertion kiểm tra dữ liệu trả về từ website có đúng kỳ vọng:

* **Name:** Check HTML
* **Field to Test:** Text Response
* **Pattern Matching Rules:** Contains
* **Patterns to Test:** "VnExpress"

![Response Assertion](images/anh-3-4.png)

*Hình 3.4. Thiết lập Response Assertion kiểm tra nội dung phản hồi.*

### 3.5. Listener

Các Listener được sử dụng:

* **View Results Tree:** Xem chi tiết kết quả trả về của từng request.
* **Summary Report:** Xem bảng thống kê tổng hợp toàn bộ hiệu năng của lượt kiểm thử.

![View Results Tree](images/anh-3-5.png)

*Hình 3.5. Kết quả phản hồi của một request trong View Results Tree.*

---

## 4. Kịch bản kiểm thử

### Kịch bản 1: Kiểm thử tải trang chủ VnExpress

* **Mục đích:** Kiểm tra khả năng phản hồi và độ ổn định của website khi có nhiều người dùng truy cập đồng thời.
* **Website kiểm thử:** `GET https://vnexpress.net/`

**Kết quả mong đợi:**

* Request thực hiện thành công.
* Response Code = 200.
* Trả về dữ liệu HTML hợp lệ.
* Tỷ lệ lỗi thấp, hệ thống hoạt động ổn định dưới tải.

---

## 5. Kết quả kiểm thử

Sau khi thực hiện kiểm thử tải đối với trang chủ VnExpress bằng Apache JMeter với cấu hình 100 người dùng ảo và 5 vòng lặp, hệ thống ghi nhận các kết quả như sau:

| Chỉ số                                  | Giá trị            |
| --------------------------------------- | ------------------ |
| Tổng số request (Samples)               | 500                |
| Thời gian phản hồi trung bình (Average) | 1610 ms            |
| Thời gian phản hồi nhỏ nhất (Min)       | 15 ms              |
| Thời gian phản hồi lớn nhất (Max)       | 6587 ms            |
| Độ lệch chuẩn (Std. Dev.)               | 1320.21 ms         |
| Tỷ lệ lỗi (Error %)                     | 25.80%             |
| Throughput                              | 30.8 requests/giây |
| Received KB/sec                         | 6947.12 KB/s       |
| Sent KB/sec                             | 3.46 KB/s          |
| Avg. Bytes                              | 230616.9 bytes     |

![Summary Report](images/anh-5-1.png)

*Hình 5.1. Kết quả thống kê hiệu năng từ Summary Report.*

Kết quả cho thấy hệ thống đã xử lý được phần lớn các yêu cầu truy cập. Thời gian phản hồi trung bình đạt 1610 ms, trong khi thời gian phản hồi lớn nhất lên tới 6587 ms.

---

## 6. Nhận xét

### Về số lượng Request

Tổng cộng 500 requests đã được gửi tới trang chủ VnExpress trong quá trình kiểm thử tải.

### Về thời gian phản hồi

Thời gian phản hồi trung bình là 1610 ms. Mặc dù phần lớn các request được xử lý thành công, thời gian phản hồi lớn nhất đạt 6587 ms cho thấy hệ thống có thời điểm phản hồi chậm khi chịu tải cao.

### Về độ ổn định

Độ lệch chuẩn đạt 1320.21 ms, cho thấy thời gian phản hồi giữa các request có sự dao động tương đối lớn.

### Về tỷ lệ lỗi

Tỷ lệ lỗi đạt 25.80%, tương đương khoảng 129 request gặp lỗi trên tổng số 500 request.

### Về Throughput

Throughput đạt 30.8 requests/giây, cho thấy hệ thống vẫn duy trì khả năng xử lý tương đối tốt dưới tải nhưng chưa đạt hiệu năng tối ưu khi lượng truy cập tăng cao.

---

## 7. Kết luận

Bài thực hành đã hoàn thành đầy đủ các yêu cầu đặt ra:

* Thiết lập thành công Test Plan trong Apache JMeter.
* Cấu hình Thread Group để mô phỏng người dùng ảo.
* Sử dụng HTTP Request để gửi yêu cầu tới website VnExpress.
* Sử dụng Response Assertion để kiểm tra nội dung phản hồi.
* Thu thập dữ liệu bằng View Results Tree và Summary Report.
* Phân tích các chỉ số hiệu năng như Response Time, Throughput và Error Rate.

Kết quả kiểm thử cho thấy website VnExpress có khả năng xử lý tốt số lượng lớn yêu cầu truy cập đồng thời. Tuy nhiên, khi tải tăng cao, hệ thống xuất hiện tỷ lệ lỗi khoảng 25.80% và thời gian phản hồi có thể tăng lên hơn 6 giây.
