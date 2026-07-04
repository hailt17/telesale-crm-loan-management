# Từ Điển Dữ Liệu Hệ Thống (Data Dictionary)

## 1. Mục đích
Tài liệu Data Dictionary mô tả chi tiết các nhóm dữ liệu cấu trúc, kiểu dữ liệu, ràng buộc và quy tắc kiểm tra (Validation Rules) được áp dụng xuyên suốt hệ thống CRM quản lý hồ sơ vay Telesale. Đây là cơ sở dữ liệu chung giúp đội ngũ Phân tích nghiệp vụ (BA), Lập trình (Developer) và Kiểm thử (Tester) thống nhất kiến trúc thông tin của sản phẩm trong giai đoạn MVP.

---

## 2. Thực thể: Customer (Thông tin khách hàng)

| Field Name | Tên tiếng Việt | Data Type | Required | Example | Description / Rule |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **customerId** | Mã khách hàng | String | M | KH001 | Mã định danh duy nhất của khách hàng trong hệ thống CRM. |
| **fullName** | Họ tên khách hàng | String | M | Nguyễn Văn A | Không được để trống. |
| **phoneNumber** | Số điện thoại | String | M | 0901234567 | Không được để trống, hệ thống dùng trường này để quét check trùng dữ liệu. |
| **idNumber** | Số CCCD/CMND | String | M | 001201xxxxxx | Không được để trống, hệ thống dùng trường này để quét check trùng dữ liệu. |
| **dateOfBirth** | Ngày sinh | Date | O | 1998-01-01 | Ngày sinh của khách hàng phục vụ kiểm tra điều kiện độ tuổi vay. |
| **address** | Địa chỉ | String | M | 123 Đường ABC, Quận 1 | Địa chỉ liên hệ chi tiết hoặc địa chỉ phục vụ công tác thu hồ sơ giấy. |
| **area** | Khu vực | String | M | Quận 1, TP. HCM | Sử dụng để phân tuyến tự động cho nhân sự Courier thực địa phụ trách. |
| **createdAt** | Ngày tạo | Datetime | M | 2026-06-06 09:30:00 | Thời điểm khách hàng được khởi tạo trên hệ thống CRM. |
| **updatedAt** | Ngày cập nhật | Datetime | M | 2026-06-06 10:30:00 | Thời điểm cập nhật dữ liệu gần nhất của bản ghi khách hàng. |

---

## 3. Thực thể: Case / Lead (Hồ sơ vay)

| Field Name | Tên tiếng Việt | Data Type | Required | Example | Description / Rule |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **caseId** | Mã hồ sơ | String | M | HS001 | Mã định danh duy nhất của một bộ hồ sơ vay trên CRM. |
| **customerId** | Mã khách hàng | String | M | KH001 | Khóa ngoại liên kết trực tiếp với thực thể Customer. |
| **assignedTelesale** | Telesale phụ trách | String | M | TS001 | Mã định danh của nhân viên Telesale chịu trách nhiệm xử lý hồ sơ. |
| **assignedTeam** | Nhóm phụ trách | String | O | Nhóm Telesale 01 | Tên nhóm hoặc phòng ban quản lý hồ sơ để phân quyền báo cáo. |
| **caseStatus** | Trạng thái hồ sơ | String | M | Đã chuyển Courier | Chỉ được phép nhận các giá trị trong danh sách trạng thái hợp lệ. |
| **lastUpdated** | Cập nhật cuối | Datetime | M | 2026-06-06 10:30:00 | Thời điểm cập nhật trạng thái hồ sơ gần nhất. |
| **createdBy** | Người tạo | String | M | Admin01 | Mã định danh của tài khoản thực hiện import hoặc khởi tạo hồ sơ. |
| **createdAt** | Ngày tạo hồ sơ | Datetime | M | 2026-06-06 09:30:00 | Thời điểm bộ hồ sơ vay được khởi tạo hệ thống. |

