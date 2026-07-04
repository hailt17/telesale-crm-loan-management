# Hệ Thống CRM Quản Lý Hồ Sơ Vay Qua Kênh Telesale

## 🚀 Giới thiệu dự án
Dự án tập trung phân tích và thiết kế hệ thống CRM Web App chuyên dụng cho luồng xử lý hồ sơ vay tín dụng qua kênh Telesale. Giải pháp được xây dựng nhằm giải quyết triệt để bài toán quản trị vận hành khi các điểm chạm dữ liệu (thông tin khách hàng, kết quả cuộc gọi, tiến độ đội Courier thực địa và trạng thái đẩy sang core thẩm định BPM) đang bị phân mảnh, rời rạc do quản lý thủ công bằng nhiều file Excel và kênh chat độc lập.

---

## 🎯 Phạm vi giải pháp (MVP Scope)
Hệ thống giai đoạn MVP tập trung giải quyết dứt điểm 3 nhóm phân hệ chức năng cốt lõi:
1. **Import dữ liệu đầu vào:** Thiết lập tính năng tải file Excel danh sách khách hàng tập trung, tự động kiểm tra định dạng, kiểm toán trường bắt buộc và quét check trùng dữ liệu (Validation & Deduplication).
2. **Quản lý hồ sơ tập trung:** Màn hình giám sát, phân quyền khai thác, tìm kiếm và tracking trạng thái vòng đời của một bộ hồ sơ vay theo thời gian thực.
3. **Quản lý Courier thực địa:** Hệ thống hóa luồng giao việc, bàn giao thông tin và giám sát chặt chẽ tiến độ đi thu chứng từ giấy ngoài thị trường của đội ngũ Courier.

---

## 💻 Bảng Quản Lý Tính Năng & User Stories (Agile Project Management)
Toàn bộ quá trình phân rã tính năng, quản lý Product Backlog, thiết lập nhãn độ ưu tiên (Must-have/Should-have) và module hóa User Stories được quản trị trực quan tại bảng GitHub Project của dự án:

👉 **[BẤM VÀO ĐÂY ĐỂ XEM BẢNG QUẢN TRỊ TÍNH NĂNG TRÊN GITHUB PROJECTS](DÁN_LINK_GITHUB_PROJECT_CỦA_BẠN_VÀO_ĐÂY)**

---

## 📊 Tài liệu chi tiết dự án (Main Deliverables)

Hệ thống tài liệu đặc tả được phân rã thành các cấu trúc file chuyên biệt giúp các bộ phận liên quan (Stakeholders, Developers, Testers) dễ dàng truy xuất thông tin:

| Nhóm tài liệu | Nội dung chi tiết | Link tài liệu |
| :--- | :--- | :--- |
| **01. Business Process** | Phân tích sâu quy trình vận hành hiện tại (AS-IS), giải pháp mục tiêu (TO-BE) và hệ thống sơ đồ luồng chuẩn BPMN. | [Xem chi tiết](./docs/01-process.md) |
| **02. System Requirement** | Đặc tả yêu cầu hệ thống (SRS): Sơ đồ Use Case, tài liệu Đặc tả chức năng (Functional Spec), danh sách User Stories & AC kèm thiết kế Wireframe UI/UX chi tiết từ Visily. | [Xem chi tiết](./docs/02-requirement.md) |
| **03. Data Dictionary** | Từ điển dữ liệu chi tiết mô tả cấu trúc, kiểu dữ liệu, ràng buộc khóa ngoại và logic validation cho toàn bộ thực thể hệ thống (Customer, Case, Loan, Call, Courier...). | [Xem chi tiết](./docs/03-data-dictionary.md) |
| **04. UAT Testing** | Hệ thống kịch bản kiểm thử người dùng chấp nhận (UAT Test Scenarios) bao gồm đầy đủ luồng xử lý thành công và ma trận xử lý lỗi ngoại lệ. | [Xem chi tiết](./docs/04-uat-testing.md) |

---

## 🧠 Quyết định nghiệp vụ cốt lõi (Key BA Decisions)

Để tối ưu hóa tài nguyên và đem lại giá trị vận hành thực tế nhanh nhất cho doanh nghiệp, các quyết định phân tích giải pháp được chốt dựa trên việc đào sâu nỗi đau (Pain Points) của hệ thống cũ:

*   **Ưu tiên Web App thay vì Mobile App cho MVP:** Quyết định chọn nền tảng CRM Web App cho giai đoạn đầu vì đối tượng chịu ảnh hưởng nặng nề nhất từ việc lệch pha trạng thái hồ sơ là Admin, Teamlead và Manager (những bộ phận làm việc cố định với máy tính). Đội ngũ Courier di chuyển ngoài thực địa tạm thời được tối ưu qua luồng phân tuyến khu vực và sẽ nâng cấp Mobile App ở giai đoạn sau.
*   **Chặn đứng hành vi cập nhật trạng thái tại danh sách tổng:** Hệ thống không cho phép nhân viên sửa trạng thái trực tiếp trên các dòng của bảng danh sách hồ sơ nhằm triệt tiêu rủi ro bấm nhầm do thao tác nhanh. Trạng thái tại bảng tổng chỉ hiển thị dạng badge màu (Read-only), việc cập nhật trạng thái bắt buộc phải xử lý bên trong màn hình Chi tiết hồ sơ để đảm bảo nhân sự có đủ ngữ cảnh và hệ thống ghi vết lịch sử chính xác.
*   **Thiết kế "Báo cáo lỗi" độc lập khi Import file:** Khi tệp tin Excel tải lên bị lỗi cấu trúc hoặc sai định dạng trường dữ liệu, hệ thống tự động kết xuất ra một "Báo cáo lỗi" chi tiết theo từng dòng thay vì can thiệp sửa đổi trực tiếp trên file gốc của người dùng. Quy định này giúp bảo toàn nguyên vẹn tính toàn vẹn dữ liệu gốc phục vụ công tác đối chiếu ngoại biên.
*   **Tối ưu UI bằng Dropdown "Thao tác hành động":** Để màn hình Chi tiết hồ sơ giữ được sự tinh gọn, trực quan, toàn bộ các nút hành động điều hướng nghiệp vụ (Duyệt chuyển, Từ chối, Yêu cầu bổ sung, Gửi BPM) được gom chung vào một cấu trúc Dropdown duy nhất. Hệ thống sẽ chạy ngầm các hàm kiểm tra điều kiện logic (Business Rules) để tự động hiển thị hoặc ẩn/khóa các hành động không hợp lệ với trạng thái hiện tại của hồ sơ.
