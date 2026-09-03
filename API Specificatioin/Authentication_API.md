# Authentication API Specification

## 1. Overview

API dùng để xác thực người dùng Customer, Driver và Staff trước khi sử dụng các chức năng yêu cầu đăng nhập.

## 2. API Information

| Field | Value |
|---|---|
| API ID | AUTH-01 |
| API Name | Login |
| Method | POST |
| Endpoint | `/api/auth/login` |
| Actor | Customer, Driver, Staff |
| Authentication | Not Required |
| FR | FR01 |
| UC | UC01 |
| AC | AC01 |
| TC | TC01 |

## 3. Request

### Headers

Content-Type: application/json

### Body

{
  "phone": "0901234567",
  "password": "123456"
}

## 4. Response

### Success – 200 OK

{
  "token": "JWT_TOKEN",
  "userId": "USR001",
  "role": "CUSTOMER"
}

### Failed – 401 Unauthorized

{
  "code": "INVALID_CREDENTIALS",
  "message": "Phone or password is incorrect"
}

## 5. Business Rules

- BRL01: Người dùng phải xác thực trước khi sử dụng chức năng yêu cầu đăng nhập.
- Chỉ tài khoản hợp lệ mới được cấp token.
- Role được sử dụng để xác định quyền truy cập.

## 6. Exceptions

- EX01: Người dùng chưa đăng nhập hoặc token không hợp lệ.
- Tài khoản không tồn tại.
- Mật khẩu không chính xác.
- Tài khoản bị khóa.

## 7. Requirement Traceability

| FR | UC | AC | TC |
|---|---|---|---|
| FR01 | UC01 | AC01 | TC01 |
