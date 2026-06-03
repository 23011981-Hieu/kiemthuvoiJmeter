# Báo cáo kiểm thử JMeter

## Mục tiêu
Kiểm thử hiệu năng website demo httpbin.org.

## Công cụ
Apache JMeter (mô phỏng).

## Kịch bản
- 50 users đồng thời
- 10 vòng lặp mỗi user
- Tổng cộng 500 request

## Kết quả
- Thời gian phản hồi TB: 200ms
- Tỷ lệ lỗi: 0%
- Throughput: 25 req/s

## Nhận xét
Website demo chịu tải tốt với 50 users đồng thời.
