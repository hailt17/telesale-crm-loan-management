# Tài Liệu Đặc Tả Yêu Cầu Chức Năng (FS) & Danh Sách User Stories

## 1. Sơ Đồ Ca Sử Dụng Tổng Quan (Mục 6 - Use Case Diagram)

### 1.1 Mô tả Use Case Diagram
Use Case Diagram mô tả các actor chính tham gia vào hệ thống CRM quản lý hồ sơ vay Telesale, gồm:
*   **Admin/Manager**
*   **Teamlead**
*   **Telesale**
*   **Courier**
*   **BPM System**

Các nhóm chức năng chính bao gồm: Import danh sách khách hàng, Quản lý người dùng, Xem dashboard/báo cáo, Xem danh sách hồ sơ, Cập nhật chi tiết hồ sơ, Chuyển hồ sơ sang Courier, Theo dõi Courier, Gửi hồ sơ sang BPM. Sơ đồ giúp xác định phạm vi hệ thống, actor tham gia và các chức năng chính trong MVP.

![Use Case Diagram]<img width="1480" height="842" alt="image" src="https://github.com/user-attachments/assets/38bd33b4-b745-4cad-9892-9bc0fae8b6a3" />


---

## 2. Đặc Tả Chi Tiết Các Phân Hệ Chức Năng (Mục 8 - Functional Specification)

### 📑 Phân hệ FS_01: Import danh sách khách hàng

#### 1. Mục tiêu tính năng
Tính năng Import danh sách khách hàng cho phép Admin/Manager tải file Excel chứa danh sách khách hàng lên hệ thống CRM để tạo lead và phân bổ cho Telesale xử lý. Tính năng này giúp giảm thao tác nhập liệu thủ công, hạn chế sai sót khi quản lý bằng Excel rời rạc, đồng thời hỗ trợ kiểm tra dữ liệu đầu vào trước khi tạo hồ sơ trên CRM.

#### 2. Giao diện màn hình (UI References)
*   **WF_03 – Import danh sách khách hàng:** Màn hình cho phép người dùng tải mẫu file, chọn file Excel, kiểm tra file và thực hiện import dữ liệu hợp lệ vào hệ thống CRM.
*   **WF_03A – Lỗi kiểm tra file:** Màn hình hiển thị khi file import có dữ liệu không hợp lệ như thiếu số điện thoại, sai định dạng CCCD/CMND, số tiền vay không phải dạng số hoặc thiếu địa chỉ.
*   **WF_03B – Kết quả trùng dữ liệu:** Màn hình hiển thị khi hệ thống phát hiện một số bản ghi trùng với dữ liệu hiện có, ví dụ trùng số điện thoại, trùng CCCD/CMND hoặc khách hàng đang có hồ sơ trên BPM.
*   **WF_03C – Popup import thành công:** Popup hiển thị sau khi hệ thống import thành công các bản ghi hợp lệ vào CRM.

#### 3. Mô tả chi tiết thành phần màn hình

##### 3.1 WF_03 – Giao diện Import danh sách khách hàng
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Tiêu đề màn hình | Label | Text | M | 1 | 100 | Import danh sách khách hàng | Hiển thị tên chức năng đang thao tác |
| 2 | Mô tả màn hình | Label | Text | O | 1 | 255 | Tải file Excel để đưa danh sách khách hàng vào hệ thống CRM | Giải thích mục đích màn hình |
| 3 | Tải mẫu file | Button | - | O | - | - | - | Cho phép người dùng tải file mẫu đúng cấu trúc hệ thống |
| 4 | Khu vực upload file | Upload box | File | M | - | - | Chưa có file | Cho phép kéo thả hoặc chọn file Excel từ máy |
| 5 | File đã chọn | Label/Card | Text | O | 1 | 255 | danh_sach_khach_hang_06_2026.xlsx | Hiển thị tên file người dùng đã chọn |
| 6 | Trường dữ liệu bắt buộc | Chip/Tag | Text | O | 1 | 100 | Họ tên, SĐT, CCCD/CMND, Địa chỉ, Sản phẩm vay, Số tiền vay | Hiển thị danh sách trường bắt buộc trong file import |
| 7 | Quy định import | Card + Text | Text | O | 1 | 500 | - | Mô tả các điều kiện kiểm tra file trước khi import |
| 8 | Hủy | Button | - | O | - | - | - | Hủy thao tác import và quay lại màn trước |
| 9 | Kiểm tra file | Button | - | M | - | - | - | Gửi file lên hệ thống để kiểm tra định dạng, trường bắt buộc và dữ liệu |
| 10 | Import | Button | - | M | - | - | - | Thực hiện import các bản ghi hợp lệ vào CRM |

##### 3.2 WF_03A – Lỗi kiểm tra file
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Tiêu đề lỗi | Label | Text | M | 1 | 100 | Kiểm tra file thất bại | Thông báo file không đạt điều kiện kiểm tra |
| 2 | Nội dung lỗi | Label | Text | M | 1 | 255 | File chứa dữ liệu không hợp lệ | Giải thích lý do người dùng cần kiểm tra lại file |
| 3 | Bảng lỗi | Table | Text | M | - | - | - | Hiển thị danh sách lỗi theo từng dòng trong file |
| 4 | Dòng | Table column | Number | M | 1 | 999999 | - | Số dòng phát sinh lỗi trong file Excel |
| 5 | Trường dữ liệu | Table column | Text | M | 1 | 100 | - | Tên trường dữ liệu bị lỗi |
| 6 | Giá trị hiện tại | Table column | Text | O | 0 | 255 | - | Giá trị hiện tại trong file import |
| 7 | Nguyên nhân lỗi | Table column | Text | M | 1 | 255 | - | Mô tả nguyên nhân dữ liệu không hợp lệ |
| 8 | Tải báo cáo lỗi | Button | - | O | - | - | - | Tải file báo cáo lỗi do hệ thống sinh ra để đối chiếu |
| 9 | Upload lại | Button | - | M | - | - | - | Cho phép người dùng chọn lại file Excel đã chỉnh sửa |

##### 3.3 WF_03B – Kết quả trùng dữ liệu
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Tiêu đề cảnh báo | Label | Text | M | 1 | 100 | Phát hiện dữ liệu trùng | Thông báo hệ thống phát hiện bản ghi trùng |
| 2 | Tổng bản ghi | Card | Number | M | 0 | 9999999 | 1.000 | Tổng số bản ghi trong file import |
| 3 | Hợp lệ | Card | Number | M | 0 | 9999999 | 920 | Số bản ghi đủ điều kiện import |
| 4 | Trùng dữ liệu | Card | Number | M | 0 | 9999999 | 65 | Số bản ghi trùng dữ liệu hiện có |
| 5 | Lỗi dữ liệu | Card | Number | M | 0 | 9999999 | 15 | Số bản ghi lỗi dữ liệu |
| 6 | Danh sách bản ghi trùng | Table | Text | M | - | - | - | Hiển thị chi tiết các bản ghi bị trùng |
| 7 | Lý do trùng | Table column | Text | M | 1 | 255 | - | Mô tả nguyên nhân trùng: SĐT đã tồn tại, CCCD đã tồn tại, đang có hồ sơ BPM |
| 8 | Tải báo cáo trùng | Button | - | O | - | - | - | Tải danh sách bản ghi trùng để đối chiếu |
| 9 | Import bản ghi hợp lệ | Button | - | M | - | - | - | Chỉ import các bản ghi hợp lệ, loại bỏ bản ghi trùng và lỗi |

##### 3.4 WF_03C – Popup import thành công
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Icon thành công | Icon | - | M | - | - | Check icon | Minh họa trạng thái import thành công |
| 2 | Tiêu đề popup | Label | Text | M | 1 | 100 | Import thành công | Thông báo kết quả xử lý |
| 3 | Nội dung popup | Label | Text | M | 1 | 255 | Hệ thống đã import thành công 920 bản ghi hợp lệ vào CRM | Mô tả kết quả import |
| 4 | Đã import | Card | Number | M | 0 | 9999999 | 920 | Số bản ghi đã được import vào CRM |
| 5 | Trùng dữ liệu | Card | Number | M | 0 | 9999999 | 65 | Số bản ghi trùng đã bị loại |
| 6 | Lỗi dữ liệu | Card | Number | M | 0 | 9999999 | 15 | Số bản ghi lỗi đã bị loại |
| 7 | Tiếp tục import | Button | - | O | - | - | - | Quay lại màn import để tải file khác |
| 8 | Quay về danh sách hồ sơ | Button | - | M | - | - | - | Điều hướng đến màn danh sách hồ sơ |

