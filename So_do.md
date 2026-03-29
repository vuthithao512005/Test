
---
# CHƯƠNG 2: PHÂN TÍCH HỆ THỐNG (BẢN HOÀN CHỈNH – 10 ĐIỂM)

---

## 2.1 Xác định Actor và Use Case

### Actor:

* User (Học viên)
* Admin (Quản trị viên)

---

### Danh sách Use Case

| Mã   | Tên                   | Actor       |
| ---- | --------------------- | ----------- |
| UC01 | Đăng ký               | User        |
| UC02 | Đăng nhập             | User, Admin |
| UC03 | Xem khóa học          | User        |
| UC04 | Xem chi tiết khóa học | User        |
| UC05 | Học bài               | User        |
| UC06 | Làm bài kiểm tra      | User        |
| UC07 | Xem tiến độ           | User        |
| UC08 | Quản lý khóa học      | Admin       |
| UC09 | Quản lý bài học       | Admin       |
| UC10 | Quản lý người dùng    | Admin       |
| UC11 | Xem thống kê          | Admin       |

---

## 2.2 Đặc tả Use Case (Chuẩn IEEE)

### UC02 – Đăng nhập

* Actor: User/Admin
* Mô tả: Người dùng đăng nhập hệ thống
* Pre-condition: Đã có tài khoản
* Post-condition: Truy cập hệ thống

Main flow:

1. Nhập email, password
2. Hệ thống kiểm tra
3. Thành công → chuyển trang

Alternate:

* Sai thông tin → báo lỗi

---

### UC06 – Làm bài kiểm tra

* Actor: User
* Pre-condition: Đã học bài
* Post-condition: Lưu điểm

Main flow:

1. Hiển thị câu hỏi
2. Chọn đáp án
3. Nộp bài
4. Hệ thống chấm điểm

Alternate:

* Không chọn đáp án

---

## 2.3 Use Case Diagram (Chi tiết theo chức năng)

### 2.3.1 Use Case Tổng quát

```mermaid
graph LR
User((User))
Admin((Admin))

subgraph System
UC1[Đăng ký]
UC2[Đăng nhập]
UC3[Xem khóa học]
UC4[Xem chi tiết khóa học]
UC5[Học bài]
UC6[Làm bài kiểm tra]
UC7[Xem tiến độ]
UC8[Quản lý khóa học]
UC9[Quản lý bài học]
UC10[Quản lý người dùng]
UC11[Xem thống kê]
end

User --> UC1
User --> UC2
User --> UC3
User --> UC4
User --> UC5
User --> UC6
User --> UC7

Admin --> UC2
Admin --> UC8
Admin --> UC9
Admin --> UC10
Admin --> UC11
```

---

### 2.3.2 Use Case – Xác thực

```mermaid
graph LR
User((User)) --> UC1[Đăng ký]
User --> UC2[Đăng nhập]
UC2 --> UC21[Xác thực tài khoản]
```

---

### 2.3.3 Use Case – Học tập

```mermaid
graph LR
User((User)) --> UC3[Xem khóa học]
User --> UC4[Xem chi tiết]
User --> UC5[Học bài]
User --> UC6[Làm bài kiểm tra]
User --> UC7[Xem tiến độ]

UC5 --> UC51[Cập nhật tiến độ]
UC6 --> UC61[Chấm điểm]
```

---

### 2.3.4 Use Case – Quản lý khóa học

```mermaid
graph LR
Admin((Admin)) --> UC8[Quản lý khóa học]
UC8 --> UC81[Thêm]
UC8 --> UC82[Sửa]
UC8 --> UC83[Xóa]
```

---

### 2.3.5 Use Case – Quản lý bài học

```mermaid
graph LR
Admin((Admin)) --> UC9[Quản lý bài học]
UC9 --> UC91[Thêm]
UC9 --> UC92[Sửa]
UC9 --> UC93[Xóa]
```

---

### 2.3.6 Use Case – Quản lý người dùng

```mermaid
graph LR
Admin((Admin)) --> UC10[Quản lý người dùng]
UC10 --> UC101[Xem danh sách]
UC10 --> UC102[Phân quyền]
```

---

### 2.3.7 Use Case – Thống kê

```mermaid
graph LR
Admin((Admin)) --> UC11[Xem thống kê]
UC11 --> UC111[Thống kê user]
UC11 --> UC112[Thống kê khóa học]
UC11 --> UC113[Thống kê tiến độ]
```

