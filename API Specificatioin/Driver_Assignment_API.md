# Driver Assignment API Specification

## 1. Overview

API dùng để tìm kiếm và phân công Driver cho Booking.

## 2. API Information – ASSIGN-01

| Field | Value |
|---|---|
| API ID | ASSIGN-01 |
| API Name | Search Driver |
| Method | POST |
| Endpoint | `/api/bookings/{bookingId}/driver-search` |
| Actor | System |
| Authentication | Required |
| FR | FR05, FR06 |
| UC | UC03 |
| AC | AC03 |
| TC | TC05 |

## 3. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

## 4. API Information – ASSIGN-02

| Field | Value |
|---|---|
| API ID | ASSIGN-02 |
| API Name | Create Driver Request |
| Method | POST |
| Endpoint | `/api/driver-requests` |
| Actor | System |
| Authentication | Required |
| FR | FR07 |
| UC | UC03 |
| AC | AC03 |
| TC | TC06 |

## 5. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "bookingId": "BOOK001",
  "driverId": "DRV001"
}

## 6. API Information – ASSIGN-03

| Field | Value |
|---|---|
| API ID | ASSIGN-03 |
| API Name | Accept Driver Request |
| Method | POST |
| Endpoint | `/api/driver-requests/{requestId}/accept` |
| Actor | Driver |
| Authentication | Required |
| FR | FR07 |
| UC | UC03 |
| AC | AC03 |
| TC | TC07 |

## 7. Request

### Headers

Authorization: Bearer <token>

## 8. API Information – ASSIGN-04

| Field | Value |
|---|---|
| API ID | ASSIGN-04 |
| API Name | Reject Driver Request |
| Method | POST |
| Endpoint | `/api/driver-requests/{requestId}/reject` |
| Actor | Driver |
| Authentication | Required |
| FR | FR08 |
| UC | UC03 |
| AC | AC04 |
| TC | TC08 |

## 9. Request

### Headers

Authorization: Bearer <token>

## 10. API Information – ASSIGN-05

| Field | Value |
|---|---|
| API ID | ASSIGN-05 |
| API Name | Driver Request Timeout |
| Method | POST |
| Endpoint | `/api/driver-requests/{requestId}/timeout` |
| Actor | System |
| Authentication | Required |
| FR | FR08 |
| UC | UC03 |
| AC | AC04 |
| TC | TC09 |

## 11. Request

### Headers

Authorization: Bearer <token>

## 12. API Information – ASSIGN-06

| Field | Value |
|---|---|
| API ID | ASSIGN-06 |
| API Name | Search Next Driver |
| Method | POST |
| Endpoint | `/api/bookings/{bookingId}/driver-search/next` |
| Actor | System |
| Authentication | Required |
| FR | FR09 |
| UC | UC03 |
| AC | AC05 |
| TC | TC09 |

## 13. Request

### Headers

Authorization: Bearer <token>

## 14. Business Rules

- BRL03: Chỉ tìm kiếm Driver đang AVAILABLE.
- BRL04: Ưu tiên Driver phù hợp và gần điểm đón.
- BRL05: Driver từ chối hoặc không phản hồi thì tìm Driver khác.
- BRL06: Customer không cần tạo lại Booking.
- BRL07: Không có Driver phù hợp thì thông báo Customer.

## 15. Exceptions

- EX03: Không có Driver khả dụng.
- EX04: Driver từ chối yêu cầu.
- EX05: Driver không phản hồi trong thời gian quy định.
- EX06: Không tìm được Driver phù hợp.

## 16. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR05, FR06 | UC03 | AC03 | TC05 |
| FR07 | UC03 | AC03 | TC06, TC07 |
| FR08 | UC03 | AC04 | TC08, TC09 |
| FR09 | UC03 | AC05 | TC09 |
