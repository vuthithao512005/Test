## 2.3 Sơ đồ cơ sở dữ liệu (ERD)

### 2.3.1 Mô tả

Hệ thống E-Learning Mini sử dụng cơ sở dữ liệu quan hệ để lưu trữ thông tin người dùng, khóa học, bài học, bài kiểm tra và tiến độ học tập. Các bảng được thiết kế nhằm đảm bảo tính nhất quán dữ liệu và hỗ trợ truy vấn hiệu quả.

---

### 2.3.2 Các bảng chính

- **Users**: Lưu thông tin người dùng  
- **Courses**: Lưu thông tin khóa học  
- **Lessons**: Lưu nội dung bài học  
- **Quizzes**: Lưu bài kiểm tra  
- **Results**: Lưu kết quả bài kiểm tra  
- **Progress**: Lưu tiến độ học tập  

---

### 2.3.3 Sơ đồ ERD

```mermaid
erDiagram

USERS {
    int id PK
    string name
    string email
    string password
    string role
}

COURSES {
    int id PK
    string title
    string description
}

LESSONS {
    int id PK
    string title
    text content
    int course_id FK
}

QUIZZES {
    int id PK
    string question
    string answer
    int lesson_id FK
}

RESULTS {
    int id PK
    int user_id FK
    int quiz_id FK
    float score
}

PROGRESS {
    int id PK
    int user_id FK
    int lesson_id FK
    int status
}

USERS ||--o{ RESULTS : làm
USERS ||--o{ PROGRESS : học

COURSES ||--o{ LESSONS : chứa
LESSONS ||--o{ QUIZZES : có

QUIZZES ||--o{ RESULTS : tạo
LESSONS ||--o{ PROGRESS : theo dõi
```

---

### 2.3.4 Mô tả quan hệ

- Một người dùng có thể làm nhiều bài kiểm tra → USERS - RESULTS (1-n)  
- Một người dùng có nhiều tiến độ học → USERS - PROGRESS (1-n)  
- Một khóa học có nhiều bài học → COURSES - LESSONS (1-n)  
- Một bài học có nhiều câu hỏi → LESSONS - QUIZZES (1-n)  
- Một bài kiểm tra có nhiều kết quả → QUIZZES - RESULTS (1-n)  
- Một bài học có nhiều tiến độ học → LESSONS - PROGRESS (1-n)  

---

### 2.3.5 Kết luận

Sơ đồ ERD thể hiện rõ cấu trúc dữ liệu và mối quan hệ giữa các bảng trong hệ thống. Thiết kế này đảm bảo hỗ trợ đầy đủ các chức năng như quản lý khóa học, học bài, làm bài kiểm tra và theo dõi tiến độ học tập.