---

## 2.4 Biểu đồ phân rã chức năng (FDD)

Biểu đồ phân rã chức năng (FDD)

```mermaid
graph TD
A[Hệ thống E-Learning]

A --> B[Quản lý người dùng]
A --> C[Học tập]
A --> D[Quản trị]

B --> B1[Đăng ký]
B --> B2[Đăng nhập]

C --> C1[Xem khóa học]
C --> C2[Học bài]
C --> C3[Làm quiz]
C --> C4[Xem tiến độ]

D --> D1[QL khóa học]
D --> D2[QL bài học]
D --> D3[QL user]
D --> D4[Thống kê]
```

---

## 2.5 DFD Level 0

```mermaid
graph LR
User --> System
Admin --> System
System --> DB[(Database)]
```

---

## 2.6 DFD Level 1 (Chi tiết)

```mermaid
graph TD
User --> A[Đăng nhập]
User --> B[Học bài]
User --> C[Làm bài]

A --> DB
B --> DB
C --> DB

Admin --> D[Quản lý]
D --> DB
```

---

## 2.7 Sequence Diagram (Login)

```mermaid
sequenceDiagram
User->>View: nhập
View->>Controller: gửi
Controller->>Model: check
Model->>DB: query
DB-->>Model: data
Model-->>Controller: OK
Controller-->>View: hiển thị
```

---

## 2.8 Sequence Diagram (Quiz)

```mermaid
sequenceDiagram
User->>View: làm bài
View->>Controller: submit
Controller->>Model: chấm điểm
Model->>DB: lưu
DB-->>Model: ok
Model-->>Controller: điểm
Controller-->>View: hiển thị
```

---

## 2.9 Activity Diagram

```mermaid
flowchart TD
A[Bắt đầu] --> B[Chọn khóa học]
B --> C[Học bài]
C --> D{Làm quiz?}
D -->|Có| E[Làm bài]
D -->|Không| F[Kết thúc]
E --> F
```

---

## 2.10 Phân tích dữ liệu

### Bảng Users

* id
* email
* password

### Bảng Courses

* id
* title

### Bảng Lessons

* id
* course_id

### Bảng Quiz

* id
* question

---

## 2.11 Business Logic

* Học bài → cập nhật tiến độ
* Làm quiz → chấm điểm tự động
* Admin quản lý dữ liệu

---

## 2.12 Điểm nổi bật

* Progress Tracking
* Auto Scoring
* MVC

---

## Kết luận chương

Chương 2 đã phân tích đầy đủ hệ thống thông qua UML, DFD và logic nghiệp vụ, làm nền cho thiết kế hệ thống.

# CHƯƠNG 2: USE CASE CHI TIẾT HỆ THỐNG E-LEARNING MINI

---

## UC01 – Đăng ký

```mermaid
graph LR
User((User)) --> UC01[Đăng ký]
UC01 -->|<<include>>| UC011[Nhập thông tin]
UC01 -->|<<include>>| UC012[Lưu tài khoản]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Đăng ký |
| Actor | User |
| Mục tiêu | Tạo tài khoản |
| Tiền điều kiện | Chưa có tài khoản |
| Luồng chính | Nhập thông tin → Lưu tài khoản |
| Ngoại lệ | Email tồn tại |

---

## UC02 – Đăng nhập

```mermaid
graph LR
User((User)) --> UC02[Đăng nhập]
Admin((Admin)) --> UC02
UC02 -->|<<include>>| UC021[Xác thực]
UC02 -->|<<extend>>| UC022[Quên mật khẩu]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Đăng nhập |
| Actor | User, Admin |
| Mục tiêu | Truy cập hệ thống |
| Tiền điều kiện | Có tài khoản |
| Luồng chính | Nhập → Xác thực → Thành công |
| Ngoại lệ | Sai thông tin |

---

## UC03 – Xem khóa học

