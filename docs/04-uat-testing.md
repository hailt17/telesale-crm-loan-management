# Kịch Bản Kiểm Thử Người Dùng Chấp Nhận (UAT Test Scenarios)

## 1. Mục đích
Tài liệu này mô tả chi tiết các kịch bản kiểm thử người dùng (UAT) cho hệ thống CRM quản lý hồ sơ vay Telesale. Các kịch bản tập trung kiểm tra toàn diện các chức năng cốt lõi trong phạm vi MVP, bao gồm cả luồng xử lý thành công (Happy Path) và luồng xử lý ngoại lệ (Exception Flow). Đây là căn cứ để Admin, Teamlead và Telesale nghiệm thu tính đúng đắn của hệ thống trước khi đưa vào vận hành thực tế.

---

## 2. Kịch bản kiểm thử – Import danh sách khách hàng

| TC ID | Test Scenario | Pre-condition | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_IMPORT_001** | Upload file hợp lệ và import thành công | User đã đăng nhập và có quyền import. | 1. Mở màn Import khách hàng.<br>2. Chọn file `.xlsx` hợp lệ.<br>3. Bấm Kiểm tra file.<br>4. Bấm Import. | Hệ thống import thành công và hiển thị popup Import thành công. | High |
| **TC_IMPORT_002** | Upload file sai định dạng | User đã đăng nhập. | 1. Chọn file `.pdf` hoặc `.csv`.<br>2. Bấm Kiểm tra file. | Hệ thống hiển thị lỗi file sai định dạng và không cho import. | High |
| **TC_IMPORT_003** | Upload file vượt quá dung lượng cho phép | User đã đăng nhập. | 1. Chọn file lớn hơn 10MB.<br>2. Bấm Kiểm tra file. | Hệ thống hiển thị lỗi dung lượng file vượt quá giới hạn. | Medium |
| **TC_IMPORT_004** | File thiếu cột bắt buộc | User đã đăng nhập. | 1. Chọn file thiếu cột Số điện thoại.<br>2. Bấm Kiểm tra file. | Hệ thống hiển thị màn Lỗi kiểm tra file. | High |
| **TC_IMPORT_005** | File có dữ liệu số tiền vay không hợp lệ | User đã đăng nhập. | 1. Chọn file có giá trị “abc” tại cột Số tiền vay.<br>2. Bấm Kiểm tra file. | Hệ thống hiển thị lỗi “Số tiền vay phải là số”. | High |
| **TC_IMPORT_006** | File có bản ghi thiếu địa chỉ | User đã đăng nhập. | 1. Chọn file có dòng thiếu địa chỉ.<br>2. Bấm Kiểm tra file. | Hệ thống hiển thị dòng lỗi tương ứng trong bảng lỗi. | High |
| **TC_IMPORT_007** | File có bản ghi trùng số điện thoại | User đã đăng nhập. | 1. Chọn file có SĐT đã tồn tại trong CRM.<br>2. Bấm Kiểm tra file. | Hệ thống hiển thị bản ghi trong màn Kết quả trùng dữ liệu. | High |
| **TC_IMPORT_008** | File có bản ghi trùng CCCD/CMND | User đã đăng nhập. | 1. Chọn file có CCCD/CMND đã tồn tại trong CRM.<br>2. Bấm Kiểm tra file. | Hệ thống hiển thị lý do trùng CCCD/CMND. | High |
| **TC_IMPORT_009** | File có khách hàng đang có hồ sơ BPM | User đã đăng nhập. | 1. Chọn file có khách hàng đang có hồ sơ BPM.<br>2. Bấm Kiểm tra file. | Hệ thống đánh dấu bản ghi là không được import để tránh trùng quy trình. | High |
| **TC_IMPORT_010** | Import bản ghi hợp lệ khi file có lỗi và trùng | File đã được kiểm tra, có bản ghi hợp lệ, lỗi và trùng. | 1. Bấm Import bản ghi hợp lệ. | Hệ thống chỉ import bản ghi hợp lệ, loại bỏ các bản ghi lỗi/trùng. | High |
| **TC_IMPORT_011** | Tải báo cáo lỗi | File có dữ liệu lỗi. | 1. Ở màn Lỗi kiểm tra file.<br>2. Bấm Tải báo cáo lỗi. | Hệ thống tải báo cáo lỗi gồm dòng, trường dữ liệu, giá trị hiện tại và nguyên nhân lỗi. | Medium |
| **TC_IMPORT_012** | Tải báo cáo trùng | File có bản ghi trùng. | 1. Ở màn Kết quả trùng dữ liệu.<br>2. Bấm Tải báo cáo trùng. | Hệ thống tải danh sách bản ghi trùng về máy để đối chiếu. | Medium |
| **TC_IMPORT_013** | Hủy thao tác import | User đang ở màn Import. | 1. Chọn file.<br>2. Bấm Hủy. | Hệ thống hủy thao tác, không tạo lead mới trên hệ thống. | Medium |
| **TC_IMPORT_014** | Tiếp tục import sau khi import thành công | Import đã thành công. | 1. Ở popup Import thành công.<br>2. Bấm Tiếp tục import. | Hệ thống điều hướng quay lại màn Import khách hàng ban đầu. | Low |
| **TC_IMPORT_015** | Quay về danh sách hồ sơ sau import | Import đã thành công. | 1. Ở popup Import thành công.<br>2. Bấm Quay về danh sách hồ sơ. | Hệ thống điều hướng sang màn Danh sách hồ sơ khách hàng. | Medium |