### Danh sách trạng thái hồ sơ hợp lệ (Case Status Settings)
| Status | Ý nghĩa nghiệp vụ |
| :--- | :--- |
| **Mới phân bổ** | Hồ sơ mới được import vào hệ thống và phân phối tự động cho Telesale nhưng chưa xử lý. |
| **Đang xử lý** | Nhân viên Telesale đang liên hệ cuộc gọi, tư vấn và chăm sóc khách hàng. |
| **Đồng ý vay** | Khách hàng đã hoàn thành tư vấn và đồng ý tiếp tục quy trình thu thập chứng từ giấy. |
| **Đã chuyển Courier** | Hồ sơ đã được duyệt bàn giao thông tin sang cho đội Courier đi thu hồ sơ giấy thực địa. |
| **Yêu cầu bổ sung** | Hồ sơ bị thiếu thông tin hoặc chứng từ giấy cần khách hàng bổ sung gấp để đi tiếp. |
| **Đã gửi BPM** | Hồ sơ đã thu đủ chứng từ hợp lệ và đã đẩy dữ liệu thành công sang hệ thống lõi BPM. |
| **Hủy hồ sơ** | Hồ sơ dừng xử lý hoàn toàn do khách từ chối, không đủ điều kiện hoặc mất liên lạc. |

---

## 4. Thực thể: Loan Info (Thông tin khoản vay)

| Field Name | Tên tiếng Việt | Data Type | Required | Example | Description / Rule |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **loanInfoId** | Mã thông tin khoản vay| String | M | LN001 | Mã định danh duy nhất của bản ghi thông tin khoản vay. |
| **caseId** | Mã hồ sơ | String | M | HS001 | Khóa ngoại liên kết trực tiếp với thực thể Case/Lead. |
| **loanProduct** | Sản phẩm vay | String | M | Vay tiền mặt | Tên sản phẩm tín dụng khách hàng đang quan tâm đăng ký. |
| **loanAmount** | Số tiền vay | Number | M | 30000000 | Bắt buộc phải là kiểu dữ liệu số, giá trị lớn hơn 0. |
| **loanTerm** | Thời hạn vay | Number | O | 24 | Thời hạn vay tính theo đơn vị tháng. |
| **monthlyIncome** | Thu nhập hàng tháng | Number | O | 15000000 | Phải là số, dùng làm căn cứ tính toán phê duyệt điều kiện vay sơ bộ. |
| **loanPurpose** | Mục đích vay | String | O | Vay tiêu dùng | Ghi chú mục đích sử dụng khoản vốn vay của khách hàng. |

---

## 5. Thực thể: Call Result (Kết quả cuộc gọi Telesale)

| Field Name | Tên tiếng Việt | Data Type | Required | Example | Description / Rule |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **callResultId** | Mã kết quả gọi | String | M | CALL001 | Mã định danh duy nhất của bản ghi lịch sử cuộc gọi. |
| **caseId** | Mã hồ sơ | String | M | HS001 | Khóa ngoại liên kết trực tiếp với thực thể Case/Lead. |
| **callStatus** | Kết quả cuộc gọi | String | M | Đồng ý vay | Kết quả ghi nhận cuộc gọi liên hệ gần nhất của nhân viên. |
| **callNote** | Ghi chú cuộc gọi | String | O | Khách hẹn thu hồ sơ | Chi tiết thông tin cuộc trao đổi hoặc ghi chú nội bộ của Telesale. |
| **lastCallTime** | Ngày gọi gần nhất | Datetime | O | 2026-06-06 10:15:00| Thời điểm thực hiện cuộc gọi gần nhất. |
| **callbackTime** | Lịch hẹn gọi lại | Datetime | O | 2026-06-06 16:00:00| Lịch hẹn liên hệ lại tự động hiển thị cảnh báo cho Telesale. |
| **updatedBy** | Người cập nhật | String | M | TS001 | Mã tài khoản nhân sự thực hiện cuộc gọi và cập nhật kết quả. |
| **updatedAt** | Ngày cập nhật | Datetime | M | 2026-06-06 10:20:00| Thời điểm hệ thống ghi nhận cập nhật kết quả gọi gần nhất. |

