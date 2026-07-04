# Tài Liệu Đặc Tả Yêu Cầu Chức Năng & Danh Sách User Stories (SRS)

## 1. Sơ Đồ Ca Sử Dụng Tổng Quan (Use Case Diagram)

Sơ đồ Use Case xác định rõ ràng phạm vi hệ thống CRM, các điểm chạm chức năng trong giai đoạn MVP và quyền hạn truy cập của từng đối tượng tham gia vận hành.

### 1.1 Các Actor tham gia hệ thống
*   **Admin/Manager:** Quản lý toàn bộ phễu dữ liệu đầu vào, cấu hình người dùng và giám sát chỉ số vận hành cấp cao.
*   **Teamlead:** Điều phối trực tiếp đội ngũ Telesale, kiểm tra tiến độ và xử lý các ca tắc nghẽn hồ sơ.
*   **Telesale:** Lực lượng lõi thực hiện tiếp cận khách hàng, tư vấn khoản vay và cập nhật thông tin lên CRM.
*   **Courier:** Đội ngũ thực địa tiếp nhận thông tin bàn giao để thu thập và thẩm định chứng từ giấy.
*   **BPM System:** Hệ thống core xét duyệt khoản vay phía sau, kết nối nhận dữ liệu tự động từ CRM.

### 1.2 Các phân hệ chức năng chính trong MVP
*   Import danh sách khách hàng & Tự động Validation.
*   Quản lý danh sách và Chi tiết hồ sơ vay tập trung.
*   Điều phối, bàn giao và Theo dõi tiến độ Courier thực địa.
*   Hệ thống Dashboard giám sát và Báo cáo năng suất Realtime.

![Sơ đồ Use Case Diagram](../assets/usecase-diagram.png)

---

## 2. Ma Trận User Stories & Tiêu Chí Nghiệm Thu (Product Backlog)

### 2.1 Phân hệ: Import danh sách khách hàng
| ID | User Story | Priority | Tiêu chí nghiệm thu (Acceptance Criteria) |
| :--- | :--- | :--- | :--- |
| **US_IMPORT_001** | Là Admin/Manager, tôi muốn tải mẫu file import để nhập dữ liệu khách hàng đúng cấu trúc hệ thống. | High | Người dùng ở màn Import khách hàng, khi bấm “Tải mẫu file”, hệ thống tải về file mẫu đúng định dạng `.xlsx` cấu trúc chuẩn. |
| **US_IMPORT_002** | Là Admin/Manager, tôi muốn upload file Excel danh sách khách hàng để đưa dữ liệu vào CRM. | High | Khi người dùng chọn file `.xlsx` và bấm “Kiểm tra file”, hệ thống lập tức tiếp nhận file và tự động kiểm tra định dạng, dung lượng, cột bắt buộc và dữ liệu. |
| **US_IMPORT_003** | Là Admin/Manager, tôi muốn hệ thống kiểm tra lỗi dữ liệu trong file để tránh import sai thông tin khách hàng. | High | Trường hợp file chứa dữ liệu không hợp lệ, khi hệ thống kiểm tra xong, màn hình “Lỗi kiểm tra file” phải hiển thị danh sách chi tiết lỗi phân tách theo từng dòng, rõ tên trường dữ liệu, giá trị lỗi và nguyên nhân. |
| **US_IMPORT_004** | Là Admin/Manager, tôi muốn hệ thống phát hiện dữ liệu trùng để tránh tạo hồ sơ trùng trong CRM hoặc BPM. | High | Nếu phát hiện số điện thoại/CCCD đã tồn tại trong CRM hoặc khách hàng đang có hồ sơ xử lý trên BPM, hệ thống sẽ chặn lại và hiển thị danh sách tại màn “Kết quả trùng dữ liệu”. |
| **US_IMPORT_005** | Là Admin/Manager, tôi muốn chỉ import các bản ghi hợp lệ để loại bỏ bản ghi lỗi và trùng dữ liệu. | High | Khi file đã được kiểm tra và phân loại, người dùng bấm “Import bản ghi hợp lệ”, hệ thống chỉ tạo lead cho các bản ghi đạt chuẩn, tự động loại bỏ các dòng lỗi/trùng. |
| **US_IMPORT_006** | Là Admin/Manager, tôi muốn xem kết quả import sau khi hoàn tất để biết số bản ghi đã được xử lý. | Medium | Khi import hoàn tất, popup “Import thành công” hiển thị chính xác số bản ghi đã đưa vào CRM thành công, số bản ghi trùng và số bản ghi lỗi bị loại bỏ để đối chiếu. |

