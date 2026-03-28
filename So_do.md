
```


# CHƯƠNG 2: PHÂN TÍCH HỆ THỐNG – E-LEARNING MINI (CHI TIẾT – CHUẨN 10 ĐIỂM)

---

## 2.1 Tổng quan

Phân tích hệ thống nhằm xác định rõ các chức năng, luồng xử lý, dữ liệu và tương tác giữa các thành phần trong hệ thống E-Learning Mini.

Mục tiêu:

* Hiểu hệ thống cần làm gì
* Xác định các chức năng
* Xây dựng sơ đồ UML
* Làm nền tảng cho thiết kế (Chương 3)

---

## 2.2 Actor (Tác nhân)

### 2.2.1 Admin

* Quản lý khóa học
* Quản lý bài học
* Quản lý người dùng
* Xem thống kê

### 2.2.2 User (Học viên)

* Đăng ký tài khoản
* Đăng nhập
* Xem khóa học
* Học bài
* Làm bài kiểm tra
* Xem tiến độ

---

## 2.3 Use Case Diagram (Sơ đồ chức năng hệ thống)

```mermaid
graph LR

%% Actors
User((User))
Admin((Admin))

%% System Boundary
subgraph E-Learning System

UC1[Đăng ký]
UC2[Đăng nhập]
UC3[Xem danh sách khóa học]
UC4[Xem chi tiết khóa học]
UC5[Học bài]
UC6[Làm bài kiểm tra]
UC7[Xem tiến độ]

UC8[Quản lý khóa học]
UC9[Thêm khóa học]
UC10[Sửa khóa học]
UC11[Xóa khóa học]

UC12[Quản lý bài học]
UC13[Quản lý người dùng]
UC14[Xem thống kê]

end

%% User actions
User --> UC1
User --> UC2
User --> UC3
User --> UC4
User --> UC5
User --> UC6
User --> UC7

%% Admin actions
Admin --> UC2
Admin --> UC8
Admin --> UC12
Admin --> UC13
Admin --> UC14

