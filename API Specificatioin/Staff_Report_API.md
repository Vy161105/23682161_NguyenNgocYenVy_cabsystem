# Staff and Report API Specification

## 1. Tổng quan

API phục vụ nhân viên vận hành trong việc:
- Quản lý Customer.
- Quản lý Driver.
- Quản lý Vehicle.
- Quản lý Trip.
- Theo dõi các chuyến đang diễn ra.
- Xem báo cáo vận hành cơ bản.

### Actor
- Staff

### Mapping yêu cầu
- FR18 – Quản lý khách hàng, tài xế, phương tiện, chuyến
- FR19 – Giám sát chuyến đang diễn ra
- FR20 – Báo cáo
- UC09 – Quản lý vận hành
- UC10 – Báo cáo
- AC10 – Staff quản lý và giám sát
- TC18–TC20

---

# PART A – STAFF MANAGEMENT API

## 2. STAFF-01 – Quản lý khách hàng

### Endpoint

GET `/api/staff/customers`

### Description

Staff xem danh sách khách hàng để phục vụ quản lý vận hành.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "data": [
    {
      "customerId": "<customer_id>",
      "fullName": "<full_name>",
      "phone": "<phone>",
      "email": "<email>"
    }
  ]
}

### Business Rules

- Chỉ Staff có quyền mới được truy cập.
- BRL13: Chỉ người dùng được phân quyền mới được quản lý/xem dữ liệu vận hành.

---

## 3. STAFF-02 – Quản lý tài xế

### Endpoint

GET `/api/staff/drivers`

### Description

Staff xem danh sách và thông tin tài xế.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "data": [
    {
      "driverId": "<driver_id>",
      "fullName": "<full_name>",
      "status": "<status>",
      "vehicleId": "<vehicle_id>"
    }
  ]
}

---

## 4. STAFF-03 – Quản lý phương tiện

### Endpoint

GET `/api/staff/vehicles`

### Description

Staff xem danh sách phương tiện.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "data": [
    {
      "vehicleId": "<vehicle_id>",
      "vehicleType": "<vehicle_type>",
      "licensePlate": "<license_plate>",
      "driverId": "<driver_id>"
    }
  ]
}

---

## 5. STAFF-04 – Quản lý chuyến

### Endpoint

GET `/api/staff/trips`

### Description

Staff xem danh sách chuyến để quản lý vận hành.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "data": [
    {
      "tripId": "<trip_id>",
      "bookingId": "<booking_id>",
      "driverId": "<driver_id>",
      "status": "<status>"
    }
  ]
}

---

## 6. STAFF-05 – Theo dõi chuyến đang diễn ra

### Endpoint

GET `/api/staff/trips/ongoing`

### Description

Staff xem các chuyến đang thực hiện để theo dõi tình trạng vận hành.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "data": [
    {
      "tripId": "<trip_id>",
      "driverId": "<driver_id>",
      "status": "<status>",
      "location": {
        "latitude": "<latitude>",
        "longitude": "<longitude>"
      }
    }
  ]
}

### Business Rules

- Staff được phân quyền mới được truy cập.
- Dữ liệu phải phục vụ việc giám sát các chuyến đang diễn ra.

---

# PART B – REPORT API

## 7. REPORT-01 – Báo cáo vận hành

### Endpoint

GET `/api/reports/operations?from={from}&to={to}`

### Description

Staff xem báo cáo vận hành trong một khoảng thời gian.

### Authentication

Bearer Token

### Query Parameters

- from: Thời điểm bắt đầu.
- to: Thời điểm kết thúc.

### Success Response – 200 OK

{
  "from": "<from>",
  "to": "<to>",
  "totalTrips": "<total_trips>",
  "totalRevenue": "<total_revenue>",
  "completionRate": "<completion_rate>",
  "cancellationRate": "<cancellation_rate>",
  "driverEfficiency": "<driver_efficiency>"
}

### Report Metrics

- Tổng số chuyến.
- Tổng doanh thu.
- Tỷ lệ hoàn thành.
- Tỷ lệ hủy.
- Hiệu quả tài xế.

### Business Rules

- BRL13: Chỉ người dùng được phân quyền mới được xem báo cáo.
- Báo cáo phải được giới hạn theo khoảng thời gian được yêu cầu.

### Exceptions

- EX09: Staff không có quyền truy cập.
- Khoảng thời gian báo cáo không hợp lệ.

### Mapping

- FR20 – Báo cáo
- UC10 – Báo cáo
- AC10 – Quản lý và báo cáo vận hành
- TC20 – Kiểm tra báo cáo.