#### 4. Luồng xử lý (Process Flow)
1. **Truy cập màn Import khách hàng (User):** Admin/Manager mở chức năng Import khách hàng từ sidebar.
2. **Tải mẫu file (User):** Người dùng có thể tải mẫu file Excel nếu chưa có file đúng format.
3. **Chọn file Excel (User):** Người dùng kéo thả hoặc chọn file .xlsx từ máy.
4. **Kiểm tra file (User):** Người dùng bấm “Kiểm tra file” để hệ thống validate dữ liệu.
5. **Validate định dạng file (CRM FE/BE):** Hệ thống kiểm tra định dạng file, dung lượng, cấu trúc cột.
6. **Validate dữ liệu bắt buộc (CRM BE):** Hệ thống kiểm tra các trường bắt buộc: Họ tên, SĐT, CCCD/CMND, Địa chỉ, Sản phẩm vay, Số tiền vay.
7. **Kiểm tra trùng dữ liệu (CRM BE):** Hệ thống kiểm tra trùng SĐT, CCCD/CMND và hồ sơ đang tồn tại trên BPM.
8. **Hiển thị kết quả kiểm tra (CRM FE):** Nếu có lỗi dữ liệu, hiển thị màn lỗi. Nếu có bản ghi trùng, hiển thị màn kết quả trùng. Nếu hợp lệ, cho phép import.
9. **Import bản ghi hợp lệ (User):** Người dùng bấm “Import” hoặc “Import bản ghi hợp lệ”.
10. **Tạo lead trong CRM (CRM BE):** Hệ thống tạo lead/hồ sơ cho các bản ghi hợp lệ.
11. **Hiển thị kết quả thành công (CRM FE):** Hệ thống hiển thị popup import thành công.

#### 5. Logic xử lý chi tiết
*   Hệ thống chỉ cho phép upload file có định dạng `.xlsx`. Dung lượng file tối đa là 10MB.
*   File import phải có đủ các cột bắt buộc: Họ tên khách hàng, Số điện thoại, CCCD/CMND, Địa chỉ, Sản phẩm vay, Số tiền vay.
*   Nếu file sai định dạng hoặc thiếu cột bắt buộc, hệ thống hiển thị màn Lỗi kiểm tra file. Nếu dữ liệu trong file sai định dạng, hệ thống hiển thị danh sách lỗi theo từng dòng.
*   Nếu phát hiện trùng SĐT hoặc CCCD/CMND với dữ liệu hiện có, hệ thống hiển thị màn Kết quả trùng dữ liệu.
*   Nếu khách hàng đang có hồ sơ trên BPM, bản ghi đó không được import để tránh tạo hồ sơ trùng quy trình.
*   Hệ thống chỉ import các bản ghi hợp lệ. Các bản ghi lỗi hoặc trùng dữ liệu sẽ bị loại khỏi kết quả import.
*   Sau khi import thành công, hệ thống hiển thị popup thông báo số bản ghi đã import, số bản ghi trùng và số bản ghi lỗi.

#### 6. Hệ thống API Đặc tả

##### 6.1 API kiểm tra file import
*   **API name:** Validate Import Customer File
*   **Method:** POST | **Endpoint:** `/api/customer-import/validate`
*   **Input:**
    *   `file` (File .xlsx, Max 10MB, M, User upload)
    *   `uploadedBy` (String, 1-50, M, CRM FE)
    *   `uploadTime` (Datetime, M, CRM FE)
*   **Output:**
    *   `status` (Integer, M, CRM BE), `message` (String, 1-255, M, CRM BE)
    *   `totalRecords` (Integer, M), `validRecords` (Integer, M), `duplicateRecords` (Integer, M), `invalidRecords` (Integer, M)
    *   `errorList` (Array, O), `duplicateList` (Array, O)

##### 6.2 API import bản ghi hợp lệ
*   **API name:** Import Valid Customer Records
*   **Method:** POST | **Endpoint:** `/api/customer-import/confirm`
*   **Input:**
    *   `importSessionId` (String, 1-50, M, CRM BE)
    *   `confirmImport` (Boolean, M, User)
    *   `createdBy` (String, 1-50, M, CRM FE)
*   **Output:**
    *   `status` (Integer, M), `message` (String, 1-255, M)
    *   `importedRecords` (Integer, M), `duplicateRecords` (Integer, M), `invalidRecords` (Integer, M)
    *   `createdLeadIds` (Array, O)

#### 7. Chi tiết Use Case (Use Case Detail)
*   **UC ID:** UC_IMPORT_001 | **Tên use case:** Import danh sách khách hàng
*   **Actor:** Admin/Manager
*   **Pre-condition:** Người dùng đã đăng nhập hệ thống và có quyền import danh sách khách hàng.
*   **Post-condition:** Các bản ghi hợp lệ được tạo lead/hồ sơ trên CRM. Các bản ghi lỗi hoặc trùng dữ liệu không được import.
*   **Main flow:** Theo đúng Luồng xử lý tại mục 4.
*   **Alternative flow:**
    *   *AF1 – Người dùng tải mẫu file:* Người dùng bấm Tải mẫu file $\rightarrow$ Hệ thống tải về file mẫu $\rightarrow$ Người dùng nhập dữ liệu và upload lại.
    *   *AF2 – Người dùng hủy thao tác:* Người dùng bấm Hủy $\rightarrow$ Hệ thống dừng thao tác import và không lưu dữ liệu.
*   **Exception flow:**
    *   *EF1 – File sai định dạng:* Upload file không phải .xlsx $\rightarrow$ Hệ thống hiển thị lỗi $\rightarrow$ Chọn lại file.
    *   *EF2 – File thiếu trường bắt buộc:* Phát hiện thiếu cột bắt buộc $\rightarrow$ Hiển thị màn Lỗi kiểm tra file $\rightarrow$ Sửa trên máy và upload lại.
    *   *EF3 – Dữ liệu trong file không hợp lệ:* Phát hiện dữ liệu sai định dạng $\rightarrow$ Hiển thị bảng lỗi theo dòng $\rightarrow$ Tải báo cáo lỗi $\rightarrow$ Sửa và upload lại.
    *   *EF4 – Có bản ghi trùng dữ liệu:* Phát hiện trùng SĐT/CCCD hoặc hồ sơ BPM $\rightarrow$ Hiển thị màn Kết quả trùng dữ liệu $\rightarrow$ Tải báo cáo trùng $\rightarrow$ Bấm Import bản ghi hợp lệ để đi tiếp.

#### 8. Business Rules (Quy tắc nghiệp vụ)
*   **BR_IMPORT_001:** Hệ thống chỉ cho phép upload file định dạng .xlsx.
*   **BR_IMPORT_002:** Dung lượng file import tối đa là 10MB.
*   **BR_IMPORT_003:** File import phải có đủ các trường bắt buộc: Họ tên khách hàng, SĐT, CCCD/CMND, Địa chỉ, Sản phẩm vay, Số tiền vay.
*   **BR_IMPORT_004:** Số điện thoại không được để trống và phải đúng định dạng số điện thoại.
*   **BR_IMPORT_005:** CCCD/CMND không được để trống và phải đúng độ dài theo quy định.
*   **BR_IMPORT_006:** Số tiền vay phải là dữ liệu dạng số.
*   **BR_IMPORT_007:** Nếu SĐT hoặc CCCD/CMND đã tồn tại trên CRM, bản ghi được đánh dấu là trùng dữ liệu.
*   **BR_IMPORT_008:** Nếu khách hàng đang có hồ sơ trên BPM, hệ thống không import bản ghi đó.
*   **BR_IMPORT_009:** Chỉ các bản ghi hợp lệ mới được import vào CRM.
*   **BR_IMPORT_010:** Sau khi import thành công, hệ thống hiển thị tổng số bản ghi đã import, bản ghi trùng và bản ghi lỗi.

---

### 📂 Phân hệ FS_02: Quản lý chi tiết hồ sơ khách hàng

