# Trip API Specification

## 1. Overview

API dùng để theo dõi và thực hiện chuyến đi.

## 2. API Information – TRIP-01

| Field | Value |
|---|---|
| API ID | TRIP-01 |
| API Name | Get Trip |
| Method | GET |
| Endpoint | `/api/trips/{tripId}` |
| Actor | Customer, Driver, Staff |
| Authentication | Required |
| FR | FR10, FR11, FR12 |
| UC | UC04, UC05 |
| AC | AC06, AC07 |
| TC | TC10, TC12 |

## 3. Request

### Headers

Authorization: Bearer <token>

## 4. API Information – TRIP-02

| Field | Value |
|---|---|
| API ID | TRIP-02 |
| API Name | Update Trip Status |
| Method | PATCH |
| Endpoint | `/api/trips/{tripId}/status` |
| Actor | Driver |
| Authentication | Required |
| FR | FR10 |
| UC | UC05 |
| AC | AC07 |
| TC | TC10 |

## 5. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "status": "DRIVER_ARRIVING"
}

Các trạng thái: DRIVER_ARRIVING, PICKED_UP, IN_PROGRESS.

## 6. API Information – TRIP-03

| Field | Value |
|---|---|
| API ID | TRIP-03 |
| API Name | Complete Trip |
| Method | POST |
| Endpoint | `/api/trips/{tripId}/complete` |
| Actor | Driver |
| Authentication | Required |
| FR | FR11 |
| UC | UC05 |
| AC | AC07 |
| TC | TC11 |

## 7. Request

### Headers

Authorization: Bearer <token>

## 8. API Information – TRIP-04

| Field | Value |
|---|---|
| API ID | TRIP-04 |
| API Name | Track Trip |
| Method | GET |
| Endpoint | `/api/trips/{tripId}/tracking` |
| Actor | Customer |
| Authentication | Required |
| FR | FR12 |
| UC | UC04 |
| AC | AC06 |
| TC | TC12 |

## 9. Request

### Headers

Authorization: Bearer <token>

## 10. Business Rules

- BRL08: Chỉ Driver được phân công mới được thực hiện và cập nhật Trip.
- BRL09: Trip phải hoàn thành trước khi tính cước và thanh toán.
- Customer được theo dõi trạng thái Trip sau khi Driver được phân công.

## 11. Exceptions

- Trip không tồn tại.
- Driver không được phân công cho Trip.
- Trạng thái Trip không hợp lệ.
- Trip chưa đủ điều kiện hoàn thành.

## 12. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR10, FR11, FR12 | UC04, UC05 | AC06, AC07 | TC10, TC11, TC12 |
