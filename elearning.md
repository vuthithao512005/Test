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

# 2. Sơ đồ Use Case tổng quát

Thành phần	Nội dung
Use Case	Đăng ký tài khoản (UC01)
Actor	Khách vãng lai (Guest)
Mục tiêu	Tạo một tài khoản mới để trở thành thành viên của hệ thống
Tiền điều kiện	Người dùng chưa đăng nhập, chưa có tài khoản
Luồng chính	1. Truy cập trang đăng ký
2. Nhập thông tin
3. Nhấn đăng ký
4. Hệ thống kiểm tra và lưu DB
5. Thông báo thành công
Ngoại lệ	Email đã tồn tại, thiếu dữ liệu, sai định dạng
Luồng ngoại lệ	Hiển thị lỗi và yêu cầu nhập lại

class SYS system

User --> UC01
User --> UC02
User --> UC03
Admin --> UC02