%% Include relationships
UC8 --> UC9
UC8 --> UC10
UC8 --> UC11
```

---

## 2.4 Danh sách Use Case

| Mã   | Tên                | Actor      |
| ---- | ------------------ | ---------- |
| UC01 | Đăng ký            | User       |
| UC02 | Đăng nhập          | User/Admin |
| UC03 | Xem khóa học       | User       |
| UC04 | Học bài            | User       |
| UC05 | Làm bài kiểm tra   | User       |
| UC06 | Xem tiến độ        | User       |
| UC07 | Quản lý khóa học   | Admin      |
| UC08 | Quản lý bài học    | Admin      |
| UC09 | Quản lý người dùng | Admin      |
| UC10 | Xem thống kê       | Admin      |

---

## 2.5 Đặc tả Use Case (SRS chi tiết)

### UC01 – Đăng ký

* Actor: User
* Pre-condition: Chưa có tài khoản
* Post-condition: Tạo tài khoản thành công

Main flow:

1. Người dùng nhập thông tin
2. Hệ thống kiểm tra
3. Lưu database
4. Thông báo thành công

Alternate:

* Email đã tồn tại
* Thiếu dữ liệu

---

### UC02 – Đăng nhập

* Actor: User/Admin

Main flow:

1. Nhập email và mật khẩu
2. Kiểm tra dữ liệu
3. Đăng nhập

Alternate:

* Sai thông tin

---

### UC04 – Học bài

* Actor: User

Main flow:

1. Chọn khóa học
2. Chọn bài học
3. Xem nội dung

---

### UC05 – Làm bài kiểm tra

* Actor: User

Main flow:

1. Hiển thị câu hỏi
2. Chọn đáp án
3. Nộp bài
4. Chấm điểm

---

### UC06 – Xem tiến độ

* Actor: User

Main flow:

* Hiển thị % hoàn thành

---

### UC07 – Quản lý khóa học

* Actor: Admin

Main flow:

* Thêm / sửa / xóa khóa học

---

## 2.6 Data Flow Diagram (DFD)

### Level 0

```mermaid
flowchart TD
User --> System
Admin --> System
System --> Database
```

### Level 1

```mermaid
flowchart TD
User --> Login
Login --> DB
User --> Learning
Learning --> DB
Admin --> Manage
Manage --> DB
```

---

## 2.7 Sequence Diagram (Đăng nhập)

```mermaid
sequenceDiagram
User->>View: nhập thông tin
View->>Controller: request
Controller->>Model: xử lý
Model->>DB: truy vấn
DB-->>Model: dữ liệu
Model-->>Controller: kết quả
Controller-->>View: hiển thị
```

---

## 2.8 Activity Diagram (Luồng học tập)

```mermaid
flowchart TD
A[Đăng nhập] --> B[Xem khóa học]
B --> C[Học bài]
C --> D[Làm bài kiểm tra]
D --> E[Cập nhật tiến độ]
```

---

## 2.9 Business Logic

* Tiến độ = (số bài đã học / tổng số bài) * 100
* Điểm = số câu đúng / tổng câu

---

## 2.10 Điểm nổi bật hệ thống

* Chu trình học tập hoàn chỉnh
* Có kiểm tra và đánh giá
* Theo dõi tiến độ
* Phân quyền rõ ràng

---

## Kết luận

Chương 2 đã mô tả đầy đủ chức năng, dữ liệu, sơ đồ UML và luồng xử lý, đảm bảo yêu cầu của một hệ thống E-Learning hoàn chỉnh.




# CHƯƠNG 2: PHÂN TÍCH HỆ THỐNG – E-LEARNING MINI (CHI TIẾT – CHUẨN 10 ĐIỂM)

---

## 2.1 Tổng quan

Phân tích hệ thống nhằm xác định rõ các chức năng, luồng xử lý, dữ liệu và tương tác giữa các thành phần trong hệ thống E-Learning Mini.

Mục tiêu:

* Hiểu hệ thống cần làm gì
* Xác định các chức năng
* Xây dựng sơ đồ UML
* Làm nền tảng cho thiết kế (Chương 3)

---

## 2.2 Actor (Tác nhân)

### 2.2.1 Admin

* Quản lý khóa học
* Quản lý bài học
* Quản lý người dùng
* Xem thống kê

### 2.2.2 User (Học viên)

* Đăng ký tài khoản
* Đăng nhập
* Xem khóa học
* Học bài
* Làm bài kiểm tra
* Xem tiến độ

---

## 2.3 Use Case Diagram (Sơ đồ chức năng hệ thống)

```mermaid
graph LR

%% Actors
User((User))
Admin((Admin))

%% System Boundary
subgraph E-Learning System

UC1[Đăng ký]
UC2[Đăng nhập]
UC3[Xem danh sách khóa học]
UC4[Xem chi tiết khóa học]
UC5[Học bài]
UC6[Làm bài kiểm tra]
UC7[Xem tiến độ]

UC8[Quản lý khóa học]
UC9[Thêm khóa học]
UC10[Sửa khóa học]
UC11[Xóa khóa học]

UC12[Quản lý bài học]
UC13[Quản lý người dùng]
UC14[Xem thống kê]

end

%% User actions
User --> UC1
User --> UC2
User --> UC3
User --> UC4
User --> UC5
User --> UC6
User --> UC7

%% Admin actions
Admin --> UC2
Admin --> UC8
Admin --> UC12
Admin --> UC13
Admin --> UC14