#### 1. Mục tiêu tính năng
Tính năng Quản lý chi tiết hồ sơ khách hàng cho phép người dùng theo dõi danh sách hồ sơ vay, tìm kiếm/lọc hồ sơ theo trạng thái, xem thông tin chi tiết từng khách hàng và cập nhật thông tin xử lý hồ sơ. Tính năng này giúp thay thế việc theo dõi hồ sơ thủ công bằng Excel, hỗ trợ Telesale và quản lý nắm được trạng thái xử lý hiện tại của từng hồ sơ theo thời gian gần thực tế.

#### 2. Giao diện màn hình (UI References)
*   **WF_02 – Danh sách hồ sơ khách hàng:** Màn hình hiển thị danh sách hồ sơ khách hàng trên CRM, cho phép người dùng tìm kiếm, lọc dữ liệu, xem trạng thái hồ sơ và mở màn hình chi tiết hồ sơ.
*   **WF_04 – Chi tiết hồ sơ khách hàng:** Màn hình hiển thị toàn bộ thông tin chi tiết của một hồ sơ, gồm thông tin khách hàng, khoản vay, kết quả gọi, thông tin Courier, hồ sơ đính kèm, lịch sử trạng thái và thao tác xử lý hồ sơ.

#### 3. Mô tả chi tiết thành phần màn hình

##### 3.1 WF_02 – Danh sách hồ sơ khách hàng
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Tiêu đề màn hình | Label | Text | M | 1 | 100 | Danh sách hồ sơ | Hiển thị tên màn hình |
| 2 | Mô tả màn hình | Label | Text | O | 1 | 255 | Theo dõi trạng thái xử lý hồ sơ vay theo từng khách hàng | Giải thích mục đích màn hình |
| 3 | Tìm kiếm | Textbox | Text | O | 0 | 100 | Mã hồ sơ, tên khách hàng, SĐT | Cho phép tìm kiếm hồ sơ theo từ khóa |
| 4 | Trạng thái hồ sơ | Dropdown single-select | Text | O | - | - | Tất cả trạng thái | Lọc danh sách theo một trạng thái hồ sơ |
| 5 | Nhóm phụ trách | Dropdown single-select | Text | O | - | - | Tất cả nhóm | Lọc hồ sơ theo nhóm Telesale |
| 6 | Telesale | Textbox/Dropdown | Text | O | 0 | 50 | - | Lọc hồ sơ theo mã hoặc tên Telesale phụ trách |
| 7 | Ngày cập nhật | Date picker | Date | O | - | - | - | Lọc hồ sơ theo ngày cập nhật cuối |
| 8 | Lọc dữ liệu | Button | - | O | - | - | - | Thực hiện lọc danh sách theo điều kiện đã chọn |
| 9 | Xuất file | Button | - | O | - | - | - | Xuất danh sách hồ sơ theo điều kiện lọc |
| 10 | Import danh sách khách hàng | Button | - | O | - | - | - | Điều hướng sang màn Import khách hàng |
| 11 | Bảng danh sách hồ sơ | Table | - | M | - | - | - | Hiển thị danh sách hồ sơ khách hàng |
| 12 | Mã hồ sơ | Table column | Text | M | 1 | 50 | - | Mã định danh duy nhất của hồ sơ |
| 13 | Tên khách hàng | Table column | Text | M | 1 | 100 | - | Tên khách hàng trong hồ sơ vay |
| 14 | Số điện thoại | Table column | Text | M | 10 | 15 | - | Số điện thoại khách hàng |
| 15 | CCCD/CMND | Table column | Text | M | 9 | 12 | - | Số giấy tờ định danh |
| 16 | Sản phẩm vay | Table column | Text | M | 1 | 100 | - | Loại sản phẩm vay khách hàng quan tâm |
| 17 | Số tiền vay | Table column | Number/Currency | M | 0 | - | - | Số tiền vay dự kiến |
| 18 | Telesale phụ trách | Table column | Text | M | 1 | 50 | - | Người phụ trách xử lý hồ sơ |
| 19 | Trạng thái hồ sơ | Badge | Text | M | - | - | Mới phân bổ | Hiển thị trạng thái hiện tại của hồ sơ |
| 20 | Cập nhật cuối | Table column | Datetime | M | - | - | - | Thời điểm cập nhật hồ sơ gần nhất |
| 21 | Thao tác | Button/Hyperlink | - | M | - | - | Chi tiết | Mở màn hình chi tiết hồ sơ |

##### 3.2 WF_04 – Chi tiết hồ sơ khách hàng
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Tiêu đề màn hình | Label | Text | M | 1 | 100 | Chi tiết hồ sơ khách hàng | Hiển thị tên màn hình |
| 2 | Mã hồ sơ | Label | Text | M | 1 | 50 | HS001 | Mã định danh hồ sơ |
| 3 | Tên khách hàng | Label/Textbox | Text | M | 1 | 100 | Nguyễn Văn A | Tên khách hàng |
| 4 | Số điện thoại | Label/Textbox | Text | M | 10 | 15 | 0901234567 | Số điện thoại liên hệ |
| 5 | Trạng thái hiện tại | Badge/Dropdown | Text | M | - | - | Đã chuyển Courier | Trạng thái xử lý hiện tại của hồ sơ |
| 6 | Telesale phụ trách | Label/Dropdown | Text | M | 1 | 50 | TS001 | Người xử lý hồ sơ |
| 7 | Cập nhật cuối | Label | Datetime | M | - | - | 06/06/2026 09:30 | Thời điểm cập nhật gần nhất |
| 8 | Thông tin khách hàng | Card | - | M | - | - | - | Khu vực hiển thị thông tin định danh |
| 9 | CCCD/CMND | Textbox | Text | M | 9 | 12 | - | Số giấy tờ định danh khách hàng |
| 10 | Ngày sinh | Date picker | Date | O | - | - | - | Ngày sinh khách hàng |
| 11 | Địa chỉ | Textbox/Textarea | Text | M | 1 | 255 | - | Địa chỉ khách hàng |
| 12 | Khu vực | Dropdown | Text | M | 1 | 100 | - | Khu vực thu hồ sơ/phân tuyến Courier |
| 13 | Thông tin khoản vay | Card | - | M | - | - | - | Khu vực hiển thị thông tin khoản vay |
| 14 | Sản phẩm vay | Dropdown | Text | M | 1 | 100 | Vay tiền mặt | Sản phẩm vay khách hàng quan tâm |
| 15 | Số tiền vay | Textbox | Number/Currency | M | 0 | - | 30.000.000 | Số tiền vay dự kiến |
| 16 | Thời hạn vay | Dropdown/Textbox | Number | O | 1 | 60 | - | Thời hạn vay theo tháng |
| 17 | Thu nhập hàng tháng | Textbox | Number/Currency | O | 0 | - | - | Thu nhập dự kiến của khách hàng |
| 18 | Mục đích vay | Textarea | Text | O | 0 | 255 | - | Mục đích sử dụng khoản vay |
| 19 | Kết quả gọi | Card | - | M | - | - | - | Khu vực cập nhật kết quả liên hệ |
| 20 | Kết quả cuộc gọi | Dropdown | Text | M | - | - | Đồng ý vay | Kết quả liên hệ gần nhất |
| 21 | Ghi chú cuộc gọi | Textarea | Text | O | 0 | 500 | - | Ghi chú của Telesale |
| 22 | Ngày gọi gần nhất | Datetime picker | Datetime | O | - | - | - | Thời điểm gọi gần nhất |
| 23 | Lịch hẹn gọi lại | Datetime picker | Datetime | O | - | - | - | Thời điểm hẹn gọi lại |
| 24 | Người cập nhật | Label | Text | O | 1 | 50 | TS001 | Người cập nhật kết quả gọi |
| 25 | Thông tin Courier | Card | O | - | - | - | - | Khu vực theo dõi thu hồ sơ giấy |
| 26 | Trạng thái Courier | Badge/Dropdown | Text | O | - | - | Đang chờ thu hồ sơ | Trạng thái xử lý của Courier |
| 27 | Courier phụ trách | Dropdown/Label | Text | O | 1 | 50 | Phạm Văn B | Nhân sự Courier phụ trách |
| 28 | Địa chỉ thu hồ sơ | Textarea | Text | O | 1 | 255 | - | Địa chỉ Courier đến thu hồ sơ |
| 29 | Ngày hẹn thu hồ sơ | Datetime picker | Datetime | O | - | - | - | Lịch hẹn thu hồ sơ |
| 30 | Ghi chú cho Courier | Textarea | Text | O | 0 | 500 | - | Ghi chú chuyển cho Courier |
| 31 | Hồ sơ đính kèm | Card/List | File | O | - | - | - | Danh sách file/giấy tờ liên quan |
| 32 | Lịch sử trạng thái | Timeline | Text/Datetime | M | - | - | - | Hiển thị lịch sử thay đổi trạng thái hồ sơ |
| 33 | Thao tác xử lý hồ sơ | Dropdown single-select | Text | O | - | - | Chọn thao tác cần thực hiện | Người dùng chọn thao tác xử lý tiếp theo |
| 34 | Xác nhận | Button | - | O | - | - | - | Xác nhận thực hiện thao tác đã chọn |
| 35 | Lưu thay đổi | Button | - | M | - | - | - | Lưu các thông tin đã chỉnh sửa |