### 2.2 Phân hệ: Quản lý danh sách và chi tiết hồ sơ
| ID | User Story | Priority | Tiêu chí nghiệm thu (Acceptance Criteria) |
| :--- | :--- | :--- | :--- |
| **US_CASE_001** | Là Telesale, tôi muốn xem danh sách hồ sơ được phân để biết các khách hàng cần xử lý. | High | Khi Telesale đăng nhập và mở màn Danh sách hồ sơ, hệ thống chỉ hiển thị các hồ sơ được phân phối trực tiếp cho nhân sự đó hoặc thuộc phạm vi quản lý. |
| **US_CASE_002** | Là người dùng CRM, tôi muốn tìm kiếm hồ sơ theo mã hồ sơ, tên khách hàng hoặc số điện thoại để tra cứu nhanh. | High | Khi nhập từ khóa hợp lệ và bấm “Lọc dữ liệu”, hệ thống trả kết quả hiển thị danh sách hồ sơ khớp điều kiện tìm kiếm trong vòng dưới 2 giây. |
| **US_CASE_003** | Là Manager/Teamlead, tôi muốn lọc hồ sơ theo trạng thái, nhóm phụ trách, Telesale và ngày cập nhật để theo dõi tiến độ xử lý. | High | Khi chọn các bộ lọc tương ứng và bấm “Lọc dữ liệu”, hệ thống phải hiển thị chính xác danh sách hồ sơ thỏa mãn toàn bộ điều kiện lọc. |
| **US_CASE_004** | Là người dùng CRM, tôi muốn xem trạng thái hồ sơ bằng badge màu để nhận biết nhanh hồ sơ đang ở bước nào. | Medium | Giao diện danh sách phải hiển thị rõ trạng thái hồ sơ dạng Badge màu chuẩn: Mới phân bổ, Đang xử lý, Đã chuyển Courier, Yêu cầu bổ sung, Đã gửi BPM, Hủy hồ sơ. |
| **US_CASE_005** | Là Telesale, tôi muốn mở chi tiết hồ sơ để xem đầy đủ thông tin khách hàng, khoản vay và lịch sử xử lý. | High | Khi bấm nút “Chi tiết” tại bất kỳ dòng hồ sơ nào, hệ thống điều hướng sang màn Chi tiết hồ sơ, hiển thị toàn bộ hồ sơ khách hàng, thông tin cuộc gọi và lịch sử. |
| **US_CASE_006** | Là Telesale, tôi muốn cập nhật kết quả gọi và ghi chú xử lý để hệ thống lưu lại quá trình tư vấn khách hàng. | High | Khi nhập kết quả và ghi chú cuộc gọi, bấm “Lưu thay đổi”, hệ thống cập nhật tức thì vào CRM, tự động ghi nhận chính xác ID nhân sự cập nhật và timestamp. |
| **US_CASE_007** | Là người dùng CRM, tôi muốn chọn thao tác xử lý hồ sơ từ dropdown để thực hiện các bước nghiệp vụ tiếp theo. | High | Khi chọn một thao tác xử lý nghiệp vụ từ dropdown và bấm “Xác nhận”, hệ thống phải tự động kiểm tra điều kiện logic (Business Rules) trước khi cho phép chuyển trạng thái. |
| **US_CASE_008** | Là Manager/Teamlead, tôi muốn xem lịch sử trạng thái hồ sơ để biết hồ sơ đã đi qua những bước nào và ai cập nhật. | Medium | Tại màn hình Chi tiết hồ sơ, khu vực lịch sử phải hiển thị dạng timeline trực quan, sắp xếp theo thời gian mới nhất, hiển thị rõ người thực hiện và trạng thái thay đổi. |

