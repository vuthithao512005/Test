# Đặc Tả Use Case: Quản Lý Giỏ Hàng

## Bảng Mô Tả Use Case Tổng Hợp (Gộp)

| Thuộc tính | Nội dung |
| :--- | :--- |
| **Tên Use Case** | Quản lý / Điều chỉnh giỏ hàng |
| **Tác nhân** | Người dùng |
| **Mục đích** | Người dùng có thể xem lại danh sách sản phẩm, thay đổi số lượng hoặc xóa sản phẩm khỏi giỏ hàng trước khi thanh toán. |
| **Tiền điều kiện** | Người dùng đã thêm ít nhất 1 sản phẩm vào giỏ và đang ở trang Giỏ hàng. |
| **Luồng sự kiện chính** | 1. Hệ thống hiển thị danh sách sản phẩm (tên, giá, số lượng) và Tổng tiền hiện tại.<br>2. Người dùng thực hiện một trong các thao tác:<br>   - **Tăng số lượng (+):** Hệ thống kiểm tra, nếu nhỏ hơn mức tồn kho thì cộng thêm 1.<br>   - **Giảm số lượng (-):** Nếu số lượng hiện tại > 1, hệ thống trừ đi 1.<br>   - **Xóa sản phẩm:** Hệ thống loại bỏ sản phẩm đó khỏi Session.<br>   - **Xóa tất cả:** Hệ thống làm trống toàn bộ Session giỏ hàng.<br>3. Hệ thống tính toán lại Thành tiền và Tổng tiền thanh toán.<br>4. Tải lại trang để cập nhật giao diện mới nhất. |
| **Luồng ngoại lệ** | - Nếu người dùng bấm "Tăng" nhưng sản phẩm đã đạt tối đa số lượng trong kho: Hệ thống từ chối và giữ nguyên số lượng.<br>- Nếu người dùng bấm "Giảm" khi số lượng đang là 1: Hệ thống bỏ qua thao tác để tránh số lượng bằng 0 hoặc âm. |
| **Hậu điều kiện** | Thông tin giỏ hàng (số lượng, tổng tiền) được cập nhật chính xác trong phiên làm việc (Session). |  

# Bảng Mô Tả Sơ Đồ Hoạt Động (Activity Diagram) - Quy Trình Quản Lý Giỏ Hàng Phức Tạp (Phiên bản v2)

Bảng dưới đây mô tả chi tiết các bước thực hiện, tác nhân tương ứng và nội dung mô tả xử lý trong sơ đồ hoạt động của chức năng Quản lý Giỏ hàng.

| Bước | Tác nhân (Actor) | Hành động | Mô tả |
| :---: | :--- | :--- | :--- |
| **1** | **Người dùng** | Truy cập trang Giỏ hàng | Gửi yêu cầu xem giỏ hàng (thường là phương thức POST hoặc GET) lên hệ thống. |
| **2** | **Hệ thống** | Hiển thị danh sách ban đầu | Tiếp nhận yêu cầu, xử lý và lấy dữ liệu giỏ hàng hiện tại để hiển thị danh sách sản phẩm ban đầu cho người dùng thấy. |
| **3** | **Người dùng** | Chọn thao tác trên mặt hàng | Người dùng thực hiện lựa chọn một trong các thao tác điều chỉnh trên giao diện giỏ hàng. |
| **4a** | **Hệ thống** | Tăng số lượng mặt hàng (+) | Hệ thống thực hiện tăng số lượng mặt hàng thêm 1 và tiến hành cập nhật (+1) vào Cơ sở dữ liệu (DB) hoặc mảng Session. |
| **4b** | **Hệ thống** | Giảm số lượng mặt hàng (-) | Hệ thống thực hiện giảm số lượng mặt hàng đi 1 và tiến hành cập nhật (-1) vào DB hoặc Session (có kèm logic chặn để số lượng tối thiểu là 1). |
| **4c** | **Hệ thống** | Xóa một / tất cả sản phẩm | Hệ thống thực hiện loại bỏ một sản phẩm cụ thể ra khỏi giỏ theo ID hoặc hủy toàn bộ mảng Session giỏ hàng nếu chọn xóa tất cả. |
| **5** | **Hệ thống** | Tính toán và cập nhật | Sau khi xử lý xong các thao tác thay đổi, hệ thống tiến hành tính toán lại Thành tiền, Tổng tiền thanh toán và tải lại giao diện giỏ hàng mới để hiển thị đồng bộ. |
| **6** | **Người dùng** | Xem kết quả cập nhật | Người dùng nhận được giao diện giỏ hàng mới đã đồng bộ chính xác dữ liệu vừa thay đổi và kết thúc quy trình. |



# Bảng Mô Tả Giao Diện - Trang Giỏ Hàng

Dưới đây là bảng mô tả chi tiết các thành phần trên giao diện trang Giỏ hàng.