#### 4. Luồng xử lý (Process Flow)
1. **Mở danh sách:** Người dùng mở chức năng Danh sách hồ sơ từ sidebar $\rightarrow$ Nhập điều kiện tìm kiếm/lọc $\rightarrow$ Bấm “Lọc dữ liệu”.
2. **Truy vấn & Hiển thị:** Hệ thống truy vấn lấy dữ liệu phù hợp điều kiện lọc hiển thị lên bảng.
3. **Mở chi tiết:** Người dùng bấm “Chi tiết” tại một dòng hồ sơ $\rightarrow$ Hệ thống lấy dữ liệu chi tiết hiển thị lên màn hình WF_04.
4. **Cập nhật dữ liệu:** Người dùng chỉnh sửa thông tin hoặc chọn thao tác xử lý $\rightarrow$ Bấm “Lưu thay đổi” hoặc “Xác nhận”.
5. **Hệ thống xử lý:** Hệ thống validate dữ liệu bắt buộc và điều kiện xử lý $\rightarrow$ Nếu hợp lệ, cập nhật dữ liệu vào DB và hiển thị trạng thái mới/thông báo thành công.

#### 5. Logic xử lý chi tiết
*   **Phân quyền dữ liệu:** Admin/Manager xem toàn bộ hồ sơ; Teamlead xem hồ sơ của nhóm phụ trách; Telesale chỉ xem và xử lý hồ sơ được gán cho mình.
*   Cột trạng thái trong bảng chỉ hiển thị badge trạng thái, không cho sửa trực tiếp trên bảng. Mọi thay đổi trạng thái phải được thực hiện tại màn Chi tiết hồ sơ hoặc qua thao tác xử lý nghiệp vụ được cho phép.
*   Khi người dùng bấm “Lưu thay đổi” hoặc chọn “Thao tác xử lý hồ sơ” + bấm “Xác nhận”, hệ thống phải kiểm tra điều kiện logic (Business Rules). Nếu thao tác không hợp lệ với trạng thái hiện tại, hiển thị thông báo lỗi và chặn cập nhật.
*   Mọi thay đổi trạng thái phải được ghi nhận vào lịch sử trạng thái (Status History Timeline).
*   **Điều kiện cứng:** Hồ sơ đã hủy không được phép chuyển Courier hoặc gửi BPM. Hồ sơ chưa có trạng thái “Đồng ý vay” không được phép chuyển Courier. Hồ sơ chưa có trạng thái Courier là "Thu hồ sơ thành công" không được phép gửi sang hệ thống BPM.

#### 6. Hệ thống API Đặc tả

##### 6.1 API lấy danh sách hồ sơ
*   **Method:** GET | **Endpoint:** `/api/cases`
*   **Input:** `keyword` (O), `status` (O), `teamId` (O), `telesaleId` (O), `updatedDate` (O), `page` (M), `pageSize` (M)
*   **Output:** `status`, `message`, `totalRecords`, `caseList` (Mã hồ sơ, Tên khách hàng, SĐT, CCCD, Sản phẩm vay, Số tiền vay, Telesale phụ trách, Trạng thái hồ sơ, Thời gian cập nhật cuối)

##### 6.2 API lấy chi tiết hồ sơ
*   **Method:** GET | **Endpoint:** `/api/cases/{caseId}`
*   **Input:** `caseId` (M), `userId` (M)
*   **Output:** `status`, `message`, `caseDetail` (customerInfo, loanInfo, callResult, courierInfo, attachments, statusHistory)

##### 6.3 API cập nhật hồ sơ
*   **Method:** PUT | **Endpoint:** `/api/cases/{caseId}`
*   **Input:** `caseId` (M), `updatedBy` (M), `customerInfo` (O), `loanInfo` (O), `callResult` (O), `selectedAction` (O), `note` (O)
*   **Output:** `status`, `message`, `updatedCaseStatus`, `lastUpdated`

#### 7. Chi tiết Use Case (Use Case Detail)
*   **UC ID:** UC_CASE_001 | **Tên use case:** Quản lý chi tiết hồ sơ khách hàng
*   **Actor:** Admin/Manager, Teamlead, Telesale
*   **Pre-condition:** Người dùng đã đăng nhập CRM và có quyền xem/xử lý hồ sơ.
*   **Post-condition:** Hồ sơ được hiển thị/cập nhật thành công; lịch sử trạng thái được ghi nhận nếu có thay đổi trạng thái.
*   **Main flow:** Đúng theo Luồng xử lý tại mục 4.
*   **Alternative flow:**
    *   *AF1 – Người dùng xuất danh sách hồ sơ:* Chọn bộ lọc $\rightarrow$ Bấm Xuất file $\rightarrow$ Hệ thống xuất file Excel danh sách hồ sơ phù hợp.
    *   *AF2 – Chọn thao tác xử lý hồ sơ:* Chọn thao tác trong dropdown $\rightarrow$ Bấm Xác nhận $\rightarrow$ Hệ thống check điều kiện hợp lệ $\rightarrow$ Cập nhật trạng thái mới + ghi log timeline.
*   **Exception flow:**
    *   *EF1 – Không tìm thấy hồ sơ:* Nhập từ khóa không có kết quả $\rightarrow$ Hệ thống hiển thị trống dữ liệu (No data).
    *   *EF2 – Không có quyền xem hồ sơ:* Mở hồ sơ ngoài phân quyền $\rightarrow$ Hệ thống từ chối truy cập và báo lỗi.
    *   *EF3 – Thiếu thông tin bắt buộc khi lưu:* Bỏ trống trường bắt buộc $\rightarrow$ Bấm Lưu $\rightarrow$ Báo lỗi và giữ nguyên dữ liệu cũ.
    *   *EF4 – Thao tác xử lý không hợp lệ với trạng thái hiện tại:* Chọn hành động sai logic trạng thái $\rightarrow$ Bấm Xác nhận $\rightarrow$ Hệ thống báo lỗi và chặn cập nhật.

#### 8. Business Rules (Quy tắc nghiệp vụ)
*   **BR_CASE_001:** Người dùng chỉ được xem hồ sơ trong phạm vi phân quyền.
*   **BR_CASE_002:** Admin/Manager được xem toàn bộ hồ sơ trong phạm vi quản lý.
*   **BR_CASE_003:** Teamlead được xem hồ sơ của nhóm phụ trách.
*   **BR_CASE_004:** Telesale chỉ được xem và xử lý hồ sơ được phân cho mình.
*   **BR_CASE_005:** Mỗi hồ sơ chỉ có một trạng thái hiện tại tại một thời điểm.
*   **BR_CASE_006:** Trạng thái trong bảng danh sách chỉ hiển thị dưới dạng badge, không cho sửa trực tiếp tại bảng.
*   **BR_CASE_007:** Mọi thay đổi trạng thái phải được ghi nhận vào lịch sử trạng thái.
*   **BR_CASE_008:** Hồ sơ đã hủy không được chuyển Courier hoặc gửi BPM.
*   **BR_CASE_009:** Hồ sơ chưa có trạng thái “Đồng ý vay” không được chuyển Courier.
*   **BR_CASE_010:** Hồ sơ chưa thu hồ sơ thành công từ Courier không được gửi BPM.
*   **BR_CASE_011:** Các trường bắt buộc như họ tên, số điện thoại, CCCD/CMND, địa chỉ, sản phẩm vay và số tiền vay không được để trống.
*   **BR_CASE_012:** Khi cập nhật kết quả gọi, hệ thống phải ghi nhận người cập nhật và thời gian cập nhật.