%% Include relationships
UC8 --> UC9
UC8 --> UC10
UC8 --> UC11
```

---

## 2.4 Danh sách Use Case

| Mã   | Tên                | Actor      |
| ---- | ------------------ | ---------- |
| UC01 | Đăng ký            | User       |
| UC02 | Đăng nhập          | User/Admin |
| UC03 | Xem khóa học       | User       |
| UC04 | Học bài            | User       |
| UC05 | Làm bài kiểm tra   | User       |
| UC06 | Xem tiến độ        | User       |
| UC07 | Quản lý khóa học   | Admin      |
| UC08 | Quản lý bài học    | Admin      |
| UC09 | Quản lý người dùng | Admin      |
| UC10 | Xem thống kê       | Admin      |

---

## 2.5 Đặc tả Use Case (SRS chi tiết)

### UC01 – Đăng ký

* Actor: User
* Pre-condition: Chưa có tài khoản
* Post-condition: Tạo tài khoản thành công

Main flow:

1. Nhập thông tin
2. Kiểm tra hợp lệ
3. Lưu database
4. Thông báo thành công

Alternate:

* Email đã tồn tại
* Thiếu dữ liệu

---

### UC02 – Đăng nhập

* Actor: User/Admin
* Pre-condition: Có tài khoản
* Post-condition: Truy cập hệ thống

Main flow:

1. Nhập email + password
2. Kiểm tra
3. Đăng nhập

Alternate:

* Sai thông tin

---

### UC03 – Xem danh sách khóa học

* Actor: User

Main flow:

1. Truy cập trang khóa học
2. Hệ thống hiển thị danh sách

---

### UC04 – Học bài

* Actor: User

Main flow:

1. Chọn khóa học
2. Chọn bài học
3. Xem nội dung

---

### UC05 – Làm bài kiểm tra

* Actor: User

Main flow:

1. Hiển thị câu hỏi
2. Chọn đáp án
3. Nộp bài
4. Hệ thống chấm điểm

---

### UC06 – Xem tiến độ

* Actor: User

Main flow:

1. Truy cập trang tiến độ
2. Hiển thị % hoàn thành

---

### UC07 – Quản lý khóa học

* Actor: Admin

Main flow:

1. Xem danh sách khóa học
2. Thêm / sửa / xóa
3. Lưu database

---

### UC08 – Quản lý bài học

* Actor: Admin

Main flow:

1. Chọn khóa học
2. Thêm / sửa / xóa bài học
3. Lưu database

---

### UC09 – Quản lý người dùng

* Actor: Admin

Main flow:

1. Xem danh sách người dùng
2. Cập nhật quyền

---

### UC10 – Xem thống kê

* Actor: Admin

Main flow:

1. Truy cập dashboard
2. Hiển thị số lượng user, khóa học, tiến độ

---

## 2.6 Data Flow Diagram (DFD)

Data Flow Diagram (DFD)

### Level 0

```mermaid
flowchart TD
User --> System
Admin --> System
System --> Database
```

### Level 1

```mermaid
flowchart TD
User --> Login
Login --> DB
User --> Learning
Learning --> DB
Admin --> Manage
Manage --> DB
```

---

## 2.7 Sequence Diagram (Đăng nhập)

```mermaid
sequenceDiagram
User->>View: nhập thông tin
View->>Controller: request
Controller->>Model: xử lý
Model->>DB: truy vấn
DB-->>Model: dữ liệu
Model-->>Controller: kết quả
Controller-->>View: hiển thị
```

---

## 2.8 Activity Diagram (Luồng học tập)

```mermaid
flowchart TD
A[Đăng nhập] --> B[Xem khóa học]
B --> C[Học bài]
C --> D[Làm bài kiểm tra]
D --> E[Cập nhật tiến độ]
```

---

## 2.9 Business Logic

* Tiến độ = (số bài đã học / tổng số bài) * 100
* Điểm = số câu đúng / tổng câu

---

## 2.10 Điểm nổi bật hệ thống

* Chu trình học tập hoàn chỉnh
* Có kiểm tra và đánh giá
* Theo dõi tiến độ
* Phân quyền rõ ràng

---

## 2.11 Biểu đồ phân rã chức năng (FDD)

```mermaid
graph TD

A[Hệ thống E-Learning Mini]

A --> B[Quản lý người dùng]
A --> C[Quản lý học tập]
A --> D[Quản lý hệ thống]

%% User management
B --> B1[Đăng ký]
B --> B2[Đăng nhập]
B --> B3[Quản lý người dùng]

%% Learning
C --> C1[Xem khóa học]
C --> C2[Xem chi tiết khóa học]
C --> C3[Học bài]
C --> C4[Làm bài kiểm tra]
C --> C5[Xem tiến độ]