### Danh sách trạng thái kết quả cuộc gọi gợi ý (Call Status Settings)
| Call Status | Ý nghĩa nghiệp vụ |
| :--- | :--- |
| **Chưa gọi** | Hồ sơ lead mới nhận, chưa được thực hiện bất kỳ cuộc gọi liên hệ nào. |
| **Không nghe máy** | Đổ chuông nhưng khách hàng không bắt máy hoặc thuê bao không thể liên lạc. |
| **Hẹn gọi lại** | Khách hàng bận, yêu cầu nhân viên Telesale chủ động gọi lại vào khung giờ khác. |
| **Đang tư vấn** | Đang trong quá trình trao đổi, giải thích về sản phẩm và gói vay cho khách hàng. |
| **Đồng ý vay** | Khách hàng chốt tham gia gói vay và đồng ý cung cấp thông tin thực địa cho Courier. |
| **Từ chối vay** | Khách hàng chủ động từ chối, báo không có nhu cầu vay vốn tín dụng nữa. |

---

## 6. Thực thể: Courier Tracking (Theo dõi thực địa Courier)

| Field Name | Tên tiếng Việt | Data Type | Required | Example | Description / Rule |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **courierTrackingId**| Mã theo dõi Courier | String | M | CR001 | Mã định danh duy nhất của bản ghi giám sát tiến độ thực địa Courier. |
| **caseId** | Mã hồ sơ | String | M | HS001 | Khóa ngoại liên kết trực tiếp với thực thể Case/Lead. |
| **courierId** | Mã Courier | String | M | C001 | Mã tài khoản định danh của nhân sự Courier phụ trách đi thu hồ sơ. |
| **courierName** | Tên Courier | String | M | Phạm Văn B | Họ tên của nhân sự giao nhận thực địa. |
| **pickupAddress** | Địa chỉ thu hồ sơ | String | M | 123 Đường ABC, Quận 1 | Địa chỉ cụ thể gán cho Courier di chuyển đến để thu hồ sơ giấy. |
| **area** | Khu vực | String | M | Quận 1, TP. HCM | Khu vực hành chính dùng để phân tuyến Courier. |
| **appointmentTime** | Ngày hẹn thu hồ sơ | Datetime | M | 2026-07-07 14:00:00| Lịch hẹn gặp mặt khách hàng ngoài thực địa để làm việc. |
| **courierStatus** | Trạng thái Courier | String | M | Đang thu hồ sơ | Chỉ được phép nhận các giá trị trong danh sách trạng thái Courier hợp lệ. |
| **courierNote** | Ghi chú cho Courier | String | O | Gọi trước 30 phút | Thông tin lưu ý phối hợp từ Telesale chuyển giao sang cho Courier. |
| **lastUpdated** | Cập nhật cuối | Datetime | M | 2026-07-07 10:30:00| Thời điểm cập nhật trạng thái Courier thực địa gần nhất. |

### Danh sách trạng thái Courier hợp lệ (Courier Status Settings)
| Status | Ý nghĩa vận hành |
| :--- | :--- |
| **Chờ nhận hồ sơ** | Hồ sơ bàn giao sang phân hệ Courier thành công nhưng nhân sự chưa bấm nhận việc. |
| **Đang thu hồ sơ** | Courier đã nhận việc, đang chủ động liên hệ hẹn lịch hoặc di chuyển đến điểm hẹn. |
| **Thu hồ sơ thành công**| Courier đã gặp mặt trực tiếp khách hàng, đối chiếu và thu đủ bộ chứng từ giấy hợp lệ. |
| **Yêu cầu bổ sung** | Quá trình kiểm tra thực địa phát hiện khách cung cấp thiếu hoặc sai giấy tờ, cần làm việc lại. |
| **Không liên hệ được** | Courier đến điểm hẹn hoặc liên hệ nhiều lần theo quy định nhưng khách không phản hồi. |
| **Khách hủy thu hồ sơ**| Khách hàng thay đổi quyết định vào phút chót, báo hủy lịch và dừng quy trình nộp hồ sơ giấy. |

