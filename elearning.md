## 2.5. Đặc tả chi tiết cơ sở dữ liệu

Dưới đây là chi tiết cấu trúc, kiểu dữ liệu và các ràng buộc của 11 bảng cấu thành nên hệ thống E-Learning, được chia theo các phân hệ chức năng logic:

### Phân hệ 1: Quản lý Người dùng

**Bảng 1: `users` (Quản lý tài khoản người dùng)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã định danh duy nhất của người dùng. |
| `name` | VARCHAR(100) | NULL | Họ và tên đầy đủ của người dùng. |
| `email` | VARCHAR(100) | UNIQUE | Email dùng để đăng nhập (không được trùng lặp). |
| `password` | VARCHAR(255) | NULL | Mật khẩu tài khoản (Đã được mã hóa Hash). |
| `role` | VARCHAR(20) | DEFAULT 'user' | Quyền hạn truy cập: `user` (Học viên) hoặc `admin` (Quản trị). |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Thời gian tài khoản được tạo. |

---

### Phân hệ 2: Quản lý Nội dung Khóa học

**Bảng 2: `categories` (Danh mục khóa học)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã định danh danh mục. |
| `name` | VARCHAR(255) | NOT NULL | Tên danh mục (VD: Lập trình, Thiết kế). |

**Bảng 3: `courses` (Thông tin tổng quan Khóa học)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã định danh khóa học. |
| `category_id` | INT | Khóa ngoại (categories.id) | Phân loại khóa học thuộc danh mục nào. |
| `title` | VARCHAR(255) | NULL | Tên khóa học. |
| `description` | TEXT | NULL | Mô tả chi tiết nội dung khóa học. |
| `price` | DECIMAL(10,2) | DEFAULT 0.00 | Giá bán của khóa học. |
| `image` | VARCHAR(255) | NULL | Đường dẫn URL ảnh bìa khóa học. |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Thời gian tạo khóa học. |

**Bảng 4: `lessons` (Nội dung chi tiết Bài học)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã định danh bài học. |
| `course_id` | INT | Khóa ngoại (courses.id), NOT NULL| Xác định bài học thuộc về khóa học nào. |
| `title` | VARCHAR(255) | NOT NULL | Tiêu đề bài học. |
| `content` | TEXT | NULL | Nội dung văn bản của bài học. |
| `video` | VARCHAR(255) | NULL | Đường dẫn nhúng video bài giảng (Youtube/MP4). |
| `position` | INT | DEFAULT 0 | Số thứ tự sắp xếp bài học trong lộ trình. |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Thời gian thêm bài học. |

---

### Phân hệ 3: Thương mại điện tử (Mua bán Khóa học)

**Bảng 5: `cart` (Giỏ hàng tạm thời)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã record giỏ hàng. |
| `user_id` | INT | Khóa ngoại (users.id) | Người dùng sở hữu giỏ hàng. |
| `course_id` | INT | Khóa ngoại (courses.id) | Khóa học được thêm vào giỏ. |

**Bảng 6: `orders` (Hóa đơn / Đơn hàng)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã đơn hàng. |
| `user_id` | INT | Khóa ngoại (users.id) | Người thực hiện thanh toán. |
| `total` | DECIMAL(10,2)| NULL | Tổng số tiền của đơn hàng. |
| `status` | VARCHAR(50) | NULL | Trạng thái thanh toán (VD: paid, pending). |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Thời gian tạo đơn hàng. |

**Bảng 7: `order_items` (Chi tiết từng món trong Đơn hàng)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã chi tiết đơn hàng. |
| `order_id` | INT | Khóa ngoại (orders.id) | Thuộc về hóa đơn nào. |
| `course_id` | INT | Khóa ngoại (courses.id) | Khóa học nào được mua trong hóa đơn này. |
| `price` | DECIMAL(10,2)| NULL | Giá của khóa học tại thời điểm mua. |

---

### Phân hệ 4: Học tập & Đánh giá

**Bảng 8: `user_courses` (Khóa học đã sở hữu)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã record cấp quyền. |
| `user_id` | INT | Khóa ngoại (users.id), NOT NULL | ID Học viên. |
| `course_id` | INT | Khóa ngoại (courses.id), NOT NULL| ID Khóa học được phép truy cập để học. |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Thời điểm được cấp quyền học. |

