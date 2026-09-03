# Payment API Specification

## 1. Overview

API dùng để xử lý thanh toán chuyến đi bằng tiền mặt hoặc phương thức điện tử thông qua Payment Provider.

## 2. API Information – PAY-01

| Field | Value |
|---|---|
| API ID | PAY-01 |
| API Name | Create Payment |
| Method | POST |
| Endpoint | `/api/payments` |
| Actor | Customer |
| Authentication | Required |
| FR | FR14 |
| UC | UC07 |
| AC | AC08 |
| TC | TC14 |

## 3. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "tripId": "TRIP001",
  "paymentMethod": "CASH"
}

Payment Method: CASH hoặc ELECTRONIC.

## 4. Response

### Success – 200 OK

{
  "paymentId": "PAY001",
  "tripId": "TRIP001",
  "amount": 150000,
  "paymentStatus": "PENDING"
}

## 5. API Information – PAY-02

| Field | Value |
|---|---|
| API ID | PAY-02 |
| API Name | Payment Result |
| Method | POST |
| Endpoint | `/api/payments/{paymentId}/result` |
| Actor | Payment Provider |
| Authentication | Required |
| FR | FR15 |
| UC | UC07 |
| AC | AC08 |
| TC | TC15 |

## 6. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "paymentStatus": "SUCCESS"
}

## 7. Business Rules

- BRL10: Customer được thanh toán bằng CASH hoặc ELECTRONIC.
- BRL11: Thanh toán ELECTRONIC được thực hiện thông qua Payment Provider.
- CAB System không lưu thông tin thẻ hoặc thông tin tài khoản thanh toán nhạy cảm.
- Lỗi thanh toán không được làm dừng Booking hoặc Trip.

## 8. Exceptions

- EX07: Thanh toán điện tử thất bại.
- EX08: Payment Provider timeout hoặc không phản hồi.
- Payment không tồn tại.
- Phương thức thanh toán không được hỗ trợ.

## 9. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR14 | UC07 | AC08 | TC14 |
| FR15 | UC07 | AC08 | TC15 |