### 2.3 Phân hệ: Chuyển hồ sơ sang Courier
| ID | User Story | Priority | Tiêu chí nghiệm thu (Acceptance Criteria) |
| :--- | :--- | :--- | :--- |
| **US_COURIER_001** | Là Telesale, tôi muốn chuyển hồ sơ khách hàng sang Courier sau khi khách đồng ý vay để Courier thu hồ sơ giấy. | High | Khi hồ sơ đạt trạng thái "Đồng ý vay", người dùng chọn thao tác “Chuyển Courier” và xác nhận, hệ thống phải kích hoạt mở popup bàn giao dữ liệu cho Courier. |
| **US_COURIER_002** | Là Telesale, tôi muốn kiểm tra thông tin thu hồ sơ trước khi chuyển Courier để tránh chuyển thiếu thông tin. | High | Giao diện popup chuyển Courier phải hiển thị toàn bộ thông tin kiểm tra: Mã hồ sơ, khách hàng, số điện thoại, địa chỉ thực địa, khu vực, nhân sự Courier và danh mục giấy tờ cần thu. |
| **US_COURIER_003** | Là người dùng CRM, tôi muốn hệ thống chặn chuyển Courier nếu thiếu thông tin bắt buộc để tránh lỗi vận hành. | High | Nếu hồ sơ bị khuyết Số điện thoại, Địa chỉ thu hoặc chưa gán nhân sự Courier phụ trách, khi bấm “Xác nhận”, hệ thống lập tức chặn lại và mở popup “Chuyển Courier thất bại”. |
| **US_COURIER_004** | Là Telesale, tôi muốn nhận thông báo sau khi chuyển Courier thành công để biết hồ sơ đã được bàn giao. | Medium | Khi luồng chuyển đổi dữ liệu thành công, hệ thống hiển thị popup “Chuyển Courier thành công” tóm tắt rõ mã hồ sơ, người nhận và lịch hẹn thu hồ sơ. |
| **US_COURIER_005** | Là Manager/Teamlead, tôi muốn theo dõi danh sách hồ sơ đã chuyển Courier để kiểm soát tiến độ thu hồ sơ giấy. | High | Khi truy cập màn hình "Theo dõi Courier", hệ thống hiển thị bảng danh sách toàn bộ hồ sơ đang phân bổ cho Courier kèm theo trạng thái xử lý thực địa. |
| **US_COURIER_006** | Là Manager/Teamlead, tôi muốn lọc hồ sơ Courier theo trạng thái, Courier phụ trách, khu vực và ngày hẹn thu để xử lý các hồ sơ cần chú ý. | High | Hệ thống trả về chính xác danh sách hồ sơ Courier thỏa mãn các điều kiện lọc khi người dùng tương tác với bộ lọc nâng cao tại màn hình Theo dõi Courier. |
| **US_COURIER_007** | Là người dùng CRM, tôi muốn các trạng thái Courier hiển thị bằng badge để dễ nhận biết hồ sơ đang ở giai đoạn nào. | Medium | Trạng thái của Courier phải hiển thị rõ bằng Badge màu riêng biệt: Chờ nhận hồ sơ, Đang thu hồ sơ, Thu hồ sơ thành công, Yêu cầu bổ sung, Không liên hệ được, Khách hủy thu hồ sơ. |
| **US_COURIER_008** | Là Manager/Teamlead, tôi muốn xem nhóm hồ sơ cần chú ý để ưu tiên xử lý hồ sơ quá hạn, yêu cầu bổ sung hoặc không liên hệ được. | Medium | Giao diện màn hình Theo dõi Courier phải thiết kế riêng cấu trúc card cảnh báo “Hồ sơ cần chú ý” để gom nhóm tự động các hồ sơ Courier bị lỗi vận hành. |

### 2.4 Phân hệ: Dashboard & Báo cáo vận hành
| ID | User Story | Priority | Tiêu chí nghiệm thu (Acceptance Criteria) |
| :--- | :--- | :--- | :--- |
| **US_REPORT_001** | Là Manager, tôi muốn xem dashboard tổng quan để nắm nhanh tình trạng lead và hồ sơ vay trong ngày. | High | Tại trang chủ CRM, hệ thống hiển thị thời gian thực (realtime) các khối chỉ số (KPI Cards) về tổng lead, lead mới, hồ sơ ở Courier, hồ sơ đã sang BPM và lượng hồ sơ lỗi/hủy. |
| **US_REPORT_003** | Là Manager/Teamlead, tôi muốn xem báo cáo xử lý trong ngày theo từng Telesale để đánh giá hiệu suất xử lý. | High | Màn hình Báo cáo hiệu suất hiển thị dạng bảng chi tiết theo từng mã Telesale, thống kê rõ: số lead gán, số cuộc gọi đã thực hiện, tỷ lệ đồng ý vay, số hồ sơ chuyển Courier/BPM và tỷ lệ chuyển đổi. |
| **US_REPORT_005** | Là Manager, tôi muốn xuất báo cáo để lưu trữ hoặc chia sẻ với các bên liên quan. | Medium | Khi bấm nút “Xuất báo cáo”, hệ thống kết xuất chính xác file dữ liệu theo đúng định dạng báo cáo dựa trên bộ lọc đang hiển thị tại màn hình. |

---

## 3. Đặc Tả Chi Tiết Phân Hệ Chức Năng (Functional Specifications)

### 3.1 Phân hệ FS_01: Import danh sách khách hàng từ Excel