---

## 7. Thực thể: Import Session (Phiên Import file Excel)

| Field Name | Tên tiếng Việt | Data Type | Required | Example | Description / Rule |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **importSessionId** | Mã phiên import | String | M | IMP001 | Mã định danh duy nhất cho mỗi đợt upload file danh sách khách hàng. |
| **fileName** | Tên file | String | M | ds_khach_hang_06.xlsx| Tên tệp tin gốc do người dùng tải lên hệ thống. |
| **uploadedBy** | Người upload | String | M | Admin01 | Mã tài khoản nhân sự thực hiện thao tác tải file. |
| **uploadedAt** | Thời gian upload | Datetime | M | 2026-06-06 09:00:00| Thời điểm hệ thống tiếp nhận tệp tin từ Client. |
| **totalRecords** | Tổng bản ghi | Number | M | 1000 | Tổng số dòng dữ liệu chứa trong tệp tin import (không tính dòng tiêu đề). |
| **validRecords** | Bản ghi hợp lệ | Number | M | 920 | Số lượng dòng dữ liệu đạt chuẩn định dạng và nghiệp vụ, sẵn sàng tạo lead. |
| **duplicateRecords** | Bản ghi trùng | Number | M | 65 | Số lượng dòng bị quét trùng thông tin hệ thống nội bộ hoặc BPM. |
| **invalidRecords** | Bản ghi lỗi | Number | M | 15 | Số lượng dòng bị lỗi định dạng hoặc khuyết trường thông tin bắt buộc. |
| **importStatus** | Trạng thái import | String | M | Completed | Trạng thái xử lý vòng đời của phiên import file. |

### Danh sách trạng thái phiên Import hợp lệ (Import Status Settings)
| Status | Ý nghĩa hệ thống |
| :--- | :--- |
| **Uploaded** | Tệp tin tải lên server thành công, hệ thống bắt đầu xếp hàng chờ xử lý phân tích. |
| **Validating** | Hệ thống đang chạy ngầm các hàm kiểm tra validate định dạng cấu trúc dữ liệu và check trùng. |
| **Validation Failed** | File kiểm tra xong và phát hiện có lỗi cấu trúc dữ liệu không hợp lệ. |
| **Duplicate Found** | File kiểm tra xong và phát hiện có chứa dữ liệu trùng lặp số điện thoại hoặc số CCCD. |
| **Completed** | Người dùng xác nhận import, hệ thống đã tạo thành công toàn bộ Lead hợp lệ vào CRM. |
| **Cancelled** | Người dùng chủ động nhấn nút Hủy thao tác sau khi xem báo cáo kết quả kiểm tra file. |

---

## 8. Thực thể: Import Error Detail (Chi tiết dòng dữ liệu lỗi Import)

| Field Name | Tên tiếng Việt | Data Type | Required | Example | Description / Rule |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **errorId** | Mã lỗi | String | M | ERR001 | Mã định danh duy nhất của dòng log ghi nhận bản ghi lỗi. |
| **importSessionId** | Mã phiên import | String | M | IMP001 | Khóa ngoại liên kết trực tiếp với thực thể Import Session. |
| **rowNumber** | Dòng lỗi | Number | M | 8 | Vị trí chính xác số thứ tự dòng phát sinh lỗi trong tệp file Excel gốc. |
| **fieldName** | Trường dữ liệu | String | M | Số tiền vay | Tên cột/trường thông tin chứa dữ liệu không hợp lệ. |
| **currentValue** | Giá trị hiện tại | String | O | abc | Giá trị lỗi thực tế đang nằm trong ô dữ liệu của file. |
| **errorReason** | Nguyên nhân lỗi | String | M | Phải là số | Mô tả chi tiết lý do hệ thống từ chối duyệt dữ liệu dòng này. |
| **suggestion** | Gợi ý xử lý | String | O | Nhập số tiền dạng số | Hướng dẫn định biên định dạng để người dùng chỉnh sửa file trên máy. |

