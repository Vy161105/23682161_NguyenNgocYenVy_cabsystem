
# Customer API Specification

## 1. Overview

API dùng để quản lý và cập nhật thông tin Customer.

## 2. API Information

| Field | Value |
|---|---|
| API ID | CUS-01 |
| API Name | Get Customer |
| Method | GET |
| Endpoint | `/api/customers/{customerId}` |
| Actor | Customer, Staff |
| Authentication | Required |
| FR | FR02 |
| UC | UC01 |
| AC | AC01 |
| TC | TC02 |

## 3. Request

### Headers

Authorization: Bearer <token>

## 4. Response

### Success – 200 OK

{
  "customerId": "CUS001",
  "fullName": "Nguyen Van A",
  "phone": "0901234567",
  "email": "customer@example.com"
}

### Failed – 404 Not Found

{
  "code": "CUSTOMER_NOT_FOUND",
  "message": "Customer does not exist"
}

## 5. API Information – CUS-02

| Field | Value |
|---|---|
| API ID | CUS-02 |
| API Name | Update Customer |
| Method | PUT |
| Endpoint | `/api/customers/{customerId}` |
| Actor | Customer, Staff |
| Authentication | Required |
| FR | FR02 |
| UC | UC01 |
| AC | AC01 |
| TC | TC02 |

## 6. Request

### Headers

Authorization: Bearer <token>
Content-Type: application/json

### Body

{
  "fullName": "Nguyen Van A",
  "phone": "0901234567",
  "email": "customer@example.com"
}

## 7. Response

### Success – 200 OK

{
  "customerId": "CUS001",
  "fullName": "Nguyen Van A",
  "phone": "0901234567",
  "email": "customer@example.com"
}

### Failed – 400 Bad Request

{
  "code": "INVALID_DATA",
  "message": "Customer information is invalid"
}

## 8. Business Rules

- BRL01: Người dùng phải xác thực trước khi sử dụng chức năng yêu cầu đăng nhập.
- Customer chỉ được cập nhật thông tin tài khoản của chính mình.
- Staff chỉ được cập nhật thông tin Customer khi có quyền phù hợp.

## 9. Exceptions

- Customer không tồn tại.
- Người dùng không có quyền truy cập.
- Dữ liệu cập nhật không hợp lệ.

## 10. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR02 | UC01 | AC01 | TC02 |
