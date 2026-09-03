# Trip API Specification

## 1. Tổng quan

API quản lý quá trình thực hiện chuyến đi, theo dõi chuyến và tính cước.

Fare API được gộp vào Trip API vì tiền cước được xác định dựa trên thông tin chuyến đi.

### Actor
- Customer
- Driver
- Staff

### Mapping yêu cầu
- FR10 – Cập nhật trạng thái chuyến
- FR11 – Hoàn thành chuyến
- FR12 – Theo dõi chuyến
- FR13 – Tính cước
- UC04 – Theo dõi chuyến
- UC05 – Thực hiện chuyến
- UC06 – Tính cước
- AC06–AC08
- TC10–TC13

---

## 2. TRIP-01 – Lấy thông tin chuyến

### Endpoint

GET `/api/trips/{tripId}`

### Description

Lấy thông tin và trạng thái hiện tại của chuyến.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "tripId": "<trip_id>",
  "bookingId": "<booking_id>",
  "driverId": "<driver_id>",
  "status": "<ASSIGNED|DRIVER_ARRIVING|IN_PROGRESS|COMPLETED>",
  "fare": "<fare>"
}

---

## 3. TRIP-02 – Cập nhật trạng thái chuyến

### Endpoint

PATCH `/api/trips/{tripId}/status`

### Description

Tài xế cập nhật trạng thái thực hiện chuyến.

### Authentication

Bearer Token

### Request Body

{
  "status": "<DRIVER_ARRIVING|IN_PROGRESS>"
}

### Success Response – 200 OK

{
  "tripId": "<trip_id>",
  "status": "<status>"
}

### Business Rules

- BRL08: Chỉ tài xế được phân công mới được thực hiện và cập nhật chuyến.
- Trạng thái chuyến phải tuân theo trình tự nghiệp vụ.

---

## 4. TRIP-03 – Hoàn thành chuyến

### Endpoint

POST `/api/trips/{tripId}/complete`

### Description

Tài xế xác nhận chuyến đã hoàn thành.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "tripId": "<trip_id>",
  "status": "COMPLETED"
}

### Business Rules

- BRL09: Chuyến phải hoàn thành trước khi xác định thanh toán cuối cùng.
- Sau khi hoàn thành, hệ thống có thể thực hiện tính cước và thanh toán.

---

## 5. TRIP-04 – Theo dõi chuyến

### Endpoint

GET `/api/trips/{tripId}/tracking`

### Description

Cho phép khách hàng theo dõi tài xế và trạng thái chuyến.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "tripId": "<trip_id>",
  "status": "<status>",
  "driverId": "<driver_id>",
  "driverLocation": {
    "latitude": "<latitude>",
    "longitude": "<longitude>"
  },
  "eta": "<estimated_time>"
}

### Business Rules

- Khách hàng chỉ được theo dõi chuyến của mình.
- Thông tin vị trí được lấy từ dữ liệu vị trí tài xế.

---

## 6. TRIP-05 – Tính cước chuyến

### Endpoint

POST `/api/trips/{tripId}/fare`

### Description

Hệ thống xác định số tiền cần thanh toán cho chuyến đi.

### Authentication

Internal API

### Success Response – 200 OK

{
  "tripId": "<trip_id>",
  "fare": "<calculated_fare>",
  "currency": "VND"
}

### Business Rules

- FR13: Hệ thống phải xác định tiền cước.
- Công thức tính cước cụ thể chưa được chốt trong phạm vi yêu cầu hiện tại.
- Không tự ý cố định mức giá mở cửa, giá/km, giá/phút hoặc phụ phí.

### Test Case

- TC10: Cập nhật trạng thái chuyến.
- TC11: Hoàn thành chuyến.
- TC12: Theo dõi chuyến.
- TC13: Tính cước.