---

### 📂 Phân hệ FS_03: Chuyển hồ sơ sang Courier

#### 1. Mục tiêu tính năng
Tính năng Chuyển hồ sơ sang Courier cho phép Telesale/Admin chuyển hồ sơ khách hàng đã đồng ý vay sang Courier để tiến hành thu hồ sơ giấy. Tính năng này giúp chuẩn hóa quá trình bàn giao hồ sơ từ Telesale sang Courier, giảm tình trạng chuyển thông tin thủ công qua Excel/chat, đồng thời hỗ trợ theo dõi trạng thái thu hồ sơ theo thời gian gần thực tế.

#### 2. Giao diện màn hình (UI References)
*   **WF_05 – Popup chuyển hồ sơ sang Courier:** Popup hiển thị khi người dùng chọn thao tác Chuyển Courier từ màn Chi tiết hồ sơ. Người dùng kiểm tra thông tin khách hàng, địa chỉ thu hồ sơ, Courier phụ trách, ngày hẹn thu và danh sách hồ sơ cần thu trước khi xác nhận.
*   **WF_05A – Popup chuyển Courier thành công:** Popup hiển thị sau khi hệ thống chuyển hồ sơ sang Courier thành công và cập nhật trạng thái hồ sơ thành Đã chuyển Courier.
*   **WF_05B – Popup chuyển Courier thất bại:** Popup hiển thị khi hệ thống phát hiện hồ sơ chưa đủ điều kiện chuyển Courier, ví dụ thiếu địa chỉ thu hồ sơ, thiếu số điện thoại hoặc chưa chọn Courier phụ trách.
*   **WF_06 – Theo dõi Courier:** Màn hình cho phép Admin/Manager/Teamlead theo dõi các hồ sơ đã chuyển sang Courier, lọc theo trạng thái Courier, khu vực, Courier phụ trách và ngày hẹn thu hồ sơ.

#### 3. Mô tả chi tiết thành phần màn hình

##### 3.1 WF_05 – Popup chuyển hồ sơ sang Courier
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Tiêu đề popup | Label | Text | M | 1 | 100 | Chuyển hồ sơ sang Courier | Hiển thị tên thao tác |
| 2 | Mô tả popup | Label | Text | O | 1 | 255 | Kiểm tra thông tin thu hồ sơ trước khi chuyển cho Courier phụ trách | Giải thích mục đích popup |
| 3 | Mã hồ sơ | Label | Text | M | 1 | 50 | HS001 | Mã định danh hồ sơ cần chuyển |
| 4 | Tên khách hàng | Label | Text | M | 1 | 100 | Nguyễn Văn A | Tên khách hàng |
| 5 | Số điện thoại | Label/Textbox | Text | M | 10 | 15 | 0901234567 | Số điện thoại liên hệ khách hàng |
| 6 | Địa chỉ thu hồ sơ | Textarea | Text | M | 1 | 255 | 123 Đường ABC... | Địa chỉ Courier đến thu hồ sơ |
| 7 | Khu vực | Dropdown/Label | Text | M | 1 | 100 | Quận 1, TP. HCM | Khu vực phục vụ phân tuyến Courier |
| 8 | Courier phụ trách | Dropdown single-select | Text | M | 1 | 100 | Phạm Văn B | Courier được phân công thu hồ sơ |
| 9 | Ngày hẹn thu hồ sơ | Datetime picker | Datetime | M | - | - | 07/06/2026 14:00 | Thời gian hẹn thu hồ sơ |
| 10 | Ghi chú cho Courier | Textarea | Text | O | 0 | 500 | Gọi trước 30 phút | Ghi chú hỗ trợ Courier khi liên hệ khách hàng |
| 11 | Hồ sơ cần thu | Checklist | Boolean/Text | M | - | - | - | Danh sách giấy tờ Courier cần thu |
| 12 | CCCD/CMND bản sao | Checkbox | Boolean | O | - | - | Unchecked | Loại giấy tờ cần thu |
| 13 | Giấy tờ chứng minh thu nhập | Checkbox | Boolean | O | - | - | Unchecked | Loại giấy tờ cần thu |
| 14 | Ảnh xác nhận khách hàng | Checkbox | Boolean | O | - | - | Unchecked | Loại giấy tờ cần thu |
| 15 | Biểu mẫu vay đã ký | Checkbox | Boolean | O | - | - | Unchecked | Loại giấy tờ cần thu |
| 16 | Cảnh báo thay đổi trạng thái | Label/Alert | Text | O | 1 | 255 | Sau khi xác nhận, trạng thái hồ sơ sẽ được cập nhật thành “Đã chuyển Courier” | Nhắc người dùng về tác động sau xác nhận |
| 17 | Hủy | Button | - | O | - | - | - | Đóng popup, không chuyển hồ sơ |
| 18 | Xác nhận chuyển Courier | Button | - | M | - | - | - | Xác nhận chuyển hồ sơ sang Courier |

##### 3.2 WF_05A – Popup chuyển Courier thành công
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Icon thành công | Icon | - | M | - | - | Check icon | Minh họa trạng thái thành công |
| 2 | Tiêu đề popup | Label | Text | M | 1 | 100 | Chuyển Courier thành công | Thông báo kết quả chuyển hồ sơ |
| 3 | Nội dung popup | Label | Text | M | 1 | 255 | Hồ sơ HS001 đã được chuyển cho Courier Phạm Văn B | Mô tả kết quả xử lý |
| 4 | Mã hồ sơ | Label | Text | M | 1 | 50 | HS001 | Mã hồ sơ đã chuyển |
| 5 | Khách hàng | Label | Text | M | 1 | 100 | Nguyễn Văn A | Tên khách hàng |
| 6 | Courier phụ trách | Label | Text | M | 1 | 100 | Phạm Văn B | Courier được phân công |
| 7 | Ngày hẹn thu hồ sơ | Label | Datetime | M | - | - | 07/06/2026 14:00 | Thời gian hẹn thu hồ sơ |
| 8 | Quay về chi tiết hồ sơ | Button | - | O | - | - | - | Quay lại màn Chi tiết hồ sơ |
| 9 | Theo dõi Courier | Button | - | M | - | - | - | Điều hướng sang màn Theo dõi Courier |

##### 3.3 WF_05B – Popup chuyển Courier thất bại
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Icon lỗi | Icon | - | M | - | - | Warning/Error icon | Minh họa trạng thái lỗi |
| 2 | Tiêu đề popup | Label | Text | M | 1 | 100 | Chuyển Courier thất bại | Thông báo thao tác không thành công |
| 3 | Nội dung lỗi | Label | Text | M | 1 | 255 | Không thể chuyển hồ sơ HS001 sang Courier vì còn thiếu thông tin khách hàng | Mô tả nguyên nhân lỗi |
| 4 | Danh sách lỗi | List | Text | M | - | - | - | Hiển thị các điều kiện chưa đạt |
| 5 | Thiếu địa chỉ thu hồ sơ | List item | Text | O | 1 | 255 | - | Một nguyên nhân lỗi có thể phát sinh |
| 6 | Chưa chọn Courier phụ trách | List item | Text | O | 1 | 255 | - | Một nguyên nhân lỗi có thể phát sinh |
| 7 | Thiếu số điện thoại khách hàng | List item | Text | O | 1 | 255 | - | Một nguyên nhân lỗi có thể phát sinh |
| 8 | Chưa xác nhận đủ hồ sơ cần thu | List item | Text | O | 1 | 255 | - | Một nguyên nhân lỗi có thể phát sinh |
| 9 | Đóng | Button | - | O | - | - | - | Đóng popup |
| 10 | Quay lại chỉnh thông tin | Button | - | M | - | - | - | Quay lại màn Chi tiết hồ sơ để bổ sung thông tin |