---

## 3. Kịch bản kiểm thử – Danh sách và chi tiết hồ sơ

| TC ID | Test Scenario | Pre-condition | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_CASE_001** | Xem danh sách hồ sơ | User đã đăng nhập và có quyền xem hồ sơ. | 1. Mở màn Danh sách hồ sơ. | Hệ thống hiển thị danh sách hồ sơ theo phạm vi phân quyền của tài khoản. | High |
| **TC_CASE_002** | Tìm kiếm hồ sơ theo mã hồ sơ | Có hồ sơ `HS001` trong hệ thống. | 1. Nhập “HS001” vào ô tìm kiếm.<br>2. Bấm Lọc dữ liệu. | Hệ thống hiển thị chính xác bộ hồ sơ `HS001`. | High |
| **TC_CASE_003** | Tìm kiếm hồ sơ theo tên khách hàng | Có khách hàng Nguyễn Văn A trong danh sách. | 1. Nhập “Nguyễn Văn A”.<br>2. Bấm Lọc dữ liệu. | Hệ thống hiển thị hồ sơ của khách hàng Nguyễn Văn A. | High |
| **TC_CASE_004** | Tìm kiếm hồ sơ theo số điện thoại | Có hồ sơ với SĐT `0901234567`. | 1. Nhập SĐT `0901234567`.<br>2. Bấm Lọc dữ liệu. | Hệ thống hiển thị hồ sơ tương ứng với số điện thoại tra cứu. | High |
| **TC_CASE_005** | Lọc hồ sơ theo trạng thái | Có hồ sơ ở nhiều trạng thái. | 1. Chọn trạng thái “Đã chuyển Courier”.<br>2. Bấm Lọc dữ liệu. | Hệ thống chỉ hiển thị hồ sơ có trạng thái Đã chuyển Courier. | High |
| **TC_CASE_006** | Lọc hồ sơ theo nhóm phụ trách | Có nhiều nhóm Telesale hoạt động. | 1. Chọn "Nhóm Telesale 01".<br>2. Bấm Lọc dữ liệu. | Hệ thống hiển thị danh sách hồ sơ thuộc nhóm đã chọn. | Medium |
| **TC_CASE_007** | Lọc hồ sơ theo Telesale phụ trách | Có hồ sơ được phân cho tài khoản `TS001`. | 1. Nhập/chọn `TS001`.<br>2. Bấm Lọc dữ liệu. | Hệ thống hiển thị toàn bộ hồ sơ do nhân sự `TS001` phụ trách. | Medium |
| **TC_CASE_008** | Không tìm thấy hồ sơ | Không có hồ sơ khớp với điều kiện tra cứu. | 1. Nhập từ khóa không tồn tại.<br>2. Bấm Lọc dữ liệu. | Hệ thống hiển thị trạng thái không có dữ liệu (No data found). | Medium |
| **TC_CASE_009** | Mở chi tiết hồ sơ | Danh sách hồ sơ có dữ liệu hoạt động. | 1. Bấm Chi tiết tại hồ sơ `HS001`. | Hệ thống mở màn hình Chi tiết hồ sơ `HS001`. | High |
| **TC_CASE_010** | Hiển thị đầy đủ thông tin hồ sơ | Hồ sơ có đầy đủ dữ liệu trong DB. | 1. Mở Chi tiết hồ sơ. | Hiển thị đầy đủ thông tin khách hàng, khoản vay, kết quả gọi, Courier, file đính kèm và timeline lịch sử trạng thái. | High |
| **TC_CASE_011** | Cập nhật thông tin khách hàng hợp lệ | User có quyền cập nhật hồ sơ. | 1. Sửa địa chỉ khách hàng.<br>2. Bấm Lưu thay đổi. | Hệ thống lưu thông tin mới thành công và cập nhật thời gian chỉnh sửa cuối. | High |
| **TC_CASE_012** | Lưu hồ sơ khi thiếu trường bắt buộc | User đang ở màn chi tiết. | 1. Xóa số điện thoại.<br>2. Bấm Lưu thay đổi. | Hệ thống báo lỗi trường bắt buộc và không lưu dữ liệu mới vào DB. | High |
| **TC_CASE_013** | Cập nhật kết quả gọi | User có quyền xử lý hồ sơ. | 1. Chọn kết quả gọi.<br>2. Nhập ghi chú cuộc gọi.<br>3. Bấm Lưu thay đổi. | Hệ thống lưu kết quả gọi thành công và ghi nhận chính xác tài khoản người cập nhật. | High |
| **TC_CASE_014** | Chọn thao tác không hợp lệ với trạng thái hiện tại | Bộ hồ sơ chưa đạt mốc "Đồng ý vay". | 1. Chọn thao tác "Chuyển Courier".<br>2. Bấm Xác nhận. | Hệ thống chặn thao tác, hiển thị lỗi không đủ điều kiện chuyển Courier. | High |
| **TC_CASE_015** | Xem lịch sử trạng thái | Hồ sơ đã qua nhiều trạng thái luân chuyển. | 1. Mở Chi tiết hồ sơ.<br>2. Xem khu vực Lịch sử trạng thái. | Hệ thống hiển thị timeline rõ ràng gồm thời gian, trạng thái và người thực hiện. | Medium |
| **TC_CASE_016** | Xuất danh sách hồ sơ | User có quyền xuất file dữ liệu. | 1. Chọn điều kiện lọc.<br>2. Bấm Xuất file. | Hệ thống xuất file Excel danh sách hồ sơ chuẩn theo điều kiện lọc. | Medium |

