
# Vehicle API Specification

## 1. Overview

API dùng để quản lý thông tin phương tiện của Driver.

## 2. API Information – VEH-01

| Field | Value |
|---|---|
| API ID | VEH-01 |
| API Name | Create Vehicle |
| Method | POST |
| Endpoint | `/api/vehicles` |
| Actor | Staff |
| Authentication | Required |
| FR | FR18 |
| UC | UC09 |
| AC | AC10 |
| TC | TC18 |

## 3. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "driverId": "DRV001",
  "vehicleType": "CAR",
  "licensePlate": "51A-12345"
}

## 4. API Information – VEH-02

| Field | Value |
|---|---|
| API ID | VEH-02 |
| API Name | Update Vehicle |
| Method | PUT |
| Endpoint | `/api/vehicles/{vehicleId}` |
| Actor | Staff |
| Authentication | Required |
| FR | FR18 |
| UC | UC09 |
| AC | AC10 |
| TC | TC18 |

## 5. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "driverId": "DRV001",
  "vehicleType": "CAR",
  "licensePlate": "51A-12345",
  "status": "ACTIVE"
}

## 6. API Information – VEH-03

| Field | Value |
|---|---|
| API ID | VEH-03 |
| API Name | Get Vehicle |
| Method | GET |
| Endpoint | `/api/vehicles/{vehicleId}` |
| Actor | Staff, Driver |
| Authentication | Required |
| FR | FR18 |
| UC | UC09 |
| AC | AC10 |
| TC | TC18 |

## 7. Request

### Headers

Authorization: Bearer <token>

## 8. Business Rules

- BRL13: Chỉ người dùng được phân quyền mới được quản lý dữ liệu Vehicle.
- Vehicle phải được gắn với Driver hợp lệ.
- License plate không được trùng.

## 9. Exceptions

- Vehicle không tồn tại.
- Driver không tồn tại.
- Người dùng không có quyền.
- Thông tin Vehicle không hợp lệ.

## 10. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR18 | UC09 | AC10 | TC18 |