#### 3.1.1 Giao diện màn hình & Từ điển thành phần dữ liệu (Data Dictionary)
*   **WF_03 – Màn hình chính Import danh sách khách hàng:** Giao diện cho phép Admin lựa chọn file, tải file cấu trúc mẫu và kích hoạt tiến trình validate dữ liệu đầu vào.
*   **WF_03A – Giao diện hiển thị lỗi kiểm tra file:** Hiển thị chi tiết danh sách lỗi phát sinh định dạng theo cấu trúc bảng dòng dữ liệu để người dùng nhận diện.
*   **WF_03B – Giao diện cảnh báo kết quả trùng dữ liệu:** Hiển thị số liệu phân loại bản ghi đạt chuẩn, bản ghi bị quét trùng SĐT/CCCD hoặc trùng hệ thống ngoài (BPM).
*   **WF_03C – Popup xác nhận Import thành công:** Thông báo kết xuất số lượng dữ liệu đã chính thức tạo thành công lead trên CRM.

##### Bảng đặc tả chi tiết thành phần giao diện (WF_03, WF_03A, WF_03B, WF_03C)
| STT | Tên hạng mục hiển thị | Kiểu điều khiển | Kiểu dữ liệu | Trường Bắt buộc | Giá trị khởi tạo | Mô tả chức năng & Logic xử lý |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Tiêu đề màn hình | Label | Text | M | Import danh sách khách hàng | Hiển thị tiêu đề chức năng chính. |
| 2 | Tải mẫu file | Button | - | O | - | Cho phép người dùng tải file mẫu Excel cấu trúc đạt chuẩn hệ thống. |
| 3 | Khu vực upload file | Upload box | File | M | Chưa có file | Hỗ trợ kéo thả hoặc chọn file `.xlsx` trực tiếp từ máy tính (Tối đa 10MB). |
| 4 | File đã chọn | Label/Card | Text | O | - | Hiển thị chính xác tên file người dùng vừa đăng tải lên hệ thống. |
| 5 | Kiểm tra file | Button | - | M | - | Gửi file lên server kích hoạt luồng validate định dạng, dữ liệu và check trùng. |
| 6 | Bảng danh sách lỗi | Table | Text | M (Khi có lỗi) | - | Bảng hiển thị danh sách lỗi chi tiết: Số dòng lỗi, Tên trường bị lỗi, Giá trị hiện tại, Nguyên nhân lỗi cụ thể. |
| 7 | Tải báo cáo lỗi | Button | - | O | - | Kết xuất file Excel báo cáo lỗi chứa cột nguyên nhân để người dùng đối chiếu sửa đổi. |
| 8 | Thống kê số liệu | Cards | Number | M (Màn trùng) | - | Hiển thị 4 chỉ số tổng: Tổng bản ghi, Số bản ghi hợp lệ, Số trùng dữ liệu, Số lỗi định dạng. |
| 9 | Import bản ghi hợp lệ | Button | - | M | - | Ra lệnh cho hệ thống chỉ tiến hành tạo lead đối với các dòng dữ liệu hợp lệ, loại bỏ các dòng lỗi và dòng trùng. |

#### 3.1.2 Quy tắc xử lý logic (Business Rules)
*   **BR_IMPORT_001:** Chỉ chấp nhận tệp tin có định dạng cấu trúc đuôi mở rộng `.xlsx`.
*   **BR_IMPORT_002:** Dung lượng tệp tin đăng tải tối đa không được vượt quá mốc 10MB.
*   **BR_IMPORT_003:** File dữ liệu bắt buộc phải chứa đầy đủ và chính xác các tiêu đề cột: *Họ tên khách hàng, Số điện thoại, CCCD/CMND, Địa chỉ, Sản phẩm vay, Số tiền vay*. Nếu khuyết bất kỳ cột nào, hệ thống từ chối kiểm tra và báo lỗi cấu trúc file.
*   **BR_IMPORT_004:** Số điện thoại phải là chuỗi số, không để trống và tuân thủ định dạng số điện thoại viễn thông hiện hành.
*   **BR_IMPORT_005:** Số CCCD/CMND bắt buộc tuân thủ đúng độ dài quy định hệ thống định danh pháp lý.
*   **BR_IMPORT_006:** Trường thông tin Số tiền vay bắt buộc phải nằm ở định dạng dữ liệu kiểu số (Numeric).
*   **BR_IMPORT_007:** Nếu trường Số điện thoại hoặc số CCCD/CMND đã tồn tại trùng khớp với bất kỳ bản ghi nào đang có trên CRM, bản ghi trong file import sẽ bị đánh dấu mã lỗi hệ thống là "Trùng dữ liệu".
*   **BR_IMPORT_008:** Trường hợp khách hàng quét dữ liệu phát hiện đang có một hồ sơ vay đang chạy trên hệ thống lõi BPM, CRM sẽ lập tức loại bỏ bản ghi này để ngăn chặn hành vi tạo hồ sơ trùng lặp quy trình xử lý.
*   **BR_IMPORT_009:** Hệ thống nghiêm cấm import tự động các bản ghi bị dán nhãn Lỗi hoặc Trùng. Chỉ duy nhất dữ liệu đạt trạng thái Hợp lệ mới được cấp quyền tạo Lead trên CRM.

