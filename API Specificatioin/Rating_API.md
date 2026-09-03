# Rating API Specification

## 1. Overview

API dùng để Customer đánh giá Driver sau khi chuyến đi hoàn thành.

## 2. API Information

| Field | Value |
|---|---|
| API ID | RATE-01 |
| API Name | Create Rating |
| Method | POST |
| Endpoint | `/api/trips/{tripId}/rating` |
| Actor | Customer |
| Authentication | Required |
| FR | FR17 |
| UC | UC08 |
| AC | AC09 |
| TC | TC17 |

## 3. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "customerId": "CUS001",
  "driverId": "DRV001",
  "score": 5,
  "comment": "Driver phục vụ tốt"
}

## 4. Response

### Success – 201 Created

{
  "ratingId": "RATE001",
  "tripId": "TRIP001",
  "score": 5,
  "comment": "Driver phục vụ tốt"
}

## 5. Business Rules

- BRL12: Customer chỉ được đánh giá sau khi Trip hoàn thành.
- Customer chỉ được đánh giá Driver của Trip tương ứng.
- Mỗi Trip chỉ được đánh giá theo chính sách của hệ thống.

## 6. Exceptions

- Trip chưa hoàn thành.
- Customer không thuộc Trip.
- Driver không thuộc Trip.
- Rating không hợp lệ.
- Rating đã tồn tại.

## 7. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR17 | UC08 | AC09 | TC17 |
