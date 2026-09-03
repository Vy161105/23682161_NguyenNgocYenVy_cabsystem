# Rating and Notification API Specification

## 1. Tổng quan

API xử lý:
- Đánh giá chuyến đi.
- Gửi các thông báo cơ bản trong quá trình đặt và thực hiện chuyến.

Hai chức năng được đặt chung file vì đều là các chức năng hỗ trợ sau/đi kèm quá trình booking, trip và payment.

---

# PART A – RATING API

## 2. RATE-01 – Đánh giá chuyến đi

### Endpoint

POST `/api/trips/{tripId}/rating`

### Description

Khách hàng đánh giá chuyến đi sau khi chuyến đã hoàn thành.

### Actor

Customer

### Authentication

Bearer Token

### Request Body

{
  "score": "<score>",
  "comment": "<comment>"
}

### Success Response – 201 Created

{
  "ratingId": "<rating_id>",
  "tripId": "<trip_id>",
  "score": "<score>",
  "comment": "<comment>"
}

### Business Rules

- BRL12: Chỉ được đánh giá sau khi chuyến hoàn thành.
- Mỗi chuyến chỉ được đánh giá theo chính sách của hệ thống.

### Error Response – 400 Bad Request

{
  "code": "TRIP_NOT_COMPLETED",
  "message": "Rating is only allowed after trip completion"
}

### Mapping

- FR17 – Đánh giá
- UC08 – Lịch sử/đánh giá
- AC09 – Đánh giá sau chuyến
- TC17 – Kiểm tra đánh giá

---

# PART B – NOTIFICATION API

## 3. NOTI-01 – Gửi thông báo

### Endpoint

POST `/api/notifications`

### Description

Hệ thống tạo và gửi các thông báo cơ bản cho người dùng.

### Actor

Internal System

### Authentication

Internal API

### Request Body

{
  "recipientId": "<recipient_id>",
  "type": "<BOOKING_CREATED|DRIVER_ASSIGNED|DRIVER_ARRIVING|TRIP_STARTED|TRIP_COMPLETED|PAYMENT_SUCCESS|PAYMENT_FAILED|NO_DRIVER_AVAILABLE>",
  "message": "<message>"
}

### Success Response – 201 Created

{
  "notificationId": "<notification_id>",
  "status": "SENT"
}

### Notification Types

- BOOKING_CREATED
- DRIVER_ASSIGNED
- DRIVER_ARRIVING
- TRIP_STARTED
- TRIP_COMPLETED
- PAYMENT_SUCCESS
- PAYMENT_FAILED
- NO_DRIVER_AVAILABLE

### Business Rules

- FR21: Hệ thống phải hỗ trợ các thông báo cơ bản.
- Thông báo phải được tạo tương ứng với sự kiện nghiệp vụ.
- Lỗi gửi thông báo không được làm dừng quá trình booking hoặc trip.

### Exceptions

- Notification Provider không phản hồi.
- Gửi thông báo thất bại.

### Mapping

- FR21 – Notifications
- AC11 – Thông báo
- TC21 – Kiểm tra thông báo