#### 3.1.3 Đặc tả hệ thống kỹ thuật (API Specification)

##### API 1: Kiểm tra cấu trúc và validate dữ liệu file import
*   **Method:** `POST`
*   **Endpoint:** `/api/customer-import/validate`
*   **Request Body (Multipart/Form-Data):**
    ```json
    {
      "file": "Binary_Excel_File",
      "uploadedBy": "ADMIN_001",
      "uploadTime": "2026-07-05T00:00:00Z"
    }
    ```
*   **Response Body (200 OK):**
    ```json
    {
      "status": 200,
      "message": "File validated successfully",
      "totalRecords": 1000,
      "validRecords": 920,
      "duplicateRecords": 65,
      "invalidRecords": 15,
      "errorList": [
        { "row": 12, "field": "phoneNumber", "currentValue": "090abc", "reason": "Sai định dạng số điện thoại" }
      ],
      "duplicateList": [
        { "row": 45, "field": "idNumber", "currentValue": "123456789", "reason": "Số CCCD đã tồn tại trên hệ thống CRM" }
      ]
    }
    ```

##### API 2: Xác nhận thực hiện Import bản ghi hợp lệ vào CRM
*   **Method:** `POST`
*   **Endpoint:** `/api/customer-import/confirm`
*   **Request Body:**
    ```json
    {
      "importSessionId": "SESS_20260705_01",
      "confirmImport": true,
      "createdBy": "ADMIN_001"
    }
    ```
*   **Response Body (200 OK):**
    ```json
    {
      "status": 200,
      "message": "Imported 920 valid records successfully",
      "importedRecords": 920,
      "duplicateRecords": 65,
      "invalidRecords": 15,
      "createdLeadIds": ["HS001", "HS002", "HS003"]
    }
    ```

---

### 3.2 Phân hệ FS_02: Quản lý danh sách & Chi tiết hồ sơ khách hàng

#### 3.2.1 Giao diện màn hình & Từ điển thành phần dữ liệu (Data Dictionary)
*   **WF_02 – Màn hình Danh sách hồ sơ khách hàng:** Trung tâm quản lý hiển thị toàn bộ hồ sơ dạng bảng, hỗ trợ các tính năng tìm kiếm, lọc đa điều kiện và xuất dữ liệu.
*   **WF_04 – Màn hình Chi tiết hồ sơ khách hàng:** Khu vực hiển thị toàn diện 360 độ về thông tin khách hàng, chi tiết gói vay, lịch sử cuộc gọi Telesale, tiến độ phân bổ Courier và trục timeline lịch sử trạng thái hồ sơ.

##### Bảng đặc tả chi tiết thành phần giao diện Chi tiết hồ sơ (WF_04)
| STT | Tên hạng mục hiển thị | Kiểu điều khiển | Kiểu dữ liệu | Trường Bắt buộc | Giá trị hiển thị mẫu | Mô tả chức năng & Logic xử lý |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Mã hồ sơ | Label | Text | M | HS001 | Mã định danh duy nhất của hồ sơ (Chỉ xem). |
| 2 | Trạng thái hiện tại | Badge | Text | M | Đã chuyển Courier | Badge hiển thị trạng thái hồ sơ trên CRM. |
| 3 | CCCD/CMND | Textbox | Text | M | 001095001234 | Số định danh của khách hàng (Cho phép sửa nếu có quyền). |
| 4 | Địa chỉ khách hàng | Textarea | Text | M | 123 Đường ABC, Quận 1 | Địa chỉ cư trú phục vụ xác minh thông tin. |
| 5 | Khu vực | Dropdown | Text | M | Quận 1, TP. HCM | Khu vực phục vụ bài toán phân tuyến Courier tự động. |
| 6 | Số tiền vay | Textbox | Currency | M | 30.000.000 | Số tiền vay đăng ký (Định dạng đơn vị tiền tệ). |
| 7 | Kết quả cuộc gọi | Dropdown | Text | M | Đồng ý vay | Kết quả cuộc gọi gần nhất của Telesale. |
| 8 | Ghi chú cuộc gọi | Textarea | Text | O | Khách hẹn thu hồ sơ buổi chiều | Thông tin chi tiết cuộc trao đổi của Telesale. |
| 9 | Thao tác xử lý hồ sơ | Dropdown | Text | O | Chọn thao tác | Danh sách các hành động nghiệp vụ tiếp theo (Chuyển Courier, Hủy hồ sơ, Gửi BPM). |
| 10 | Lưu thay đổi | Button | - | M | - | Thực hiện kiểm tra tính toàn vẹn dữ liệu bắt buộc và lưu lại các thông tin chỉnh sửa. |