%% Admin
D --> D1[Quản lý khóa học]
D --> D2[Quản lý bài học]
D --> D3[Xem thống kê]
```

---

## Kết luận

Chương 2 đã mô tả đầy đủ chức năng, dữ liệu, sơ đồ UML và luồng xử lý, đảm bảo yêu cầu của một hệ thống E-Learning hoàn chỉnh.



---
# CHƯƠNG 2: PHÂN TÍCH HỆ THỐNG – E-LEARNING MINI (CHI TIẾT – CHUẨN 10 ĐIỂM)

---

## 2.1 Tổng quan

Phân tích hệ thống nhằm xác định rõ các chức năng, luồng xử lý, dữ liệu và tương tác giữa các thành phần trong hệ thống E-Learning Mini.

Mục tiêu:

* Hiểu hệ thống cần làm gì
* Xác định các chức năng
* Xây dựng sơ đồ UML
* Làm nền tảng cho thiết kế (Chương 3)

---

## 2.2 Actor (Tác nhân)

### 2.2.1 Admin

* Quản lý khóa học
* Quản lý bài học
* Quản lý người dùng
* Xem thống kê

### 2.2.2 User (Học viên)

* Đăng ký tài khoản
* Đăng nhập
* Xem khóa học
* Học bài
* Làm bài kiểm tra
* Xem tiến độ

---

## 2.3 Use Case Diagram tổng quát

```mermaid
graph LR
User((User))
Admin((Admin))

subgraph System
UC1[Đăng ký]
UC2[Đăng nhập]
UC3[Xem khóa học]
UC4[Học bài]
UC5[Làm bài kiểm tra]
UC6[Xem tiến độ]
UC7[Quản lý khóa học]
UC8[Quản lý bài học]
UC9[Quản lý người dùng]
UC10[Xem thống kê]
end

User --> UC1
User --> UC2
User --> UC3
User --> UC4
User --> UC5
User --> UC6