| STT | Thành phần | Định dạng | Ràng buộc | Chức năng |
| :---: | :--- | :--- | :--- | :--- |
| **1** | Tiêu đề trang | Text (H1/Bold) | Không rỗng | Hiển thị tên trang "GIỎ HÀNG" |
| **2** | Thông tin người dùng | Text | Lấy từ Session/Tài khoản | Hiển thị lời chào và tên người dùng đăng nhập (Xin chào: Thảo) |
| **3** | Thanh tiến trình (Các bước) | Navigation Menu / Tabs | Không có | Hiển thị các bước trong quy trình mua hàng (Giỏ hàng, Vận chuyển...) |
| **4** | Cột ID | Number | Tự tăng | Số thứ tự hiển thị của sản phẩm trong giỏ hàng |
| **5** | Cột Mã sp | Text | Lấy từ Database | Hiển thị mã định danh của sản phẩm |
| **6** | Cột Tên sản phẩm | Text | Không rỗng | Hiển thị tên của sản phẩm đã chọn |
| **7** | Cột Hình ảnh | Image (`<img>`) | Đường dẫn ảnh hợp lệ | Hiển thị hình ảnh minh họa cho sản phẩm |
| **8** | Cột Số lượng (Kèm nút +, -) | Number + Buttons | > 0 và <= Số lượng tồn kho | Hiển thị và cho phép người dùng điều chỉnh số lượng mua |
| **9** | Cột Giá sản phẩm | Number (Format tiền tệ) | >= 0 | Hiển thị đơn giá của 1 sản phẩm |
| **10** | Cột Thành tiền | Number (Format tiền tệ) | = Số lượng x Giá sản phẩm | Hiển thị tổng tiền cho từng dòng mặt hàng |
| **11** | Cột Quản lý (Nút Xóa) | Button (Màu đỏ) | Không có | Xóa sản phẩm tương ứng khỏi giỏ hàng |
| **12** | Dòng Tổng tiền | Text (Bold) | = Tổng của tất cả cột Thành tiền | Hiển thị tổng giá trị thanh toán của toàn bộ giỏ hàng |
| **13** | Nút "Xóa tất cả" | Button | Không có | Xóa toàn bộ sản phẩm đang có trong giỏ hàng |
| **14** | Nút "Hình thức vận chuyển" | Button (Link) | Không có | Điều hướng người dùng sang bước tiếp theo (chọn vận chuyển/thanh toán) |

# Bảng Mô Tả Giao Diện - Trang Giỏ Hàng (Rút gọn)

| STT | Thành phần | Định dạng | Ràng buộc | Chức năng |
| :---: | :--- | :--- | :--- | :--- |
| **1** | Tiêu đề trang | Text | Không rỗng | Hiển thị "GIỎ HÀNG" |
| **2** | Tên người dùng | Text | Session | Hiển thị "Xin chào: Thảo" |
| **3** | Thanh tiến trình | Menu | Không | Hiển thị các bước mua hàng |
| **4** | Cột ID | Number | Tự tăng | Số thứ tự dòng |
| **5** | Cột Mã SP | Text | DB | Định danh sản phẩm |
| **6** | Cột Tên sản phẩm | Text | Không rỗng | Hiển thị tên sản phẩm |
| **7** | Cột Hình ảnh | Image | URL hợp lệ | Ảnh minh họa sản phẩm |
| **8** | Cột Số lượng | Input + Button | > 0, <= Kho | Thay đổi số lượng mua |
| **9** | Cột Đơn giá | Number | >= 0 | Giá 1 sản phẩm |
| **10** | Cột Thành tiền | Number | = SL x Giá | Tổng tiền sản phẩm |
| **11** | Nút Xóa (dòng) | Button | Không | Xóa sản phẩm khỏi giỏ |
| **12** | Dòng Tổng tiền | Text (Bold) | = Tổng Thành tiền | Tổng tiền toàn giỏ hàng |
| **13** | Nút Xóa tất cả | Button | Không | Làm trống giỏ hàng |
| **14** | Nút Vận chuyển | Button | Không | Chuyển sang trang kế tiếp |


# Bảng Mô Tả Giao Diện - Trang Đăng Nhập (Rút gọn)

| STT | Thành phần | Định dạng | Ràng buộc | Chức năng |
| :---: | :--- | :--- | :--- | :--- |
| **1** | Tiêu đề form | Text | Không | Hiển thị "Đăng nhập khách hàng" |
| **2** | Nhãn "Tài khoản" | Text | Không | Chú thích ô nhập tài khoản |
| **3** | Ô nhập Tài khoản | Input | Bắt buộc | Nơi nhập Email/Tên đăng nhập |
| **4** | Nhãn "Mật khẩu" | Text | Không | Chú thích ô nhập mật khẩu |
| **5** | Ô nhập Mật khẩu | Input | Bắt buộc | Nơi nhập mật khẩu (ẩn ký tự) |
| **6** | Nút "Đăng nhập" | Button | Không | Gửi thông tin xác thực |
| **7** | Link "Đăng ký..."| Link | Không | Chuyển đến trang Đăng ký |


# Bảng Mô Tả Giao Diện - Trang Chi Tiết Sản Phẩm (Rút gọn)

| STT | Thành phần | Định dạng | Ràng buộc | Chức năng |
| :---: | :--- | :--- | :--- | :--- |
| **1** | Tiêu đề trang | Text | Không | Hiển thị "CHI TIẾT SẢN PHẨM" |
| **2** | Tên sản phẩm | Text (Bold) | Không rỗng | Hiển thị tên sản phẩm |
| **3** | Mã sản phẩm | Text | Theo DB | Hiển thị mã định danh sản phẩm |
| **4** | Giá sản phẩm | Text | >= 0 | Hiển thị giá bán (format tiền tệ) |
| **5** | Số lượng sp | Text | >= 0 | Hiển thị số lượng tồn kho |
| **6** | Danh mục sản phẩm | Text | Không | Hiển thị danh mục chứa sản phẩm |
| **7** | Nút "Thêm giỏ hàng" | Button | Không | Lưu sản phẩm vào giỏ hàng |
| **8** | Nút "Đánh giá..." | Button | Không | Mở giao diện/trang đánh giá sản phẩm |