---

## 4. Kịch bản kiểm thử – Chuyển hồ sơ sang Courier

| TC ID | Test Scenario | Pre-condition | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_COURIER_001** | Mở popup chuyển Courier | Hồ sơ đang có trạng thái Đồng ý vay. | 1. Mở chi tiết hồ sơ.<br>2. Chọn thao tác Chuyển Courier.<br>3. Bấm Xác nhận. | Hệ thống kích hoạt hiển thị popup Chuyển hồ sơ sang Courier. | High |
| **TC_COURIER_002** | Chuyển Courier thành công | Hồ sơ đủ điều kiện và đầy đủ thông tin bắt buộc. | 1. Kiểm tra thông tin trong popup.<br>2. Bấm Xác nhận chuyển Courier. | Hệ thống đổi trạng thái hồ sơ thành Đã chuyển Courier và hiển thị popup thành công. | High |
| **TC_COURIER_003** | Chuyển Courier khi thiếu số điện thoại | Hồ sơ bị khuyết số điện thoại khách hàng. | 1. Bấm Xác nhận chuyển Courier. | Hệ thống chặn lại và hiển thị popup Chuyển Courier thất bại. | High |
| **TC_COURIER_004** | Chuyển Courier khi thiếu địa chỉ thu hồ sơ | Hồ sơ bị khuyết thông tin địa chỉ thực địa. | 1. Bấm Xác nhận chuyển Courier. | Hệ thống hiển thị lỗi thiếu thông tin địa chỉ thu hồ sơ giấy. | High |
| **TC_COURIER_005** | Chuyển Courier khi chưa chọn Courier phụ trách | Chưa chọn nhân sự gán việc. | 1. Để trống ô Courier phụ trách.<br>2. Bấm Xác nhận chuyển Courier. | Hệ thống hiển thị thông báo lỗi bắt buộc chọn Courier. | High |
| **TC_COURIER_006** | Chuyển Courier cho hồ sơ chưa đồng ý vay | Hồ sơ đang ở trạng thái Đang xử lý. | 1. Chọn thao tác Chuyển Courier. | Hệ thống tự động từ chối thao tác (ẩn hoặc khóa nút gán việc). | High |
| **TC_COURIER_007** | Chuyển Courier cho hồ sơ đã hủy | Hồ sơ đang ở trạng thái Hủy hồ sơ. | 1. Chọn thao tác Chuyển Courier. | Hệ thống khóa tính năng, không cho phép thực hiện thao tác này. | High |
| **TC_COURIER_008** | Hủy thao tác chuyển Courier | Giao diện popup chuyển Courier đang mở. | 1. Bấm Hủy. | Hệ thống đóng popup, không cập nhật trạng thái mới của hồ sơ. | Medium |
| **TC_COURIER_009** | Quay về chi tiết sau khi chuyển thành công | Tiến trình chuyển Courier hoàn tất. | 1. Bấm Quay về chi tiết hồ sơ trên popup. | Hệ thống đóng màn thông báo và quay lại giao diện Chi tiết hồ sơ. | Low |
| **TC_COURIER_010** | Điều hướng sang Theo dõi Courier sau khi chuyển thành công | Tiến trình chuyển Courier hoàn tất. | 1. Bấm Theo dõi Courier trên popup. | Hệ thống tự động điều hướng mở màn hình Theo dõi Courier. | Medium |