Admin --> UC2
Admin --> UC7
Admin --> UC8
Admin --> UC9
Admin --> UC10
```

---

## 2.3.1 Use Case – Đăng ký

```mermaid
graph LR
User((User)) --> UC1[Đăng ký tài khoản]
```

---

## 2.3.2 Use Case – Đăng nhập

```mermaid
graph LR
User((User)) --> UC2[Đăng nhập]
Admin((Admin)) --> UC2
```

---

## 2.3.3 Use Case – Học tập

```mermaid
graph LR
User((User)) --> UC3[Xem khóa học]
User --> UC4[Học bài]
User --> UC5[Làm bài kiểm tra]
User --> UC6[Xem tiến độ]
```

---

## 2.3.4 Use Case – Quản lý khóa học

```mermaid
graph LR
Admin((Admin)) --> UC7[Quản lý khóa học]
UC7 --> UC71[Thêm]
UC7 --> UC72[Sửa]
UC7 --> UC73[Xóa]
```

---

## 2.3.5 Use Case – Quản lý hệ thống

```mermaid
graph LR
Admin((Admin)) --> UC8[Quản lý bài học]
Admin --> UC9[Quản lý người dùng]
Admin --> UC10[Xem thống kê]
```

---

## 2.4 Danh sách Use Case

Danh sách Use Case

| Mã   | Tên                | Actor      |
| ---- | ------------------ | ---------- |
| UC01 | Đăng ký            | User       |
| UC02 | Đăng nhập          | User/Admin |
| UC03 | Xem khóa học       | User       |
| UC04 | Học bài            | User       |
| UC05 | Làm bài kiểm tra   | User       |
| UC06 | Xem tiến độ        | User       |
| UC07 | Quản lý khóa học   | Admin      |
| UC08 | Quản lý bài học    | Admin      |
| UC09 | Quản lý người dùng | Admin      |
| UC10 | Xem thống kê       | Admin      |

---

## 2.5 Đặc tả Use Case (SRS chi tiết)

### UC01 – Đăng ký

* Actor: User
* Pre-condition: Chưa có tài khoản
* Post-condition: Tạo tài khoản thành công

Main flow:

1. Nhập thông tin
2. Kiểm tra hợp lệ
3. Lưu database
4. Thông báo thành công

Alternate:

* Email đã tồn tại
* Thiếu dữ liệu

---

### UC02 – Đăng nhập

* Actor: User/Admin
* Pre-condition: Có tài khoản
* Post-condition: Truy cập hệ thống

Main flow:

1. Nhập email + password
2. Kiểm tra
3. Đăng nhập

Alternate:

* Sai thông tin

---

### UC03 – Xem danh sách khóa học

* Actor: User

Main flow:

1. Truy cập trang khóa học
2. Hệ thống hiển thị danh sách

---

### UC04 – Học bài

* Actor: User

Main flow:

1. Chọn khóa học
2. Chọn bài học
3. Xem nội dung

---

### UC05 – Làm bài kiểm tra

* Actor: User

Main flow:

1. Hiển thị câu hỏi
2. Chọn đáp án
3. Nộp bài
4. Hệ thống chấm điểm

---

### UC06 – Xem tiến độ

* Actor: User

Main flow:

1. Truy cập trang tiến độ
2. Hiển thị % hoàn thành

---

### UC07 – Quản lý khóa học

* Actor: Admin

Main flow:

1. Xem danh sách khóa học
2. Thêm / sửa / xóa
3. Lưu database

---

### UC08 – Quản lý bài học

* Actor: Admin

Main flow:

1. Chọn khóa học
2. Thêm / sửa / xóa bài học
3. Lưu database

---

### UC09 – Quản lý người dùng

* Actor: Admin

Main flow:

1. Xem danh sách người dùng
2. Cập nhật quyền

---

### UC10 – Xem thống kê

* Actor: Admin

Main flow:

1. Truy cập dashboard
2. Hiển thị số lượng user, khóa học, tiến độ

---

## 2.6 Data Flow Diagram (DFD)

Data Flow Diagram (DFD)

### Level 0

```mermaid
flowchart TD
User --> System
Admin --> System
System --> Database
```

### Level 1

```mermaid
flowchart TD
User --> Login
Login --> DB
User --> Learning
Learning --> DB
Admin --> Manage
Manage --> DB
```

---

## 2.7 Sequence Diagram (Đăng nhập)

```mermaid
sequenceDiagram
User->>View: nhập thông tin
View->>Controller: request
Controller->>Model: xử lý
Model->>DB: truy vấn
DB-->>Model: dữ liệu
Model-->>Controller: kết quả
Controller-->>View: hiển thị
```

---

## 2.8 Activity Diagram (Luồng học tập)

```mermaid
flowchart TD
A[Đăng nhập] --> B[Xem khóa học]
B --> C[Học bài]
C --> D[Làm bài kiểm tra]
D --> E[Cập nhật tiến độ]
```

---

## 2.9 Business Logic

* Tiến độ = (số bài đã học / tổng số bài) * 100
* Điểm = số câu đúng / tổng câu

---

## 2.10 Điểm nổi bật hệ thống

* Chu trình học tập hoàn chỉnh
* Có kiểm tra và đánh giá
* Theo dõi tiến độ
* Phân quyền rõ ràng

---

## 2.11 Biểu đồ phân rã chức năng (FDD)

```mermaid
graph TD

A[Hệ thống E-Learning Mini]

A --> B[Quản lý người dùng]
A --> C[Quản lý học tập]
A --> D[Quản lý hệ thống]

%% User management
B --> B1[Đăng ký]
B --> B2[Đăng nhập]
B --> B3[Quản lý người dùng]

%% Learning
C --> C1[Xem khóa học]
C --> C2[Xem chi tiết khóa học]
C --> C3[Học bài]
C --> C4[Làm bài kiểm tra]
C --> C5[Xem tiến độ]

%% Admin
D --> D1[Quản lý khóa học]
D --> D2[Quản lý bài học]
D --> D3[Xem thống kê]
```

---

## Kết luận

Chương 2 đã mô tả đầy đủ chức năng, dữ liệu, sơ đồ UML và luồng xử lý, đảm bảo yêu cầu của một hệ thống E-Learning hoàn chỉnh.
