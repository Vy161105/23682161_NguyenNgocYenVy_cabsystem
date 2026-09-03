# Staff API Specification

## 1. Overview

API dùng cho Staff quản lý Customer, Driver, Vehicle và Trip; đồng thời theo dõi các chuyến đang diễn ra.

## 2. API Information – STAFF-01

| Field | Value |
|---|---|
| API ID | STAFF-01 |
| API Name | Manage Customers |
| Method | GET / PUT |
| Endpoint | `/api/staff/customers` / `/api/staff/customers/{customerId}` |
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

## 4. API Information – STAFF-02

| Field | Value |
|---|---|
| API ID | STAFF-02 |
| API Name | Manage Drivers |
| Method | GET / PUT |
| Endpoint | `/api/staff/drivers` / `/api/staff/drivers/{driverId}` |
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

## 6. API Information – STAFF-03

| Field | Value |
|---|---|
| API ID | STAFF-03 |
| API Name | Manage Vehicles |
| Method | GET / PUT |
| Endpoint | `/api/staff/vehicles` / `/api/staff/vehicles/{vehicleId}` |
| Actor | Staff |
| Authentication | Required |
| FR | FR18 |
| UC | UC09 |
| AC | AC10 |
| TC | TC18 |

## 7. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

## 8. API Information – STAFF-04

| Field | Value |
|---|---|
| API ID | STAFF-04 |
| API Name | Manage Trips |
| Method | GET |
| Endpoint | `/api/staff/trips` / `/api/staff/trips/{tripId}` |
| Actor | Staff |
| Authentication | Required |
| FR | FR18 |
| UC | UC09 |
| AC | AC10 |
| TC | TC18 |

## 9. Request

### Headers

Authorization: Bearer <token>

## 10. API Information – STAFF-05

| Field | Value |
|---|---|
| API ID | STAFF-05 |
| API Name | Get Ongoing Trips |
| Method | GET |
| Endpoint | `/api/staff/trips/ongoing` |
| Actor | Staff |
| Authentication | Required |
| FR | FR19 |
| UC | UC09 |
| AC | AC10 |
| TC | TC19 |

## 11. Request

### Headers

Authorization: Bearer <token>

## 12. Business Rules

- BRL13: Chỉ Staff được phân quyền mới được quản lý và xem dữ liệu vận hành.
- Staff chỉ được thực hiện chức năng phù hợp với Role.
- Các hoạt động quản trị quan trọng phải được ghi nhận để truy vết.

## 13. Exceptions

- EX09: Staff không có quyền truy cập.
- EX10: Có sự cố trong quá trình quản lý hoặc xử lý Trip.
- Dữ liệu không tồn tại.
- Token không hợp lệ.

## 14. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR18 | UC09 | AC10 | TC18 |
| FR19 | UC09 | AC10 | TC19 |
