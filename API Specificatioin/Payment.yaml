# Payment API Specification

## 1. Tổng quan

API xử lý thanh toán cho chuyến đi.

Hệ thống hỗ trợ:
- Thanh toán tiền mặt.
- Thanh toán điện tử thông qua một Payment Provider.

CAB System không lưu trữ thông tin nhạy cảm của thẻ hoặc tài khoản thanh toán.

### Actor
- Customer
- Payment Provider

### Mapping yêu cầu
- FR14 – Thanh toán
- FR15 – Ghi nhận kết quả và xử lý lỗi thanh toán
- UC07 – Thanh toán
- AC08 – Kết quả thanh toán được ghi nhận
- TC14–TC15

---

## 2. PAY-01 – Tạo yêu cầu thanh toán

### Endpoint

POST `/api/payments`

### Description

Tạo yêu cầu thanh toán cho một chuyến đã hoàn thành.

### Authentication

Bearer Token

### Request Body

{
  "tripId": "<trip_id>",
  "method": "<CASH|ELECTRONIC>"
}

### Success Response – 201 Created

{
  "paymentId": "<payment_id>",
  "tripId": "<trip_id>",
  "method": "<CASH|ELECTRONIC>",
  "status": "PENDING"
}

### Business Rules

- BRL09: Chuyến phải hoàn thành trước khi thanh toán.
- BRL10: Chỉ sử dụng phương thức thanh toán được hệ thống hỗ trợ.
- Nếu chọn ELECTRONIC, yêu cầu được chuyển đến Payment Provider.
- CAB System không lưu thông tin nhạy cảm của thẻ/tài khoản.

---

## 3. PAY-02 – Ghi nhận kết quả thanh toán

### Endpoint

POST `/api/payments/{paymentId}/result`

### Description

Payment Provider gửi kết quả xử lý thanh toán về CAB System.

### Authentication

Provider authentication / secure integration

### Request Body

{
  "status": "<SUCCESS|FAILED>",
  "providerTransactionId": "<provider_transaction_id>"
}

### Success Response – 200 OK

{
  "paymentId": "<payment_id>",
  "status": "<SUCCESS|FAILED>"
}

### Business Rules

- BRL11: Thanh toán điện tử được thực hiện thông qua Payment Provider.
- Kết quả giao dịch phải được ghi nhận.
- EX07: Thanh toán điện tử thất bại.
- EX08: Payment Provider timeout/failure.
- Lỗi thanh toán không được làm dừng toàn bộ chức năng đặt xe.

### Test Case

- TC14: Thanh toán tiền mặt/điện tử.
- TC15: Thanh toán thất bại hoặc Payment Provider không phản hồi.
