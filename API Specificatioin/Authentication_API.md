# Authentication API Specification

## 1. Tổng quan

API phục vụ xác thực người dùng trong CAB System.

### Actor
- Customer
- Driver
- Staff

### Authentication
- Không yêu cầu authentication khi đăng nhập.

### Mapping yêu cầu
- FR01 – Đăng nhập/xác thực người dùng
- UC01 – Quản lý tài khoản
- AC01 – Người dùng đăng nhập thành công
- TC01 – Kiểm tra xác thực

---

## 2. AUTH-01 – Đăng nhập

### Endpoint

POST `/api/auth/login`

### Description

Cho phép Customer, Driver hoặc Staff đăng nhập vào hệ thống bằng thông tin tài khoản.

### Request Headers

Content-Type: application/json

### Request Body

{
  "phone": "<phone>",
  "password": "<password>"
}

### Success Response – 200 OK

{
  "token": "<access_token>",
  "userId": "<user_id>",
  "role": "<CUSTOMER|DRIVER|STAFF>"
}

### Error Response – 401 Unauthorized

{
  "code": "INVALID_CREDENTIALS",
  "message": "Invalid phone or password"
}

### Business Rules

- BRL01: Người dùng phải xác thực trước khi sử dụng các chức năng được bảo vệ.
- Thông tin đăng nhập không hợp lệ phải bị từ chối.

### Exceptions

- EX01: Người dùng chưa đăng nhập hoặc thông tin xác thực không hợp lệ.

### Test Case

- TC01: Kiểm tra đăng nhập với thông tin hợp lệ và không hợp lệ.
