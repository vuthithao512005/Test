# CHƯƠNG 2: PHÂN TÍCH HỆ THỐNG – E-LEARNING MINI

## 2.1 Tổng quan

Phân tích hệ thống nhằm xác định rõ các chức năng, yêu cầu và cách thức hoạt động của hệ thống trước khi thiết kế và triển khai.

Hệ thống E-Learning Mini tập trung vào:

* Xác định actor
* Xây dựng Use Case
* Đặc tả chức năng (SRS)
* Phân tích dữ liệu và luồng xử lý

---

## 2.2 Actor (Tác nhân)

### 2.2.1 Admin

* Quản lý khóa học
* Quản lý bài học
* Quản lý người dùng
* Xem thống kê

### 2.2.2 Người dùng (User)

* Đăng ký / đăng nhập
* Xem khóa học
* Học bài
* Làm bài kiểm tra
* Xem tiến độ

---

## 2.3 Danh sách Use Case

### Admin

| Mã   | Tên                |
| ---- | ------------------ |
| UC01 | Đăng nhập          |
| UC02 | Quản lý khóa học   |
| UC03 | Quản lý bài học    |
| UC04 | Quản lý người dùng |
| UC05 | Xem thống kê       |

### User

| Mã   | Tên              |
| ---- | ---------------- |
| UC06 | Đăng ký          |
| UC07 | Đăng nhập        |
| UC08 | Xem khóa học     |
| UC09 | Học bài          |
| UC10 | Làm bài kiểm tra |
| UC11 | Xem tiến độ      |

---

## 2.4 Đặc tả Use Case (SRS rút gọn)

### UC06 – Đăng ký

* Actor: User
* Input: name, email, password
* Output: thành công / lỗi

Luồng chính:

1. Nhập thông tin
2. Kiểm tra hợp lệ
3. Lưu DB
4. Thông báo

Luồng lỗi:

* Thiếu dữ liệu
* Email sai
* Email tồn tại

---

### UC07 – Đăng nhập

* Actor: User/Admin

Luồng chính:

1. Nhập email + password
2. Kiểm tra
3. Đăng nhập thành công

Luồng lỗi:

* Sai mật khẩu
* Không tồn tại

---

### UC02 – Quản lý khóa học

* Actor: Admin

Chức năng:

* Thêm
* Sửa
* Xóa

---

### UC09 – Học bài

* Actor: User

Luồng:

1. Chọn khóa học
2. Chọn bài
3. Xem nội dung

---

### UC10 – Làm bài kiểm tra

* Actor: User

Luồng:

1. Hiển thị câu hỏi
2. Chọn đáp án
3. Nộp bài
4. Chấm điểm

---

### UC11 – Xem tiến độ

* Actor: User
* Hiển thị % hoàn thành

---

## 2.5 Yêu cầu hệ thống

### 2.5.1 Chức năng

* Đăng ký / đăng nhập
* CRUD khóa học
* Học online
* Làm quiz
* Theo dõi tiến độ

### 2.5.2 Phi chức năng

* Giao diện dễ dùng
* Tốc độ nhanh
* Bảo mật
* Ổn định

---

## 2.6 Phân tích dữ liệu

Các bảng chính:

* Users
* Courses
* Lessons
* Quizzes
* Questions
* Progress

---

## 2.7 Luồng hệ thống

### User

Đăng nhập → Xem khóa học → Học → Làm quiz → Lưu tiến độ

### Admin

Đăng nhập → Quản lý → Thống kê

---

## 2.8 Điểm nổi bật hệ thống

### 1. Chu trình học tập hoàn chỉnh

Học → Kiểm tra → Tiến độ

### 2. Theo dõi tiến độ

Hiển thị % hoàn thành

### 3. Phân quyền rõ ràng

Admin / User

### 4. Dễ mở rộng

Có thể thêm thanh toán, video, AI

---

**Kết luận:**
Chương 2 đã xác định đầy đủ chức năng, dữ liệu và luồng xử lý của hệ thống, làm cơ sở cho thiết kế ở Chương 3.