##### 3.4 WF_06 – Theo dõi Courier
| No | Hạng mục | Kiểu điều khiển | Kiểu dữ liệu | Bắt buộc | Độ dài min | Độ dài max | Giá trị khởi tạo | Mô tả |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Tiêu đề màn hình | Label | Text | M | 1 | 100 | Theo dõi Courier | Hiển thị tên màn hình |
| 2 | Mô tả màn hình | Label | Text | O | 1 | 255 | Theo dõi tình trạng thu hồ sơ giấy từ khách hàng | Giải thích mục đích màn hình |
| 3 | Tìm kiếm | Textbox | Text | O | 0 | 100 | Mã hồ sơ, tên khách hàng, SĐT | Tìm kiếm hồ sơ Courier |
| 4 | Trạng thái Courier | Dropdown single-select | Text | O | - | - | Tất cả trạng thái | Lọc theo trạng thái Courier |
| 5 | Courier phụ trách | Dropdown/Textbox | Text | O | 0 | 100 | - | Lọc theo Courier phụ trách |
| 6 | Khu vực | Dropdown | Text | O | 0 | 100 | - | Lọc theo khu vực thu hồ sơ |
| 7 | Ngày hẹn thu hồ sơ | Date picker | Date | O | - | - | - | Lọc theo ngày hẹn thu hồ sơ |
| 8 | Lọc dữ liệu | Button | - | O | - | - | - | Áp dụng bộ lọc |
| 9 | Xuất file | Button | - | O | - | - | - | Xuất danh sách hồ sơ Courier |
| 10 | Đã chuyển Courier | Card | Number | M | 0 | 9999991 | 180 | Tổng số hồ sơ đã chuyển Courier |
| 11 | Đang thu hồ sơ | Card | Number | M | 0 | 9999991 | 72 | Số hồ sơ Courier đang xử lý |
| 12 | Thu hồ sơ thành công | Card | Number | M | 0 | 9999991 | 85 | Số hồ sơ thu thành công |
| 13 | Yêu cầu bổ sung | Card | Number | M | 0 | 9999991 | 23 | Số hồ sơ cần bổ sung |
| 14 | Danh sách hồ sơ Courier | Table | - | M | - | - | - | Hiển thị danh sách hồ sơ đã chuyển Courier |
| 15 | Mã hồ sơ | Table column | Text | M | 1 | 50 | - | Mã định danh hồ sơ |
| 16 | Tên khách hàng | Table column | Text | M | 1 | 100 | - | Tên khách hàng |
| 17 | Số điện thoại | Table column | Text | M | 10 | 15 | - | Số điện thoại khách hàng |
| 18 | Địa chỉ thu hồ sơ | Table column | Text | M | 1 | 255 | - | Địa chỉ thu hồ sơ |
| 19 | Courier phụ trách | Table column | Text | M | 1 | 100 | - | Courier xử lý hồ sơ |
| 20 | Ngày hẹn thu | Table column | Datetime | M | - | - | - | Ngày hẹn thu hồ sơ |
| 21 | Trạng thái Courier | Badge | Text | M | - | - | - | Hiển thị trạng thái Courier |
| 22 | Cập nhật cuối | Table column | Datetime | M | - | - | - | Thời điểm Courier cập nhật gần nhất |
| 23 | Thao tác | Button/Hyperlink | - | M | - | - | Chi tiết | Mở chi tiết hồ sơ Courier |
| 24 | Hồ sơ cần chú ý | Card/List | Text | O | - | - | - | Hiển thị nhóm hồ sơ quá hạn, yêu cầu bổ sung hoặc không liên hệ được |

#### 4. Luồng xử lý (Process Flow)
1. **Mở popup bàn giao:** Tại màn Chi tiết hồ sơ, User chọn thao tác "Chuyển Courier" và bấm Xác nhận $\rightarrow$ Hệ thống hiển thị popup WF_05.
2. **Kiểm tra thông tin:** User kiểm tra địa chỉ, chọn Courier phụ trách, chọn ngày hẹn thu và các danh mục giấy tờ cần thu $\rightarrow$ Bấm “Xác nhận chuyển Courier”.
3. **Hệ thống Validate:** Hệ thống kiểm tra điều kiện (trạng thái hồ sơ, địa chỉ, số điện thoại, Courier phụ trách, ngày hẹn thu).
4. **Cập nhật & Lưu vết:** Nếu hợp lệ, hệ thống cập nhật trạng thái hồ sơ tổng thành “Đã chuyển Courier”, đồng thời tự động khởi tạo 1 bản ghi theo dõi nằm trong bảng Courier tracking với trạng thái ban đầu là `Chờ nhận hồ sơ`. Hệ thống bật popup WF_05A thông báo thành công.

#### 5. Logic xử lý chi tiết
*   Chỉ hồ sơ có trạng thái Đồng ý vay mới được chuyển sang Courier. Hồ sơ đã hủy không được chuyển sang Courier.
*   Khi chuyển Courier, hệ thống bắt buộc phải có: Số điện thoại khách hàng, Địa chỉ thu hồ sơ, Khu vực, Courier phụ trách, Ngày hẹn thu hồ sơ. Nếu thiếu thông tin bắt buộc, hệ thống hiển thị popup Chuyển Courier thất bại (`WF_05B`).
*   Courier tiến hành xử lý thực địa và cập nhật kết quả:
    *   Thu hồ sơ thành công $\rightarrow$ Trạng thái Courier chuyển thành `Thu hồ sơ thành công`.
    *   Thiếu giấy tờ $\rightarrow$ Trạng thái Courier chuyển thành `Yêu cầu bổ sung`.
    *   Không liên hệ được khách hàng $\rightarrow$ Trạng thái Courier chuyển thành `Không liên hệ được`.
    *   Khách hủy lịch thu hồ sơ $\rightarrow$ Trạng thái Courier chuyển thành `Khách hủy thu hồ sơ`.
*   Tất cả thay đổi trạng thái Courier phải ghi nhận rõ ID tài khoản người cập nhật và thời gian cập nhật. Hồ sơ chỉ được phép gửi sang hệ thống BPM sau khi Courier đạt trạng thái `Thu hồ sơ thành công` và dữ liệu hồ sơ đầy đủ.

#### 6. Hệ thống API Đặc tả

##### 6.1 API chuyển hồ sơ sang Courier
*   **Method:** POST | **Endpoint:** `/api/cases/{caseId}/transfer-courier`
*   **Input:** `caseId` (M), `customerName` (M), `phoneNumber` (M), `pickupAddress` (M), `area` (M), `courierId` (M), `appointmentTime` (M), `courierNote` (O), `requiredDocuments` (O), `createdBy` (M)
*   **Output:** `status`, `message`, `caseId`, `courierTrackingId`, `updatedCaseStatus` (Đã chuyển Courier), `courierStatus` (Chờ nhận hồ sơ), `lastUpdated`

##### 6.2 API lấy danh sách hồ sơ Courier
*   **Method:** GET | **Endpoint:** `/api/courier-tracking`
*   **Input:** `keyword` (O), `courierStatus` (O), `courierId` (O), `area` (O), `appointmentDate` (O), `page` (M), `pageSize` (M)
*   **Output:** `status`, `message`, `totalRecords`, `courierCaseList` (Mã hồ sơ, Tên khách hàng, SĐT, Địa chỉ thu hồ sơ, Courier phụ trách, Ngày hẹn thu, Trạng thái Courier, Thời gian cập nhật cuối)

##### 6.3 API cập nhật trạng thái Courier
*   **Method:** PUT | **Endpoint:** `/api/courier-tracking/{courierTrackingId}`
*   **Input:** `courierTrackingId` (M), `courierStatus` (M), `collectedDocuments` (O), `missingDocuments` (O), `note` (O), `updatedBy` (M)
*   **Output:** `status`, `message`, `courierTrackingId`, `updatedCourierStatus`, `updatedCaseStatus`, `lastUpdated`

#### 7. Chi tiết Use Case (Use Case Detail)
*   **UC ID:** UC_COURIER_001 | **Tên use case:** Chuyển hồ sơ sang Courier
*   **Actor:** Telesale, Teamlead, Admin/Manager, Courier
*   **Pre-condition:** Người dùng đã đăng nhập CRM, có quyền xử lý hồ sơ và hồ sơ đủ điều kiện chuyển Courier.
*   **Post-condition:** Hồ sơ được chuyển sang Courier thành công, trạng thái hồ sơ được cập nhật và bản ghi theo dõi Courier được tạo trên hệ thống.
*   **Main flow:** Đúng theo Luồng xử lý tại mục 4.
*   **Alternative flow:**
    *   *AF1 – Hủy thao tác chuyển Courier:* Tại popup WF_05 bấm Hủy $\rightarrow$ Đóng popup, giữ nguyên trạng thái hồ sơ cũ.
    *   *AF2 – Theo dõi danh sách Courier:* Mở màn Theo dõi Courier từ sidebar $\rightarrow$ Nhập điều kiện lọc $\rightarrow$ Bấm Lọc dữ liệu $\rightarrow$ Hiển thị danh sách hồ sơ Courier phù hợp.