#### 3.2.2 Quy tắc xử lý logic (Business Rules)
*   **BR_CASE_001 đến BR_CASE_004 (Phân quyền xem dữ liệu):** 
    *   Nhân sự cấp *Telesale* chỉ có quyền tìm kiếm, xem và xử lý các hồ sơ được hệ thống phân bổ trực tiếp cho tài khoản của mình.
    *   Cấp *Teamlead* được quyền xem toàn bộ hồ sơ thuộc nhóm phụ trách xử lý.
    *   Cấp *Admin/Manager* có toàn quyền truy xuất toàn bộ hồ sơ trên toàn hệ thống CRM.
*   **BR_CASE_006:** Nghiêm cấm mọi hành vi can thiệp thay đổi trực tiếp trạng thái hồ sơ ngay tại giao diện Bảng danh sách (`WF_02`). Trạng thái tại bảng danh sách chỉ hiển thị dạng Badge màu tĩnh (Read-only) để phòng tránh lỗi bấm nhầm. Mọi hành động chuyển trạng thái bắt buộc phải xử lý bên trong màn hình Chi tiết hồ sơ (`WF_04`) hoặc qua trigger tự động.
*   **BR_CASE_007:** Bất kỳ hành động thay đổi trạng thái nào của hồ sơ đều phải được hệ thống tự động ghi vết timestamp và ID tài khoản thực hiện vào cấu trúc bảng lịch sử trạng thái (Status History Timeline).
*   **BR_CASE_008:** Nếu hồ sơ đã bị dán nhãn trạng thái là `Hủy hồ sơ`, hệ thống lập tức khóa toàn bộ tính năng chuyển giao Courier hoặc đẩy dữ liệu sang BPM.
*   **BR_CASE_009:** Hệ thống chặn tính năng bàn giao Courier nếu hồ sơ chưa đạt trạng thái ghi nhận là `Đồng ý vay`.
*   **BR_CASE_010:** Hệ thống chặn hoàn toàn hành động chuyển hồ sơ sang `Đã gửi BPM` nếu bộ phận Courier chưa cập nhật trạng thái kết quả thực địa đạt mốc `Thu hồ sơ thành công`.

#### 3.2.3 Đặc tả hệ thống kỹ thuật (API Specification)

##### API: Lấy thông tin chi tiết của một bộ hồ sơ vay
*   **Method:** `GET`
*   **Endpoint:** `/api/cases/{caseId}`
*   **Response Body (200 OK):**
    ```json
    {
      "status": 200,
      "caseId": "HS001",
      "caseStatus": "Đồng ý vay",
      "customerInfo": {
        "customerName": "Nguyễn Văn A",
        "phoneNumber": "0901234567",
        "idNumber": "001095001234",
        "address": "123 Đường ABC, Quận 1",
        "area": "Quận 1, TP. HCM"
      },
      "loanInfo": {
        "loanProduct": "Vay tiền mặt",
        "loanAmount": 30000000,
        "tenor": 24
      },
      "statusHistory": [
        { "status": "Mới phân bổ", "updatedBy": "SYSTEM", "updatedTime": "2026-07-05T01:00:00Z" },
        { "status": "Đang xử lý", "updatedBy": "TS001", "updatedTime": "2026-07-05T02:30:00Z" }
      ]
    }
    ```

---

### 3.3 Phân hệ FS_03: Chuyển hồ sơ sang Courier & Theo dõi tiến độ thực địa

#### 3.3.1 Giao diện màn hình & Từ điển thành phần dữ liệu (Data Dictionary)
*   **WF_05 – Popup thiết lập chuyển hồ sơ sang Courier:** Giao diện kiểm tra thông tin thu thập chứng từ, gán mã nhân sự Courier, lên lịch hẹn thực địa và tích chọn danh mục hồ sơ bắt buộc phải thu thập.
*   **WF_05A / WF_05B – Giao diện kết quả bàn giao:** Hiển thị popup thông báo luồng chuyển đổi dữ liệu thành công hoặc liệt kê danh sách thông tin bị khuyết gây thất bại luồng bàn giao Courier.
*   **WF_06 – Màn hình Theo dõi tiến độ Courier:** Giao diện bảng quản trị chuyên biệt dành cho Admin/Teamlead để quản lý lượng hồ sơ đang lưu thông ngoài thị trường, theo dõi các ca lỗi như quá hạn thu thập hoặc thiếu giấy tờ.