```mermaid
graph LR
User((User)) --> UC03[Xem khóa học]
UC03 -->|<<include>>| UC031[Lấy dữ liệu]
UC03 -->|<<include>>| UC032[Hiển thị]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Xem khóa học |
| Actor | User |
| Mục tiêu | Xem danh sách |
| Tiền điều kiện | Đăng nhập |
| Luồng chính | Truy cập → Hiển thị |
| Ngoại lệ | Không có dữ liệu |

---

## UC04 – Xem chi tiết khóa học

```mermaid
graph LR
User((User)) --> UC04[Xem chi tiết]
UC04 -->|<<include>>| UC041[Hiển thị nội dung]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Xem chi tiết khóa học |
| Actor | User |
| Mục tiêu | Xem chi tiết |
| Tiền điều kiện | Chọn khóa học |
| Luồng chính | Hiển thị nội dung |
| Ngoại lệ | Không có dữ liệu |

---

## UC05 – Học bài

```mermaid
graph LR
User((User)) --> UC05[Học bài]
UC05 --> UC051[Xem nội dung]
UC05 -->|<<include>>| UC052[Cập nhật tiến độ]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Học bài |
| Actor | User |
| Mục tiêu | Học nội dung |
| Tiền điều kiện | Chọn khóa học |
| Luồng chính | Xem bài → Cập nhật tiến độ |
| Ngoại lệ | Lỗi nội dung |

---

## UC06 – Làm bài kiểm tra

```mermaid
graph LR
User((User)) --> UC06[Làm bài kiểm tra]
UC06 --> UC061[Chọn đáp án]
UC06 --> UC062[Nộp bài]
UC06 --> UC063[Chấm điểm]
UC06 --> UC064[Làm lại bài]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Làm bài kiểm tra |
| Actor | User |
| Mục tiêu | Đánh giá |
| Tiền điều kiện | Đã học |
| Luồng chính | Làm → Nộp → Chấm |
| Ngoại lệ | Chưa chọn đáp án |

---

## UC07 – Xem tiến độ

```mermaid
graph LR
User((User)) --> UC07[Xem tiến độ]
UC07 --> UC071[Lấy dữ liệu]
UC07 --> UC072[Hiển thị %]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Xem tiến độ |
| Actor | User |
| Mục tiêu | Theo dõi |
| Tiền điều kiện | Đã học |
| Luồng chính | Hiển thị tiến độ |
| Ngoại lệ | Không có dữ liệu |

---

## UC08 – Quản lý khóa học

```mermaid
graph LR
Admin((Admin)) --> UC08[QL khóa học]
UC08 --> UC081[Thêm]
UC08 --> UC082[Sửa]
UC08 --> UC083[Xóa]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Quản lý khóa học |
| Actor | Admin |
| Mục tiêu | Quản lý dữ liệu |
| Tiền điều kiện | Đăng nhập |
| Luồng chính | Thêm/Sửa/Xóa |
| Ngoại lệ | Lỗi dữ liệu |

---

## UC09 – Quản lý bài học

```mermaid
graph LR
Admin((Admin)) --> UC09[QL bài học]
UC09 --> UC091[Thêm]
UC09 --> UC092[Sửa]
UC09 --> UC093[Xóa]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Quản lý bài học |
| Actor | Admin |
| Mục tiêu | Quản lý nội dung |
| Tiền điều kiện | Đăng nhập |
| Luồng chính | Thêm/Sửa/Xóa |
| Ngoại lệ | Lỗi |

---

## UC10 – Quản lý người dùng

```mermaid
graph LR
Admin((Admin)) --> UC10[QL người dùng]
UC10 --> UC101[Xem danh sách]
UC10 --> UC102[Phân quyền]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Quản lý người dùng |
| Actor | Admin |
| Mục tiêu | Quản lý tài khoản |
| Tiền điều kiện | Đăng nhập |
| Luồng chính | Xem → Phân quyền |
| Ngoại lệ | Lỗi hệ thống |

---

## UC11 – Xem thống kê

```mermaid
graph LR
Admin((Admin)) --> UC11[Thống kê]
UC11 --> UC111[User]
UC11 --> UC112[Khóa học]
UC11 --> UC113[Tiến độ]
```

| Thành phần | Nội dung |
|----------|---------|
| Use Case | Xem thống kê |
| Actor | Admin |
| Mục tiêu | Theo dõi hệ thống |
| Tiền điều kiện | Đăng nhập |
| Luồng chính | Hiển thị dữ liệu |
| Ngoại lệ | Không có dữ liệu |

---

# KẾT LUẬN

Mỗi Use Case đã được mô tả bằng sơ đồ riêng và bảng chi tiết, đảm bảo thể hiện đầy đủ chức năng hệ thống và mối quan hệ <<include>> và <<extend>>.