*   **Exception flow:**
    *   *EF1 – Thiếu thông tin bắt buộc:* Bấm Xác nhận chuyển Courier $\rightarrow$ Hệ thống phát hiện thiếu SĐT, địa chỉ hoặc Courier phụ trách $\rightarrow$ Hiển thị popup Chuyển Courier thất bại (`WF_05B`) $\rightarrow$ Quay lại chỉnh thông tin.
    *   *EF2 – Hồ sơ chưa đủ điều kiện chuyển Courier:* Chọn chuyển Courier cho hồ sơ chưa đạt trạng thái Đồng ý vay $\rightarrow$ Hệ thống từ chối thao tác và hiển thị thông báo lỗi.
    *   *EF3 – Hồ sơ đã hủy:* Thao tác trên hồ sơ đã hủy $\rightarrow$ Hệ thống chặn không cho phép chuyển Courier.
    *   *EF4 – Courier cập nhật yêu cầu bổ sung:* Courier cập nhật kết quả thu là Yêu cầu bổ sung $\rightarrow$ Hệ thống cập nhật trạng thái Courier $\rightarrow$ Tự động đẩy hồ sơ vào nhóm card "Hồ sơ cần chú ý".

#### 8. Business Rules (Quy tắc nghiệp vụ)
*   **BR_COURIER_001:** Chỉ hồ sơ đủ điều kiện mới được chuyển sang Courier.
*   **BR_COURIER_002:** Hồ sơ đã hủy không được chuyển Courier.
*   **BR_COURIER_003:** Hồ sơ chưa có trạng thái “Đồng ý vay” không được chuyển Courier.
*   **BR_COURIER_004:** Khi chuyển Courier, hệ thống bắt buộc phải có số điện thoại, địa chỉ thu hồ sơ, khu vực, Courier phụ trách và ngày hẹn thu.
*   **BR_COURIER_005:** Sau khi chuyển Courier thành công, trạng thái hồ sơ được cập nhật thành “Đã chuyển Courier”.
*   **BR_COURIER_006:** Hệ thống phải tạo bản ghi Courier tracking sau khi chuyển Courier thành công.
*   **BR_COURIER_007:** Trạng thái Courier phải thuộc danh sách giá trị hợp lệ: Chờ nhận hồ sơ, Đang thu hồ sơ, Thu hồ sơ thành công, Yêu cầu bổ sung, Không liên hệ được, Khách hủy thu hồ sơ.
*   **BR_COURIER_008:** Mọi thay đổi trạng thái Courier phải ghi nhận người cập nhật và thời gian cập nhật.
*   **BR_COURIER_009:** Nếu Courier thu hồ sơ thành công, hồ sơ có thể được chuyển sang bước kiểm tra trước khi gửi BPM.
*   **BR_COURIER_010:** Nếu Courier yêu cầu bổ sung, hồ sơ phải được đưa vào danh sách hồ sơ cần theo dõi.

---

## 3. Danh Sách Đầy Đủ User Stories & Tiêu Chí Nghiệm Thu (Mục 9)

### 3.1 Epic 1: Import danh sách khách hàng
*   **US_IMPORT_001:** Là Admin/Manager, tôi muốn tải mẫu file import để nhập dữ liệu khách hàng đúng cấu trúc hệ thống.
    *   *Acceptance Criteria:* Given người dùng ở màn Import khách hàng, when bấm “Tải mẫu file”, then hệ thống tải về file mẫu đúng định dạng `.xlsx`. (Priority: High)
*   **US_IMPORT_002:** Là Admin/Manager, tôi muốn upload file Excel danh sách khách hàng để đưa dữ liệu vào CRM.
    *   *Acceptance Criteria:* Given người dùng chọn file `.xlsx`, when bấm “Kiểm tra file”, then hệ thống tiếp nhận file và bắt đầu kiểm tra định dạng, dung lượng, cột bắt buộc và dữ liệu. (Priority: High)
*   **US_IMPORT_003:** Là Admin/Manager, tôi muốn hệ thống kiểm tra lỗi dữ liệu trong file để tránh import sai thông tin khách hàng.
    *   *Acceptance Criteria:* Given file có dữ liệu không hợp lệ, when hệ thống kiểm tra file, then màn “Lỗi kiểm tra file” hiển thị danh sách lỗi theo dòng, trường dữ liệu, giá trị hiện tại và nguyên nhân lỗi. (Priority: High)
*   **US_IMPORT_004:** Là Admin/Manager, tôi muốn hệ thống phát hiện dữ liệu trùng để tránh tạo hồ sơ trùng trong CRM hoặc BPM.
    *   *Acceptance Criteria:* Given file có SĐT/CCCD trùng hoặc khách đang có hồ sơ BPM, when kiểm tra file, then hệ thống hiển thị màn “Kết quả trùng dữ liệu” và danh sách bản ghi trùng. (Priority: High)
*   **US_IMPORT_005:** Là Admin/Manager, tôi muốn chỉ import các bản ghi hợp lệ để loại bỏ bản ghi lỗi và trùng dữ liệu.
    *   *Acceptance Criteria:* Given file đã được kiểm tra và có bản ghi hợp lệ, when bấm “Import bản ghi hợp lệ”, then hệ thống chỉ tạo lead cho bản ghi hợp lệ và loại bỏ bản ghi lỗi/trùng. (Priority: High)
*   **US_IMPORT_006:** Là Admin/Manager, tôi muốn xem kết quả import sau khi hoàn tất để biết số bản ghi đã được xử lý.
    *   *Acceptance Criteria:* Given import hoàn tất, when hệ thống xử lý xong, then popup “Import thành công” hiển thị số bản ghi đã import, bản ghi trùng và bản ghi lỗi. (Priority: Medium)

### 3.2 Epic 2: Quản lý danh sách và chi tiết hồ sơ
*   **US_CASE_001:** Là Telesale, tôi muốn xem danh sách hồ sơ được phân để biết các khách hàng cần xử lý.
    *   *Acceptance Criteria:* Given Telesale đã đăng nhập, when mở màn Danh sách hồ sơ, then hệ thống hiển thị các hồ sơ thuộc phạm vi được phân quyền. (Priority: High)
*   **US_CASE_002:** Là người dùng CRM, tôi muốn tìm kiếm hồ sơ theo mã hồ sơ, tên khách hàng hoặc số điện thoại để tra cứu nhanh.
    *   *Acceptance Criteria:* Given người dùng nhập từ khóa hợp lệ, when bấm “Lọc dữ liệu”, then hệ thống hiển thị danh sách hồ sơ phù hợp. (Priority: High)
*   **US_CASE_003:** Là Manager/Teamlead, tôi muốn lọc hồ sơ theo trạng thái, nhóm phụ trách, Telesale và ngày cập nhật để theo dõi tiến độ xử lý.
    *   *Acceptance Criteria:* Given người dùng chọn điều kiện lọc, when bấm “Lọc dữ liệu”, then hệ thống trả về danh sách hồ sơ đúng điều kiện. (Priority: High)
*   **US_CASE_004:** Là người dùng CRM, tôi muốn xem trạng thái hồ sơ bằng badge màu để nhận biết nhanh hồ sơ đang ở bước nào.
    *   *Acceptance Criteria:* Given danh sách hồ sơ được hiển thị, then mỗi hồ sơ có một badge trạng thái như Mới phân bổ, Đang xử lý, Đã chuyển Courier, Yêu cầu bổ sung, Đã gửi BPM hoặc Hủy hồ sơ. (Priority: Medium)
*   **US_CASE_005:** Là Telesale, tôi muốn mở chi tiết hồ sơ để xem đầy đủ thông tin khách hàng, khoản vay và lịch sử xử lý.
    *   *Acceptance Criteria:* Given người dùng bấm “Chi tiết” tại một hồ sơ, then hệ thống mở màn Chi tiết hồ sơ khách hàng và hiển thị đầy đủ thông tin liên quan. (Priority: High)
