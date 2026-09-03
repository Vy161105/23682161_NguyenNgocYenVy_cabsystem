# Driver API Specification

## 1. Tổng quan

API quản lý thông tin, trạng thái và vị trí của tài xế.

### Actor
- Customer
- Driver
- Staff

### Mapping yêu cầu
- FR05 – Tìm tài xế
- FR06 – Lọc/ưu tiên tài xế phù hợp
- FR10 – Cập nhật trạng thái chuyến
- FR12 – Theo dõi tài xế/chuyến
- FR18 – Quản lý tài xế
- FR19 – Giám sát chuyến đang diễn ra
- UC03 – Tìm và phân công tài xế
- UC04 – Theo dõi chuyến
- UC05 – Thực hiện chuyến
- UC09 – Quản lý vận hành

---

## 2. DRV-01 – Lấy thông tin tài xế

### Endpoint

GET `/api/drivers/{driverId}`

### Description

Lấy thông tin tài xế phục vụ việc theo dõi chuyến hoặc quản lý tài xế.

### Authentication

Bearer Token

### Request Headers

Authorization: Bearer <access_token>

### Success Response – 200 OK

{
  "driverId": "<driver_id>",
  "fullName": "<full_name>",
  "phone": "<phone>",
  "status": "<AVAILABLE|BUSY|OFFLINE>",
  "vehicleId": "<vehicle_id>"
}

### Error Response – 404 Not Found

{
  "code": "DRIVER_NOT_FOUND",
  "message": "Driver not found"
}

---

## 3. DRV-02 – Cập nhật trạng thái tài xế

### Endpoint

PATCH `/api/drivers/{driverId}/status`

### Description

Cho phép tài xế cập nhật trạng thái hoạt động.

### Authentication

Bearer Token

### Request Body

{
  "status": "<AVAILABLE|BUSY|OFFLINE>"
}

### Success Response – 200 OK

{
  "driverId": "<driver_id>",
  "status": "<status>"
}

### Business Rules

- Chỉ tài xế hợp lệ mới được cập nhật trạng thái của chính mình.
- Driver ở trạng thái AVAILABLE mới được xem xét cho việc phân công chuyến.

---

## 4. DRV-03 – Cập nhật vị trí tài xế

### Endpoint

PATCH `/api/drivers/{driverId}/location`

### Description

Cập nhật vị trí hiện tại của tài xế để phục vụ tìm kiếm, phân công và theo dõi chuyến.

### Authentication

Bearer Token

### Request Body

{
  "latitude": "<latitude>",
  "longitude": "<longitude>"
}

### Success Response – 200 OK

{
  "driverId": "<driver_id>",
  "latitude": "<latitude>",
  "longitude": "<longitude>"
}

### Business Rules

- Vị trí tài xế được sử dụng để xác định tài xế phù hợp với điểm đón.
- Chỉ tài xế hợp lệ mới được cập nhật vị trí.

### Test Case

- TC05: Kiểm tra tìm tài xế dựa trên trạng thái và vị trí.
- TC12: Kiểm tra theo dõi tài xế/chuyến.
- TC18: Kiểm tra quản lý tài xế.
