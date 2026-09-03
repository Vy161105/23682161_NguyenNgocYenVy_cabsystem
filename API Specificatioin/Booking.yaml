# Booking API Specification

## 1. Tổng quan

API quản lý đặt xe và tìm kiếm/phân công tài xế.

Các chức năng tìm và phân công tài xế được gộp vào Booking API vì quá trình phân công được thực hiện trực tiếp trên một booking.

### Actor
- Customer
- Driver
- Staff

### Mapping yêu cầu
- FR03 – Nhập điểm đón, điểm đến và loại xe
- FR04 – Ghi nhận booking
- FR05 – Tự động tìm tài xế
- FR06 – Lọc/ưu tiên tài xế phù hợp
- FR07 – Gửi yêu cầu và ghi nhận phản hồi
- FR08 – Xử lý tài xế từ chối/không phản hồi
- FR09 – Tìm tài xế khác/thông báo không có tài xế
- UC02 – Đặt xe
- UC03 – Tìm và phân công tài xế
- AC02–AC05
- TC03–TC09

---

## 2. BOOK-01 – Tạo booking

### Endpoint

POST `/api/bookings`

### Description

Khách hàng tạo yêu cầu đặt xe.

### Authentication

Bearer Token

### Request Body

{
  "pickupLocation": {
    "latitude": "<latitude>",
    "longitude": "<longitude>"
  },
  "dropoffLocation": {
    "latitude": "<latitude>",
    "longitude": "<longitude>"
  },
  "vehicleType": "<vehicle_type>"
}

### Success Response – 201 Created

{
  "bookingId": "<booking_id>",
  "status": "PENDING"
}

### Error Response – 400 Bad Request

{
  "code": "INVALID_BOOKING",
  "message": "Pickup, dropoff and vehicle type are required"
}

### Business Rules

- BRL02: Booking phải có điểm đón, điểm đến và loại xe.
- Không cho phép tạo booking nếu dữ liệu bắt buộc không đầy đủ.

---

## 3. BOOK-02 – Lấy thông tin booking

### Endpoint

GET `/api/bookings/{bookingId}`

### Description

Lấy thông tin và trạng thái của booking.

### Authentication

Bearer Token

### Success Response – 200 OK

{
  "bookingId": "<booking_id>",
  "customerId": "<customer_id>",
  "driverId": "<driver_id>",
  "pickupLocation": {
    "latitude": "<latitude>",
    "longitude": "<longitude>"
  },
  "dropoffLocation": {
    "latitude": "<latitude>",
    "longitude": "<longitude>"
  },
  "vehicleType": "<vehicle_type>",
  "status": "<PENDING|ASSIGNED|IN_PROGRESS|COMPLETED>"
}

---

## 4. BOOK-03 – Tìm tài xế

### Endpoint

POST `/api/bookings/{bookingId}/driver-search`

### Description

Hệ thống tự động tìm tài xế phù hợp cho booking.

### Authentication

Internal API

### Success Response – 200 OK

{
  "bookingId": "<booking_id>",
  "status": "DRIVER_SEARCHING",
  "driverId": "<driver_id>"
}

### Business Rules

- BRL03: Chỉ tìm các tài xế đang AVAILABLE.
- BRL04: Ưu tiên tài xế phù hợp và gần điểm đón.
- Khi tìm được tài xế, hệ thống gửi yêu cầu nhận chuyến.

---

## 5. BOOK-04 – Gửi yêu cầu nhận chuyến

### Endpoint

POST `/api/driver-requests`

### Description

Gửi yêu cầu chuyến đến tài xế được lựa chọn.

### Request Body

{
  "bookingId": "<booking_id>",
  "driverId": "<driver_id>"
}

### Success Response – 201 Created

{
  "requestId": "<request_id>",
  "bookingId": "<booking_id>",
  "driverId": "<driver_id>",
  "status": "PENDING"
}

---

## 6. BOOK-05 – Tài xế chấp nhận chuyến

### Endpoint

POST `/api/driver-requests/{requestId}/accept`

### Description

Tài xế chấp nhận yêu cầu nhận chuyến.

### Success Response – 200 OK

{
  "requestId": "<request_id>",
  "status": "ACCEPTED",
  "bookingStatus": "ASSIGNED"
}

### Business Rules

- Khi tài xế chấp nhận, booking được chuyển sang trạng thái ASSIGNED.

---

## 7. BOOK-06 – Tài xế từ chối chuyến

### Endpoint

POST `/api/driver-requests/{requestId}/reject`

### Description

Ghi nhận việc tài xế từ chối yêu cầu.

### Success Response – 200 OK

{
  "requestId": "<request_id>",
  "status": "REJECTED"
}

### Business Rules

- BRL05: Khi tài xế từ chối, hệ thống phải tìm tài xế khác.
- BRL06: Khách hàng không cần tạo lại booking.

---

## 8. BOOK-07 – Xử lý tài xế không phản hồi

### Endpoint

POST `/api/driver-requests/{requestId}/timeout`

### Description

Ghi nhận trường hợp tài xế không phản hồi trong thời gian quy định.

### Success Response – 200 OK

{
  "requestId": "<request_id>",
  "status": "TIMEOUT"
}

### Business Rules

- EX05: Driver timeout.
- Khi timeout, hệ thống tiếp tục tìm tài xế khác.

---

## 9. BOOK-08 – Tìm tài xế tiếp theo

### Endpoint

POST `/api/bookings/{bookingId}/driver-search/next`

### Description

Tiếp tục tìm tài xế khác khi tài xế trước đó từ chối hoặc không phản hồi.

### Success Response – 200 OK

{
  "bookingId": "<booking_id>",
  "status": "DRIVER_SEARCHING",
  "driverId": "<driver_id>"
}

### No Driver Response

{
  "bookingId": "<booking_id>",
  "status": "NO_DRIVER_AVAILABLE"
}

### Business Rules

- BRL05: Tài xế từ chối/timeout → tìm tài xế khác.
- BRL07: Nếu không còn tài xế phù hợp, thông báo cho khách hàng.
- EX03: Không có tài xế khả dụng.
- EX06: Không có tài xế phù hợp.

### Test Case

- TC03–TC04: Tạo và kiểm tra booking.
- TC05: Tìm tài xế.
- TC06: Lọc/ưu tiên tài xế.
- TC07: Tài xế chấp nhận.
- TC08: Tài xế từ chối.
- TC09: Tài xế timeout/không có tài xế.