**Bảng 9: `progress` (Tiến độ học tập)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã tiến độ. |
| `user_id` | INT | Khóa ngoại (users.id) | ID Học viên. |
| `lesson_id` | INT | Khóa ngoại (lessons.id) | ID Bài học đang ghi nhận. |
| `completed` | TINYINT(4) | DEFAULT 1 | Trạng thái hoàn thành bài học (1 là đã học xong). |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Thời điểm hoàn thành. |

**Bảng 10: `quizzes` (Ngân hàng câu hỏi trắc nghiệm)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã câu hỏi. |
| `lesson_id` | INT | Khóa ngoại (lessons.id) | Câu hỏi thuộc về bài kiểm tra của bài học nào. |
| `question` | TEXT | NULL | Nội dung chi tiết của câu hỏi. |
| `option_a` | VARCHAR(255)| NULL | Nội dung đáp án A. |
| `option_b` | VARCHAR(255)| NULL | Nội dung đáp án B. |
| `option_c` | VARCHAR(255)| NULL | Nội dung đáp án C. |
| `option_d` | VARCHAR(255)| NULL | Nội dung đáp án D. |
| `correct_answer`| CHAR(1) | NULL | Ký tự đáp án đúng (A, B, C hoặc D). |

**Bảng 11: `results` (Kết quả điểm thi)**
| Tên trường (Column) | Kiểu dữ liệu | Ràng buộc | Vai trò / Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `id` | INT | Khóa chính, AUTO_INCREMENT | Mã record kết quả. |
| `user_id` | INT | Khóa ngoại (users.id) | ID Học viên thực hiện bài test. |
| `lesson_id` | INT | Khóa ngoại (lessons.id) | ID Bài học chứa bài test. |
| `score` | INT | NULL | Điểm số đạt được hoặc số câu trả lời đúng. |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Thời gian nộp bài thi. |


# THIẾT KẾ USE CASE HỆ THỐNG E-LEARNING

## 1. Danh sách các Use Case tổng quát

Dưới đây là bảng liệt kê các chức năng cốt lõi của hệ thống, phân định rõ vai trò của Học viên (User) và Quản trị viên (Admin).

| ID | Tên Use Case | Tác nhân (Actor) | Mô tả tóm tắt |
| :--- | :--- | :--- | :--- |
| **UC01** | Đăng ký | User | Người dùng tạo tài khoản mới để tham gia hệ thống. |
| **UC02** | Đăng nhập | User, Admin | Xác thực quyền truy cập vào hệ thống. |
| **UC03** | Lọc và Tìm kiếm khóa học | User | Tìm khóa học theo từ khóa, danh mục hoặc học phí. |
| **UC04** | Xem chi tiết khóa học | User | Xem lộ trình bài học và thông tin trước khi mua. |
| **UC05** | Quản lý Giỏ hàng | User | Thêm/Xóa khóa học vào giỏ hàng cá nhân. |
| **UC06** | Thanh toán đơn hàng | User | Thực hiện mua khóa học và cấp quyền sở hữu. |
| **UC07** | Học bài trực tuyến | User | Xem nội dung bài giảng video và văn bản. |
| **UC08** | Theo dõi tiến độ | User | Xem phần trăm (%) hoàn thành bài học của mỗi khóa. |
| **UC09** | Làm bài kiểm tra (Quiz) | User | Thực hiện bài trắc nghiệm cuối mỗi bài học. |
| **UC10** | Xem kết quả và Làm lại | User | Xem điểm số, đáp án đúng/sai và thực hiện thi lại. |
| **UC11** | Quản lý Danh mục & Khóa học| Admin | Thêm, sửa, xóa danh mục và thông tin khóa học. |
| **UC12** | Quản lý Bài giảng & Quiz | Admin | Xây dựng nội dung bài học và ngân hàng câu hỏi. |
| **UC13** | Quản lý Người dùng | Admin | Quản lý danh sách thành viên và phân quyền hệ thống. |
| **UC14** | Quản lý Đơn hàng & Thống kê| Admin | Theo dõi các giao dịch mua hàng và báo cáo doanh thu. |

