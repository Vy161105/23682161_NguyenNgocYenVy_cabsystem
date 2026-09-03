# Notification API Specification

## 1. Overview

API dùng để gửi các thông báo cơ bản liên quan đến Booking, Driver, Trip và Payment.

## 2. API Information

| Field | Value |
|---|---|
| API ID | NOTI-01 |
| API Name | Send Notification |
| Method | POST |
| Endpoint | `/api/notifications` |
| Actor | System |
| Authentication | Required |
| FR | FR21 |
| UC | UC03, UC04, UC05, UC07 |
| AC | AC11 |
| TC | TC21 |

## 3. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "userId": "CUS001",
  "type": "DRIVER_ASSIGNED",
  "message": "Driver đã được phân công cho chuyến đi của bạn."
}

## 4. Notification Types

- BOOKING_CREATED
- DRIVER_ASSIGNED
- DRIVER_ARRIVING
- TRIP_STARTED
- TRIP_COMPLETED
- PAYMENT_SUCCESS
- PAYMENT_FAILED
- NO_DRIVER_AVAILABLE

## 5. Business Rules

- BRL07: Customer phải được thông báo khi không tìm được Driver phù hợp.
- Các sự kiện quan trọng của Booking, Driver, Trip và Payment phải có thông báo cơ bản.
- Lỗi Notification không được làm dừng quá trình Booking hoặc Trip.

## 6. Exceptions

- User không tồn tại.
- Loại Notification không hợp lệ.
- Notification Provider không phản hồi.
- Gửi Notification thất bại.

## 7. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR21 | UC03, UC04, UC05, UC07 | AC11 | TC21 |