##### Bảng đặc tả chi tiết thành phần giao diện Popup Chuyển Courier (WF_05)
| STT | Tên hạng mục hiển thị | Kiểu điều khiển | Kiểu dữ liệu | Trường Bắt buộc | Giá trị hiển thị mẫu | Mô tả chức năng & Logic xử lý |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Tiêu đề popup | Label | Text | M | Chuyển hồ sơ sang Courier | Hiển thị tên thao tác nghiệp vụ. |
| 2 | Địa chỉ thu hồ sơ | Textarea | Text | M | 123 Đường ABC, Quận 1 | Địa chỉ thực tế mà nhân sự Courier sẽ phải di chuyển đến để gặp khách hàng. |
| 3 | Courier phụ trách | Dropdown | Text | M | Phạm Văn B | Danh sách nhân sự thuộc đội Courier phụ trách khu vực tương ứng để gán việc. |
| 4 | Ngày hẹn thu hồ sơ | Datetime picker | Datetime | M | 2026-07-06 14:00 | Lịch hẹn gặp mặt khách hàng đã chốt qua điện thoại. |
| 5 | Ghi chú cho Courier | Textarea | Text | O | Gọi trước khi đến 30 phút | Các thông tin lưu ý đặc biệt phục vụ Courier xử lý ca thực địa. |
| 6 | Danh sách giấy tờ cần thu| Checklist | Boolean | M | CCCD (Checked), HĐLĐ (Unchecked) | Danh sách danh mục chứng từ giấy bắt buộc Courier phải kiểm tra và thu đủ từ khách hàng. |

#### 3.3.2 Quy tắc xử lý logic (Business Rules)
*   **BR_COURIER_004:** Khi kích hoạt hành động chuyển giao Courier, hệ thống tự động quét kiểm tra dữ liệu bắt buộc (Data Validation). Nếu một trong các trường *Số điện thoại khách hàng, Địa chỉ thu hồ sơ, Khu vực, Courier phụ trách, Ngày hẹn thu hồ sơ* bị khuyết, CRM phải chặn đứng luồng xử lý và xuất giao diện `WF_05B - Chuyển Courier thất bại`.
*   **BR_COURIER_005:** Sau khi luồng xác nhận chuyển Courier thành công, hệ thống tự động đổi trạng thái hồ sơ tổng trên CRM sang mã `Đã chuyển Courier`.
*   **BR_COURIER_006:** Hệ thống phải tự động khởi tạo song song một bản ghi theo dõi tiến độ nằm trong bảng quản trị Courier Tracking (`WF_06`) với trạng thái gốc ban đầu thiết lập mặc định là `Chờ nhận hồ sơ`.
*   **BR_COURIER_007:** Trạng thái tiến độ thực địa của Courier bắt buộc chỉ được luân chuyển đóng khung trong ma trận 6 giá trị: *Chờ nhận hồ sơ, Đang thu hồ sơ, Thu hồ sơ thành công, Yêu cầu bổ sung, Không liên hệ được, Khách hủy thu hồ sơ*.
*   **BR_COURIER_010:** Hệ thống tự động cấu hình bộ lọc quét thông minh, đưa toàn bộ hồ sơ Courier rơi vào trạng thái lỗi như *Quá hạn lịch hẹn, Yêu cầu bổ sung chứng từ, Không liên hệ được khách* vào khu vực quản trị tiêu điểm mang tên **"Hồ sơ cần chú ý"** để Teamlead và Admin can thiệp xử lý khẩn cấp.

#### 3.3.3 Đặc tả hệ thống kỹ thuật (API Specification)

##### API: Thực hiện chuyển giao bộ hồ sơ sang phân hệ Courier Tracking
*   **Method:** `POST`
*   **Endpoint:** `/api/cases/{caseId}/transfer-courier`
*   **Request Body:**
    ```json
    {
      "pickupAddress": "123 Đường ABC, Quận 1",
      "area": "Quận 1, TP. HCM",
      "courierId": "COUR_09",
      "appointmentTime": "2026-07-06T14:00:00Z",
      "courierNote": "Gọi trước khi đến 30 phút",
      "requiredDocuments": ["CCCD_SAO", "CHUNG_MINH_THU_NHAP"]
    }
    ```
*   **Response Body (200 OK):**
    ```json
    {
      "status": 200,
      "message": "Transferred to Courier successfully",
      "caseId": "HS001",
      "courierTrackingId": "TRK_COU_9981",
      "updatedCaseStatus": "Đã chuyển Courier",
      "courierStatus": "Chờ nhận hồ sơ",
      "lastUpdated": "2026-07-05T03:00:00Z"
    }
    ```