---

## 5. Kịch bản kiểm thử – Theo dõi tiến độ Courier

| TC ID | Test Scenario | Pre-condition | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_TRACK_001** | Xem danh sách hồ sơ Courier | Hệ thống đã có hồ sơ chuyển sang phân hệ Courier. | 1. Mở màn Theo dõi Courier. | Hệ thống hiển thị danh sách hồ sơ Courier kèm thông tin tiến độ liên quan. | High |
| **TC_TRACK_002** | Lọc theo trạng thái Courier | Có hồ sơ ở nhiều trạng thái thực địa khác nhau. | 1. Chọn trạng thái “Đang thu hồ sơ”.<br>2. Bấm Lọc dữ liệu. | Hệ thống hiển thị chính xác các hồ sơ có trạng thái Đang thu hồ sơ. | High |
| **TC_TRACK_003** | Lọc theo Courier phụ trách | Có hồ sơ được phân công cho nhân sự Phạm Văn B. | 1. Chọn Courier Phạm Văn B.<br>2. Bấm Lọc dữ liệu. | Hệ thống hiển thị toàn bộ hồ sơ do Courier Phạm Văn B phụ trách. | Medium |
| **TC_TRACK_004** | Lọc theo khu vực địa lý | Có hồ sơ nằm ở nhiều quận huyện/khu vực. | 1. Chọn khu vực Quận 1.<br>2. Bấm Lọc dữ liệu. | Hệ thống lọc hiển thị các hồ sơ thuộc khu vực Quận 1. | Medium |
| **TC_TRACK_005** | Lọc theo ngày hẹn thu hồ sơ | Có hồ sơ có lịch hẹn cụ thể trong DB. | 1. Chọn ngày hẹn thu.<br>2. Bấm Lọc dữ liệu. | Hệ thống hiển thị hồ sơ có ngày hẹn thu khớp với bộ lọc đã chọn. | Medium |
| **TC_TRACK_006** | Hiển thị nhóm hồ sơ cần chú ý | Có hồ sơ Courier rơi vào nhóm lỗi vận hành (quá hạn/bổ sung). | 1. Mở màn Theo dõi Courier. | Hệ thống tự động gom nhóm và hiển thị hồ sơ lỗi tại khu vực Hồ sơ cần chú ý. | High |
| **TC_TRACK_007** | Courier cập nhật thu hồ sơ thành công | Hồ sơ đang được Courier xử lý thực địa. | 1. Cập nhật trạng thái Courier thành "Thu hồ sơ thành công". | Cập nhật trạng thái Courier, đồng thời ghi log chính xác thời gian hoàn thành. | High |
| **TC_TRACK_008** | Courier cập nhật yêu cầu bổ sung | Khách nộp thiếu giấy tờ chứng từ khi gặp mặt. | 1. Cập nhật trạng thái Courier thành "Yêu cầu bổ sung". | Trạng thái cập nhật thành công, hồ sơ tự động được đưa vào nhóm cần chú ý. | High |
| **TC_TRACK_009** | Courier cập nhật không liên hệ được khách | Courier không liên hệ được khách hàng ngoài thực địa. | 1. Cập nhật trạng thái thành "Không liên hệ được". | Trạng thái cập nhật thành công, hồ sơ tự động đưa vào nhóm cần chú ý. | Medium |
| **TC_TRACK_010** | Xuất danh sách hồ sơ Courier | User có quyền xuất file báo cáo dữ liệu. | 1. Chọn điều kiện lọc.<br>2. Bấm Xuất file. | Hệ thống xuất danh sách hồ sơ Courier định dạng Excel chuẩn theo bộ lọc. | Medium |

