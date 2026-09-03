# Vehicle API Specification

## 1. Tổng quan

API quản lý thông tin phương tiện trong CAB System.

### Actor
- Driver
- Staff

### Mapping yêu cầu
- FR18 – Quản lý khách hàng, tài xế, phương tiện và chuyến
- UC09 – Quản lý vận hành
- AC10 – Staff quản lý dữ liệu vận hành
- TC18 – Kiểm tra quản lý dữ liệu vận hành

---

## 2. VEH-01 – Thêm phương tiện

### Endpoint

POST `/api/vehicles`

### Description

Staff thêm thông tin phương tiện vào hệ thống.

### Authentication

Bearer Token

### Request Body

{
  "vehicleType": "<vehicle_type>",
  "licensePlate": "<license_plate>",
  "driverId": "<driver_id>"
}

### Success Response – 201 Created

{
  "vehicleId": "<vehicle_id>",
  "vehicleType": "<vehicle_type>",
  "licensePlate": "<license_plate>",
  "driverId": "<driver_id>"
}

---

## 3. VEH-02 – Cập nhật phương tiện

### Endpoint

PUT `/api/vehicles/{vehicleId}`

### Description

Staff cập nhật thông tin phương tiện.

### Authentication

Bearer Token

### Request Body

{
  "vehicleType": "<vehicle_type>",
  "licensePlate": "<license_plate>",
  "driverId": "<driver_id>"
}

### Success Response – 200 OK

{
  "vehicleId": "<vehicle_id>",
  "vehicleType": "<vehicle_type>",
  "licensePlate": "<license_plate>",
  "driverId": "<driver_id>"
}

---

## 4. VEH-03 – Lấy thông tin phương tiện

### Endpoint

GET `/api/vehicles/{vehicleId}`

### Description

Lấy thông tin phương tiện.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "vehicleId": "<vehicle_id>",
  "vehicleType": "<vehicle_type>",
  "licensePlate": "<license_plate>",
  "driverId": "<driver_id>"
}

### Business Rules

- Chỉ Staff có quyền mới được quản lý phương tiện.
- Thông tin phương tiện phải hợp lệ.

### Test Case

- TC18: Kiểm tra quản lý phương tiện.