---

## 4. Kịch Bản Kiểm Thử Người Dùng Chấp Nhận (UAT Test Scenarios)

Hệ thống kịch bản kiểm thử UAT đảm bảo tính đúng đắn về mặt logic nghiệp vụ của phần mềm trước khi nghiệm thu bàn giao sản phẩm.

| Mã Kịch Bản | Phân hệ chức năng | Mô tả mục tiêu kịch bản kiểm thử | Các bước thực hiện (Test Steps) | Kết quả kỳ vọng đạt tiêu chuẩn (Expected Result) |
| :--- | :--- | :--- | :--- | :--- |
| **TC_IMPORT_001**| Import dữ liệu | Kiểm thử luồng thành công khi file Excel chuẩn định dạng và dữ liệu sạch. | 1. Truy cập màn Import khách hàng.<br>2. Upload file `.xlsx` đạt chuẩn dữ liệu.<br>3. Nhấn Kiểm tra file.<br>4. Nhấn Import bản ghi hợp lệ. | Hệ thống import thành công toàn bộ dữ liệu, tạo Lead trên CRM và hiển thị popup thông báo số lượng chính xác. |
| **TC_IMPORT_003**| Import dữ liệu | Kiểm thử luồng ngoại lệ khi file Excel bị khuyết trường dữ liệu bắt buộc. | 1. Upload file Excel bị xóa cột Số điện thoại.<br>2. Nhấn nút Kiểm tra file. | Hệ thống chặn tiến trình, hiển thị màn hình giao diện báo lỗi cấu trúc file và liệt kê chi tiết cột bị khuyết. |
| **TC_IMPORT_005**| Import dữ liệu | Kiểm thử tính năng quét trùng dữ liệu hệ thống. | 1. Upload file chứa số SĐT đã tồn tại trên CRM.<br>2. Nhấn nút Kiểm tra file. | Hệ thống phát hiện dữ liệu trùng, đưa bản ghi vào bảng danh sách màn hình Kết quả trùng dữ liệu. |
| **TC_CASE_006**  | Quản lý hồ sơ | Kiểm thử tính năng Telesale cập nhật thông tin và kết quả cuộc gọi. | 1. Vào màn hình Chi tiết hồ sơ.<br>2. Chỉnh sửa trường địa chỉ và chọn kết quả "Đồng ý vay".<br>3. Nhấn Lưu thay đổi. | CRM lưu thông tin mới thành công, cập nhật Badge trạng thái, ghi nhận tài khoản thực hiện vào Lịch sử trạng thái. |
| **TC_CASE_008**  | Quản lý hồ sơ | Kiểm thử quy tắc chặn logic nghiệp vụ khi hồ sơ chưa đạt điều kiện. | 1. Vào chi tiết hồ sơ trạng thái "Mới phân bổ".<br>2. Chọn thao tác "Chuyển Courier" từ dropdown.<br>3. Bấm Xác nhận. | Hệ thống tự động chặn hành động, hiển thị thông báo lỗi cảnh báo hồ sơ chưa đạt trạng thái Đồng ý vay. |
| **TC_COURIER_001**| Quản lý Courier| Kiểm thử luồng thành công bàn giao dữ liệu sang cho đội Courier. | 1. Mở chi tiết hồ sơ "Đồng ý vay".<br>2. Chọn thao tác Chuyển Courier.<br>3. Điền địa chỉ, gán Courier, chọn ngày hẹn.<br>4. Bấm Xác nhận. | Hồ sơ chuyển sang trạng thái Đã chuyển Courier, hệ thống sinh mã bản ghi tracking và mở popup thông báo thành công. |
| **TC_COURIER_002**| Quản lý Courier| Kiểm thử luồng ngoại lệ thiếu thông tin vận hành thực địa. | 1. Mở popup bàn giao Courier.<br>2. Để trống ô nhập Địa chỉ thu hồ sơ.<br>3. Bấm Xác nhận chuyển Courier. | Hệ thống kích hoạt chặn thao tác, xuất hiển thị giao diện popup Chuyển Courier thất bại và báo lỗi thiếu địa chỉ. |
| **TC_COURIER_009**| Quản lý Courier| Kiểm thử tính năng cập nhật và cảnh báo hồ sơ Courier lỗi thực địa. | 1. Nhân sự cập nhật trạng thái Courier sang mã "Yêu cầu bổ sung".<br>2. Mở giao diện Theo dõi Courier. | Bản ghi lập tức cập nhật trạng thái, hệ thống tự động đẩy hồ sơ này vào khu vực danh sách "Hồ sơ cần chú ý" trên giao diện. |