---

## 6. Kịch bản kiểm thử – Dashboard và báo cáo vận hành

| TC ID | Test Scenario | Pre-condition | Test Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_REPORT_001** | Xem Dashboard tổng quan | User có quyền truy cập Dashboard. | 1. Mở Trang chủ hệ thống CRM. | Hiển thị chính xác các số liệu Realtime của KPI tổng lead, lead mới, chuyển Courier, gửi BPM, bổ sung và hủy. | High |
| **TC_REPORT_002** | Xem biểu đồ phân bổ trạng thái hồ sơ | Hệ thống đang có dữ liệu hồ sơ phân rã theo trạng thái. | 1. Mở Trang chủ hệ thống CRM. | Biểu đồ phân bổ hiển thị trực quan tỷ lệ phần trăm chuẩn theo dữ liệu thực tế. | Medium |
| **TC_REPORT_003** | Xem bảng danh sách hồ sơ cần chú ý | Có hồ sơ lỗi vận hành tồn tại trên hệ thống. | 1. Mở Trang chủ hệ thống CRM. | Hiển thị bảng tổng hợp các hồ sơ cần xử lý gấp để quản lý can thiệp. | Medium |
| **TC_REPORT_004** | Xem báo cáo năng suất xử lý trong ngày | User có quyền xem hệ thống báo cáo. | 1. Mở màn Báo cáo xử lý trong ngày. | Hiển thị đầy đủ hệ thống chỉ số KPI, biểu đồ và bảng báo cáo chi tiết theo từng mã Telesale. | High |
| **TC_REPORT_005** | Lọc số liệu báo cáo theo ngày | Hệ thống lưu trữ dữ liệu báo cáo qua nhiều ngày. | 1. Chọn khung ngày báo cáo.<br>2. Bấm Lọc dữ liệu. | Hệ thống tính toán lại và hiển thị chính xác số liệu trong phạm vi ngày gán lọc. | Medium |
| **TC_REPORT_006** | Lọc báo cáo theo nhóm Telesale | Có dữ liệu hoạt động của nhiều nhóm phòng ban. | 1. Chọn nhóm phụ trách.<br>2. Bấm Lọc dữ liệu. | Số liệu hiển thị thu hẹp chuẩn theo phạm vi nhóm được chọn. | Medium |
| **TC_REPORT_007** | Lọc báo cáo theo nhân sự Telesale | Có dữ liệu chi tiết của nhiều nhân viên. | 1. Chọn tài khoản Telesale cần xem.<br>2. Bấm Lọc dữ liệu. | Số liệu hiển thị chi tiết năng suất của riêng nhân sự được chọn. | Medium |
| **TC_REPORT_008** | Kiểm tra logic tính toán tỷ lệ chuyển đổi | Bảng báo cáo hiển thị lượng lead và lượng đồng ý vay. | 1. Mở báo cáo.<br>2. Thực hiện kiểm tra tính toán cột Tỷ lệ chuyển đổi. | Tỷ lệ phần trăm chuyển đổi hiển thị đúng theo công thức nghiệp vụ quy định. | High |
| **TC_REPORT_009** | Xuất báo cáo hiệu suất vận hành | User có quyền xuất file dữ liệu báo cáo. | 1. Chọn điều kiện lọc.<br>2. Bấm Xuất báo cáo. | Hệ thống kết xuất file báo cáo chuẩn định dạng dựa trên phạm vi số liệu đang lọc hiển thị. | Medium |

