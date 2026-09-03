# Fare API Specification

## 1. Overview

API dùng để xác định số tiền phải thanh toán cho chuyến đi.

## 2. API Information

| Field | Value |
|---|---|
| API ID | FARE-01 |
| API Name | Calculate Fare |
| Method | POST |
| Endpoint | `/api/trips/{tripId}/fare` |
| Actor | System |
| Authentication | Required |
| FR | FR13 |
| UC | UC06 |
| AC | AC08 |
| TC | TC13 |

## 3. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

## 4. Response

### Success – 200 OK

{
  "tripId": "TRIP001",
  "fare": 150000,
  "currency": "VND"
}

## 5. Business Rules

- BRL09: Trip phải hoàn thành trước khi tính cước.
- Công thức tính cước phải được xác định theo chính sách kinh doanh của CAB.

## 6. Exceptions

- Trip chưa hoàn thành.
- Trip không tồn tại.
- Không đủ dữ liệu để tính cước.

## 7. Note

Công thức tính cước cụ thể chưa được chốt trong yêu cầu hiện tại. Không tự quy định giá mở cửa, giá/km, giá/phút, phụ phí hoặc Dynamic Surge Pricing.

## 8. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR13 | UC06 | AC08 | TC13 |
