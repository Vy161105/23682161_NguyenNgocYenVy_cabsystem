# Customer API Specification

## 1. Tổng quan

API quản lý thông tin khách hàng trong CAB System.

### Actor
- Customer
- Staff

### Mapping yêu cầu
- FR02 – Cập nhật thông tin tài khoản
- UC01 – Quản lý tài khoản
- AC01 – Quản lý tài khoản thành công
- TC02 – Kiểm tra cập nhật thông tin khách hàng

---

## 2. CUS-01 – Lấy thông tin khách hàng

### Endpoint

GET `/api/customers/{customerId}`

### Description

Lấy thông tin của một khách hàng.

### Authentication

Bearer Token

### Request Headers

Authorization: Bearer <access_token>

### Path Parameter

- customerId: ID của khách hàng cần lấy thông tin.

### Success Response – 200 OK

{
  "customerId": "<customer_id>",
  "fullName": "<full_name>",
  "phone": "<phone>",
  "email": "<email>"
}

### Error Response – 404 Not Found

{
  "code": "CUSTOMER_NOT_FOUND",
  "message": "Customer not found"
}

---

## 3. CUS-02 – Cập nhật thông tin khách hàng

### Endpoint

PUT `/api/customers/{customerId}`

### Description

Cho phép khách hàng cập nhật thông tin tài khoản.

### Authentication

Bearer Token

### Request Headers

Authorization: Bearer <access_token>
Content-Type: application/json

### Request Body

{
  "fullName": "<full_name>",
  "phone": "<phone>",
  "email": "<email>"
}

### Success Response – 200 OK

{
  "customerId": "<customer_id>",
  "fullName": "<full_name>",
  "phone": "<phone>",
  "email": "<email>"
}

### Error Response – 400 Bad Request

{
  "code": "INVALID_CUSTOMER_DATA",
  "message": "Invalid customer information"
}

### Business Rules

- Chỉ khách hàng hợp lệ hoặc Staff có quyền mới được truy cập thông tin.
- Thông tin cập nhật phải hợp lệ.

### Test Case

- TC02: Kiểm tra xem và cập nhật thông tin khách hàng.
