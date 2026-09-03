
# Driver API Specification

## 1. Overview

API dùng để quản lý thông tin, trạng thái và vị trí của Driver.

## 2. API Information – DRV-01

| Field | Value |
|---|---|
| API ID | DRV-01 |
| API Name | Get Driver |
| Method | GET |
| Endpoint | `/api/drivers/{driverId}` |
| Actor | Customer, Driver, Staff |
| Authentication | Required |
| FR | FR02, FR12 |
| UC | UC01, UC04 |
| AC | AC06 |
| TC | TC12 |

## 3. Request

### Headers

Authorization: Bearer <token>

## 4. Response

### Success – 200 OK

{
  "driverId": "DRV001",
  "fullName": "Tran Van B",
  "phone": "0901234568",
  "status": "AVAILABLE",
  "currentLocation": {
    "latitude": 10.7769,
    "longitude": 106.7009
  }
}

### Failed – 404 Not Found

{
  "code": "DRIVER_NOT_FOUND",
  "message": "Driver does not exist"
}

## 5. API Information – DRV-02

| Field | Value |
|---|---|
| API ID | DRV-02 |
| API Name | Update Driver Status |
| Method | PATCH |
| Endpoint | `/api/drivers/{driverId}/status` |
| Actor | Driver |
| Authentication | Required |
| FR | FR18, FR19 |
| UC | UC05, UC09 |
| AC | AC10 |
| TC | TC18, TC19 |

## 6. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "status": "AVAILABLE"
}

## 7. API Information – DRV-03

| Field | Value |
|---|---|
| API ID | DRV-03 |
| API Name | Update Driver Location |
| Method | PATCH |
| Endpoint | `/api/drivers/{driverId}/location` |
| Actor | Driver |
| Authentication | Required |
| FR | FR05, FR06, FR12 |
| UC | UC03, UC04 |
| AC | AC03, AC06 |
| TC | TC05, TC12 |

## 8. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "latitude": 10.7769,
  "longitude": 106.7009
}

## 9. Business Rules

- BRL03: Chỉ tìm kiếm Driver đang ở trạng thái AVAILABLE.
- BRL04: Ưu tiên Driver phù hợp và gần điểm đón.
- Driver phải đăng nhập để cập nhật trạng thái và vị trí.

## 10. Exceptions

- Driver không tồn tại.
- Driver không có quyền cập nhật dữ liệu.
- Vị trí không hợp lệ.
- Trạng thái Driver không hợp lệ.

## 11. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR02, FR12 | UC01, UC04 | AC06 | TC12 |
| FR18, FR19 | UC05, UC09 | AC10 | TC18, TC19 |
| FR05, FR06, FR12 | UC03, UC04 | AC03, AC06 | TC05, TC12 |
