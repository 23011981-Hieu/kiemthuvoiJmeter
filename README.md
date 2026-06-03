# Báo cáo kiểm thử JMeter

## Mục tiêu
Kiểm thử hiệu năng website báo điện tử vnexpress.net.

## Công cụ
Apache JMeter (mô phỏng).

## Kịch bản
- 100 users đồng thời
- 5 vòng lặp mỗi user
- Tổng cộng 500 request

## Kết quả
- Thời gian phản hồi TB: 350ms
- Tỷ lệ lỗi: 2%
- Throughput: 40 req/s

## Nhận xét
Website hoạt động ổn định, nhưng khi tải nhiều ảnh/video thì có một số request timeout.
