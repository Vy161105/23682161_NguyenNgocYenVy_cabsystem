
# Booking API Specification

## 1. Overview

API dùng để Customer tạo và tra cứu yêu cầu đặt xe.

## 2. API Information – BOOK-01

| Field | Value |
|---|---|
| API ID | BOOK-01 |
| API Name | Create Booking |
| Method | POST |
| Endpoint | `/api/bookings` |
| Actor | Customer |
| Authentication | Required |
| FR | FR03, FR04 |
| UC | UC02 |
| AC | AC02 |
| TC | TC03 |

## 3. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "customerId": "CUS001",
  "pickupLocation": "Ben Thanh Market",
  "destination": "Tan Son Nhat Airport",
  "vehicleType": "CAR"
}

## 4. Response

### Success – 201 Created

{
  "bookingId": "BOOK001",
  "customerId": "CUS001",
  "bookingStatus": "PENDING",
  "createdAt": "2026-09-03T10:00:00"
}

### Failed – 400 Bad Request

{
  "code": "INVALID_BOOKING",
  "message": "Pickup, destination and vehicle type are required"
}

## 5. API Information – BOOK-02

| Field | Value |
|---|---|
| API ID | BOOK-02 |
| API Name | Get Booking |
| Method | GET |
| Endpoint | `/api/bookings/{bookingId}` |
| Actor | Customer, Staff |
| Authentication | Required |
| FR | FR04 |
| UC | UC02 |
| AC | AC02 |
| TC | TC04 |

## 6. Request

### Headers

Authorization: Bearer <token>

## 7. Business Rules

- BRL02: Booking phải có Pickup Location, Destination và Vehicle Type.
- Customer phải đăng nhập trước khi tạo Booking.
- Customer không cần tạo lại Booking khi Driver từ chối hoặc không phản hồi.

## 8. Exceptions

- Thông tin Booking không đầy đủ.
- Customer không tồn tại.
- Booking không tồn tại.
- Người dùng không có quyền truy cập.

## 9. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR03, FR04 | UC02 | AC02 | TC03 |
| FR04 | UC02 | AC02 | TC04 |