---

## 9. Thực thể: Status History (Lịch sử trạng thái hồ sơ)

| Field Name | Tên tiếng Việt | Data Type | Required | Example | Description / Rule |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **historyId** | Mã lịch sử | String | M | HIS001 | Mã định danh duy nhất của dòng log lịch sử luân chuyển trạng thái. |
| **caseId** | Mã hồ sơ | String | M | HS001 | Khóa ngoại liên kết trực tiếp với thực thể Case/Lead. |
| **oldStatus** | Trạng thái cũ | String | O | Đồng ý vay | Trạng thái của hồ sơ ngay trước thời điểm thực hiện hành động cập nhật. |
| **newStatus** | Trạng thái mới | String | M | Đã chuyển Courier | Trạng thái mới được hệ thống ghi nhận sau khi thực hiện hành động. |
| **updatedBy** | Người cập nhật | String | M | TS001 | Mã tài khoản nhân sự hoặc định danh hệ thống thực hiện lệnh chuyển đổi. |
| **updatedAt** | Thời gian cập nhật | Datetime | M | 2026-06-06 11:30:00| Timestamp chính xác thời điểm hệ thống lưu vết hành động. |
| **note** | Ghi chú | String | O | Chuyển hồ sơ sang Courier| Ghi chú nghiệp vụ đi kèm khi thực hiện thay đổi trạng thái. |

---

## 10. Mối quan hệ dữ liệu chính (Data Relationships Architecture)

Hệ thống kiến trúc cơ sở dữ liệu của CRM vận hành dựa trên các mối quan hệ ràng buộc khóa ngoại (Foreign Key Constraints) chặt chẽ sau:
*   **Customer - Case (1:N):** Một khách hàng trong vòng đời có thể phát sinh nhiều hồ sơ vay (Cases) ở các giai đoạn thời gian khác nhau, nhưng một hồ sơ vay tại một thời điểm chỉ thuộc về duy nhất một khách hàng (`customerId`).
*   **Case - Loan Info (1:1):** Mỗi một hồ sơ vay đăng ký trên hệ thống chỉ liên kết tương ứng với một bản ghi đặc tả chi tiết gói sản phẩm và số tiền vay (`caseId`).
*   **Case - Call Result (1:N):** Một hồ sơ vay trong giai đoạn tư vấn sẽ được nhân viên Telesale thực hiện cuộc gọi nhiều lần, tạo ra nhiều bản ghi lịch sử kết quả gọi (`caseId`). Bản ghi có `lastCallTime` lớn nhất sẽ đại diện cho kết quả cuộc gọi gần nhất.
*   **Case - Courier Tracking (1:1):** Tại một phiên xử lý nghiệp vụ, một hồ sơ vay khi chuyển giao sang thực địa chỉ liên kết với duy nhất một bản ghi giám sát tiến độ thu thập chứng từ giấy của Courier (`caseId`).
*   **Case - Status History (1:N):** Một hồ sơ vay trong suốt vòng đời của mình sẽ đi qua nhiều bước luân chuyển trạng thái khác nhau, hệ thống tự động sinh ra chuỗi các dòng log lịch sử liên kết để phục vụ công tác audit truy vết (`caseId`).
*   **Import Session - Import Error Detail (1:N):** Một đợt import file từ người dùng nếu có lỗi sẽ chứa danh sách chi tiết nhiều dòng log lỗi thành phần để đối chiếu xuất báo cáo (`importSessionId`).