---

## 7. Ghi chú điều kiện nghiệm thu (UAT Summary Notes)

*   **Đối tượng tham gia thực hiện UAT:** Admin/Manager, Teamlead và đội ngũ nhân sự đại diện phòng Telesale.
*   **Dữ liệu sử dụng trong quá trình test (Test Data):** Sử dụng tệp tin file import dữ liệu mẫu, thông tin khách hàng mẫu, tài khoản nhân sự mẫu và các trạng thái Courier giả lập dựa trên kịch bản nghiệp vụ.
*   **Phạm vi kiểm thử chấp nhận (In-Scope):** Toàn bộ luồng xử lý trên giao diện Web App CRM bao gồm: chức năng Import khách hàng, màn hình Quản lý danh sách hồ sơ, Popup Chi tiết hồ sơ, luồng bàn giao sang phân hệ Courier và hệ thống Dashboard/Báo cáo vận hành tổng quan.
*   **Ngoài phạm vi kiểm thử (Out-of-Scope):** Tiến trình đồng bộ tích hợp dữ liệu với Mobile App Courier thực tế ngoài thực địa, luồng xử lý phê duyệt thẩm định tự động phía trong Core BPM và quy trình giải ngân tài chính của ngân hàng/tổ chức tín dụng phía sau.
*   **Tiêu chí phê duyệt đạt chuẩn UAT (Exit Criteria):**
    *   **100%** các Test Cases được gắn nhãn độ ưu tiên cao (**High Priority**) bắt buộc phải vượt qua vòng kiểm thử thành công (Pass).
    *   Các Test Cases có mức ưu tiên trung bình và thấp (**Medium/Low Priority**) không tồn tại bất kỳ lỗi nghiêm trọng nào gây tắc nghẽn luồng xử lý hệ thống hoặc sai lệch cấu trúc dữ liệu cốt lõi.