*   **US_CASE_006:** Là Telesale, tôi muốn cập nhật kết quả gọi và ghi chú xử lý để hệ thống lưu lại quá trình tư vấn khách hàng.
    *   *Acceptance Criteria:* Given người dùng nhập kết quả gọi và ghi chú, when bấm “Lưu thay đổi”, then hệ thống cập nhật dữ liệu và ghi nhận người cập nhật, thời gian cập nhật. (Priority: High)
*   **US_CASE_007:** Là người dùng CRM, tôi muốn chọn thao tác xử lý hồ sơ từ dropdown để thực hiện các bước nghiệp vụ tiếp theo.
    *   *Acceptance Criteria:* Given người dùng chọn một thao tác xử lý và bấm “Xác nhận”, then hệ thống kiểm tra điều kiện xử lý trước khi cập nhật trạng thái hồ sơ. (Priority: High)
*   **US_CASE_008:** Là Manager/Teamlead, tôi muốn xem lịch sử trạng thái hồ sơ để biết hồ sơ đã đi qua những bước nào và ai cập nhật.
    *   *Acceptance Criteria:* Given hồ sơ có lịch sử trạng thái, when mở màn Chi tiết hồ sơ, then hệ thống hiển thị timeline gồm thời gian, trạng thái và người thực hiện. (Priority: Medium)

### 3.3 Epic 3: Chuyển hồ sơ sang Courier
*   **US_COURIER_001:** Là Telesale, tôi muốn chuyển hồ sơ khách hàng sang Courier sau khi khách đồng ý vay để Courier thu hồ sơ giấy.
    *   *Acceptance Criteria:* Given hồ sơ đủ điều kiện chuyển Courier, when người dùng chọn thao tác “Chuyển Courier” và xác nhận, then hệ thống mở popup chuyển hồ sơ sang Courier. (Priority: High)
*   **US_COURIER_002:** Là Telesale, tôi muốn kiểm tra thông tin thu hồ sơ trước khi chuyển Courier để tránh chuyển thiếu thông tin.
    *   *Acceptance Criteria:* Given popup chuyển Courier được mở, then hệ thống hiển thị mã hồ sơ, tên khách hàng, SĐT, địa chỉ thu hồ sơ, khu vực, Courier phụ trách, ngày hẹn thu và hồ sơ cần thu. (Priority: High)
*   **US_COURIER_003:** Là người dùng CRM, tôi muốn hệ thống chặn chuyển Courier nếu thiếu thông tin bắt buộc để tránh lỗi vận hành.
    *   *Acceptance Criteria:* Given hồ sơ thiếu SĐT, địa chỉ thu hồ sơ hoặc Courier phụ trách, when bấm “Xác nhận chuyển Courier”, then hệ thống hiển thị popup “Chuyển Courier thất bại”. (Priority: High)
*   **US_COURIER_004:** Là Telesale, tôi muốn nhận thông báo sau khi chuyển Courier thành công để biết hồ sơ đã được bàn giao.
    *   *Acceptance Criteria:* Given hệ thống chuyển Courier thành công, then popup “Chuyển Courier thành công” hiển thị mã hồ sơ, khách hàng, Courier phụ trách và ngày hẹn thu hồ sơ. (Priority: Medium)
*   **US_COURIER_005:** Là Manager/Teamlead, tôi muốn theo dõi danh sách hồ sơ đã chuyển Courier để kiểm soát tiến độ thu hồ sơ giấy.
    *   *Acceptance Criteria:* Given người dùng mở màn Theo dõi Courier, then hệ thống hiển thị danh sách hồ sơ đã chuyển Courier cùng trạng thái thu hồ sơ. (Priority: High)
*   **US_COURIER_006:** Là Manager/Teamlead, tôi muốn lọc hồ sơ Courier theo trạng thái, Courier phụ trách, khu vực và ngày hẹn thu để xử lý các hồ sơ cần chú ý.
    *   *Acceptance Criteria:* Given người dùng chọn bộ lọc Courier, when bấm “Lọc dữ liệu”, then hệ thống hiển thị danh sách hồ sơ Courier phù hợp điều kiện lọc. (Priority: High)
*   **US_COURIER_007:** Là người dùng CRM, tôi muốn các trạng thái Courier hiển thị bằng badge để dễ nhận biết hồ sơ đang chờ nhận, đang thu, thành công hay cần bổ sung.
    *   *Acceptance Criteria:* Given danh sách Courier được hiển thị, then mỗi hồ sơ có badge trạng thái Courier tương ứng. (Priority: Medium)
*   **US_COURIER_008:** Là Manager/Teamlead, tôi muốn xem nhóm hồ sơ cần chú ý để ưu tiên xử lý hồ sơ quá hạn, yêu cầu bổ sung hoặc không liên hệ được.
    *   *Acceptance Criteria:* Given màn Theo dõi Courier được mở, then hệ thống hiển thị card “Hồ sơ cần chú ý” gồm các nhóm cảnh báo quan trọng. (Priority: Medium)

### 3.4 Epic 4: Dashboard và báo cáo
*   **US_REPORT_001:** Là Manager, tôi muốn xem dashboard tổng quan để nắm nhanh tình trạng lead và hồ sơ vay trong ngày.
    *   *Acceptance Criteria:* Given Manager mở Trang chủ, then hệ thống hiển thị KPI tổng lead, lead mới, hồ sơ chuyển Courier, hồ sơ gửi BPM, yêu cầu bổ sung và hồ sơ hủy. (Priority: High)
*   **US_REPORT_002:** Là Manager, tôi muốn xem biểu đồ phân bổ trạng thái hồ sơ để biết hồ sơ đang tập trung ở bước nào.
    *   *Acceptance Criteria:* Given dữ liệu hồ sơ có nhiều trạng thái, then dashboard hiển thị biểu đồ phân bổ trạng thái hồ sơ. (Priority: Medium)
*   **US_REPORT_003:** Là Manager/Teamlead, tôi muốn xem báo cáo xử lý trong ngày theo từng Telesale để đánh giá hiệu suất xử lý.
    *   *Acceptance Criteria:* Given người dùng mở màn Báo cáo xử lý trong ngày, then hệ thống hiển thị bảng báo cáo theo Telesale gồm lead được phân, đã gọi, đồng ý vay, chuyển Courier, gửi BPM, hủy hồ sơ và tỷ lệ chuyển đổi. (Priority: High)
*   **US_REPORT_004:** Là Manager/Teamlead, tôi muốn lọc báo cáo theo ngày, nhóm, Telesale, trạng thái và Courier để phân tích đúng phạm vi cần xem.
    *   *Acceptance Criteria:* Given người dùng chọn điều kiện lọc báo cáo, when bấm “Lọc dữ liệu”, then hệ thống hiển thị số liệu báo cáo đúng điều kiện đã chọn. (Priority: Medium)
*   **US_REPORT_005:** Là Manager, tôi muốn xuất báo cáo để lưu trữ hoặc chia sẻ với các bên liên quan.
    *   *Acceptance Criteria:* Given báo cáo đã được lọc, when bấm “Xuất báo cáo”, then hệ thống xuất file báo cáo theo dữ liệu đang hiển thị. (Priority: Medium)

### 🚀 Ghi chú lộ trình ưu tiên phát triển MVP
| Nhóm chức năng | Mức ưu tiên | Lý do phân bổ |
| :--- | :--- | :--- |
| **Import danh sách khách hàng** | High | Giải quyết trực tiếp bài toán nhập liệu thủ công và chặn dữ liệu lỗi ngay từ cổng vào Excel. |
| **Danh sách hồ sơ & Chi tiết hồ sơ** | High | Trục lõi trung tâm điều phối dữ liệu và tracking trạng thái cho toàn bộ hệ thống. |
| **Chuyển hồ sơ sang Courier** | High | Số hóa quy trình bàn giao hồ sơ giấy, chấm dứt tình trạng thất lạc thông tin qua chat lẻ. |
| **Theo dõi Courier** | Medium | Phục vụ công tác quản trị exception (quá hạn, yêu cầu bổ sung, không liên hệ được khách). |
| **Dashboard/Báo cáo** | Medium | Hỗ trợ cấp quản lý theo dõi hiệu suất tổng quan của dự án để ra quyết định vận hành kịp thời. |
