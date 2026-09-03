# Report API Specification

## 1. Overview

API dùng để Staff xem các báo cáo vận hành cơ bản của CAB System.

## 2. API Information

| Field | Value |
|---|---|
| API ID | REPORT-01 |
| API Name | Get Operation Report |
| Method | GET |
| Endpoint | `/api/reports/operations?from={from}&to={to}` |
| Actor | Staff |
| Authentication | Required |
| FR | FR20 |
| UC | UC10 |
| AC | AC10 |
| TC | TC20 |

## 3. Request

### Headers

Authorization: Bearer <token>

## 4. Response

### Success – 200 OK

{
  "from": "2026-09-01",
  "to": "2026-09-03",
  "totalTrips": 120,
  "totalRevenue": 18000000,
  "completionRate": 95.0,
  "cancellationRate": 5.0,
  "driverEfficiency": 90.0
}

## 5. Business Rules

- BRL13: Chỉ Staff được phân quyền mới được xem báo cáo.
- Báo cáo được truy vấn theo khoảng thời gian.
- Báo cáo phải hỗ trợ các chỉ số vận hành cơ bản.

## 6. Exceptions

- Staff không có quyền truy cập.
- Khoảng thời gian không hợp lệ.
- Không có dữ liệu trong khoảng thời gian được yêu cầu.

## 7. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR20 | UC10 | AC10 | TC20 |
