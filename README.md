# CRM Quản Lý Hồ Sơ Vay Qua Telesale

## 🚀 Giới thiệu dự án
Đây là dự án phân tích và thiết kế hệ thống CRM Web App chuyên dụng cho quy trình xử lý hồ sơ vay qua kênh Telesale. Dự án tập trung giải quyết triệt để bài toán tracking trạng thái hồ sơ rời rạc khi dữ liệu khách hàng, kết quả cuộc gọi, đội ngũ Courier và hệ thống BPM đang bị quản lý thủ công bằng Excel.

---

## 🎯 Phạm vi giải pháp (MVP Scope)
Hệ thống tập trung giải quyết 3 nhóm chức năng cốt lõi:
*   **Import dữ liệu:** Import danh sách khách hàng từ file Excel và tự động kiểm tra dữ liệu đầu vào.
*   **Quản lý hồ sơ:** Quản lý, tìm kiếm, phân quyền và tracking trạng thái hồ sơ vay tập trung.
*   **Quản lý Courier:** Chuyển giao hồ sơ sang bộ phận Courier và theo dõi tiến độ thu chứng từ giấy ngoài thực địa.

👉 **[BẢNG QUẢN LÝ TÍNH NĂNG & USER STORIES TRÊN GITHUB PROJECTS](https://github.com/users/hailt17/projects/1/views/1)**

---

## 📊 Tài liệu dự án (Main Deliverables)

| Nhóm tài liệu | Nội dung chi tiết | Link tài liệu |
| :--- | :--- | :--- |
| **Process** | Quy trình nghiệp vụ AS-IS, TO-BE, sơ đồ BPMN | [Xem chi tiết](./docs/01-process.md) |
| **Requirement** | Scope, Use Case Diagram, Danh sách User Stories & AC | [Xem chi tiết](./docs/02-requirement.md) |
| **UI/UX** | Wireframe/UI hoàn chỉnh cho các màn hình chính (Dashboard, Chi tiết hồ sơ) | [Xem Figma/Ảnh](./docs/03-ui-ux.md) |
| **Specification** | Đặc tả chức năng (Functional Spec) cho Import, Quản lý và Courier | [Xem chi tiết](./docs/04-spec.md) |
| **Data** | Từ điển dữ liệu (Data Dictionary) cho Customer, Case, Loan Info, Courier... | [Xem chi tiết](./docs/05-data.md) |
| **Testing** | Kịch bản kiểm thử UAT (UAT Test Scenarios) luồng thành công & ngoại lệ | [Xem chi tiết](./docs/06-testing.md) |

---

## 🧠 Quyết định nghiệp vụ cốt lõi (Key BA Decisions)
Để tạo nên sự khác biệt cho giải pháp, dự án quyết định phân tích dựa trên nỗi đau thực tế của vận hành:
*   **Ưu tiên Web App thay vì Mobile App:** Quyết định chọn CRM Web App làm MVP vì đối tượng chịu ảnh hưởng lớn nhất từ việc lệch trạng thái hồ sơ là Admin, Teamlead và Manager (những người làm việc cố định bằng máy tính). Đội ngũ Courier thực địa sẽ được tối ưu bằng Mobile App ở giai đoạn sau.
*   **Chặn cập nhật trạng thái tại danh sách tổng:** Không cho phép sửa trạng thái trực tiếp tại bảng Danh sách hồ sơ để tránh bấm nhầm. Trạng thái chỉ hiển thị dạng badge màu, việc cập nhật bắt buộc phải thực hiện trong màn hình *Chi tiết hồ sơ* để đảm bảo có đủ ngữ cảnh và ghi nhận lịch sử.
*   **Thiết kế "Báo cáo lỗi" thay vì sửa file:** Khi kiểm tra file Excel Import đầu vào bị lỗi, hệ thống sẽ sinh ra một "Báo cáo lỗi" riêng biệt thay vì can thiệp sửa trực tiếp vào file gốc của người dùng, giúp đảm bảo tính toàn vẹn dữ liệu.
*   **Gom tính năng vào Dropdown "Thao tác":** Để UI màn hình Chi tiết hồ sơ gọn gàng, các nút hành động (Duyệt, Từ chối, Bổ sung) được gom chung vào một Dropdown hành động. Hệ thống sẽ tự động bắt điều kiện trước khi cho phép người dùng kích hoạt các thao tác này.