---

## 2. Sơ đồ Use Case tổng quát (Mermaid Diagram)
flowchart LR

%% Style tổng thể
classDef actor fill:#e6e6fa,stroke:#8a79c9,stroke-width:1px;
classDef usecase fill:#e6e6fa,stroke:#8a79c9,stroke-width:1px;
classDef system fill:#f5f5dc,stroke:#c2b280,stroke-width:2px;

%% Actors
User((User)):::actor
Admin((Admin)):::actor

%% System
subgraph SYS["Hệ thống E-Learning Mini"]
    direction TB

    UC01([Đăng ký]):::usecase
    UC02([Đăng nhập]):::usecase
    UC03([Lọc & Tìm kiếm khóa học]):::usecase
    UC05([Quản lý giỏ hàng]):::usecase
    UC06([Thanh toán]):::usecase
    UC07([Học trực tuyến]):::usecase
    UC08([Theo dõi tiến độ]):::usecase
    UC10([Làm bài & Làm lại Quiz]):::usecase

    UC11([Quản lý khóa học & Danh mục]):::usecase
    UC12([Quản lý bài giảng & Quiz]):::usecase
    UC13([Quản lý người dùng]):::usecase
    UC14([Quản lý đơn hàng & Thống kê]):::usecase
end

%% Gán style cho system
class SYS system

%% User
User --> UC01
User --> UC02
User --> UC03
User --> UC05
User --> UC06
User --> UC07
User --> UC08
User --> UC10

%% Admin
Admin --> UC11
Admin --> UC12
Admin --> UC13
Admin --> UC14


// USE CASE CHI TIẾT
```mermaid
flowchart LR

%% Style tím
classDef actor fill:#e6e6fa,stroke:#8a79c9,stroke-width:1px;
classDef usecase fill:#e6e6fa,stroke:#8a79c9,stroke-width:1px;

Guest((Khách)):::actor

UC01([Đăng ký]):::usecase
UC01_1([Nhập thông tin]):::usecase
UC01_2([Kiểm tra email]):::usecase
UC01_3([Mã hóa mật khẩu]):::usecase

Guest --> UC01
UC01 --> UC01_1
UC01 --> UC01_2
UC01 --> UC01_3


// UC02
```mermaid
flowchart LR

%% Style tím
classDef actor fill:#e6e6fa,stroke:#8a79c9,stroke-width:1px;
classDef usecase fill:#e6e6fa,stroke:#8a79c9,stroke-width:1px;

User(("Người dùng (User/Admin)")):::actor

subgraph "Phân hệ Xác thực"
    UC02(["UC02: Đăng nhập"]):::usecase
    UC02_1(["Xác thực tài khoản"]):::usecase
    UC02_2(["Phân quyền truy cập"]):::usecase
    UC02_3(["Báo lỗi đăng nhập"]):::usecase
end

User --> UC02

%% include (luôn xảy ra)
UC02 -. include .-> UC02_1
UC02 -. include .-> UC02_2

%% extend (khi lỗi)
UC02 -. extend .-> UC02_3
---

# ✅ UC03 – Lọc & Tìm kiếm khóa học

---

# ✅ UC03 – Tìm kiếm & Lọc (màu tím + chuẩn hóa)

```md
```mermaid
flowchart LR

%% Style tím
classDef actor fill:#e6e6fa,stroke:#8a79c9,stroke-width:1px;
classDef usecase fill:#e6e6fa,stroke:#8a79c9,stroke-width:1px;

Student(("Học viên (User)")):::actor

subgraph "Phân hệ Tìm kiếm"
    UC03(["UC03: Tìm kiếm khóa học"]):::usecase
    UC03_1(["Tìm theo từ khóa"]):::usecase
    UC03_2(["Lọc theo danh mục"]):::usecase
    UC03_3(["Lọc theo giá"]):::usecase
    UC03_4(["Hiển thị kết quả"]):::usecase
end

Student --> UC03

%% include
UC03 -. include .-> UC03_1
UC03 -. include .-> UC03_2
UC03 -. include .-> UC03_3
UC03 -. include .-> UC03_4
