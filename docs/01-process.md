# Tài Liệu Phân Tích Quy Trình Nghiệp Vụ & Giải Pháp CRM

## 1. Quy trình hiện tại (AS-IS Process)

### 1.1 Mô tả quy trình hiện tại
Quy trình vận hành hiện tại chủ yếu dựa trên Excel và các kênh trao đổi thủ công giữa các bộ phận. Danh sách khách hàng được tổng hợp bằng file Excel, sau đó Admin/Manager tiến hành phân phối cho đội ngũ Telesale xử lý. Nhân viên Telesale thực hiện cuộc gọi, tư vấn và cập nhật kết quả. Đối với các khách hàng đồng ý vay, thông tin sẽ được chuyển tiếp cho bộ phận Courier để đi thu hồ sơ giấy ngoài thực địa. Sau khi thu thập đủ, hồ sơ tiếp tục được chuyển giao sang hệ thống BPM để xử lý các bước tiếp theo.

### 1.2 Các bên tham gia trong quy trình hiện tại
| Actor | Vai trò |
| :--- | :--- |
| **Admin/Manager** | Nhận danh sách khách hàng, quản lý file Excel tổng và theo dõi kết quả vận hành chung. |
| **Teamlead** | Theo dõi sát sao nhóm Telesale, thực hiện phân công lead và kiểm tra tiến độ xử lý công việc. |
| **Telesale** | Gọi điện liên hệ khách hàng, tư vấn các gói sản phẩm vay và cập nhật kết quả xử lý lên file. |
| **Courier** | Di chuyển thực địa để thu hồi các chứng từ, hồ sơ giấy từ phía khách hàng. |
| **BPM System** | Hệ thống tiếp nhận các hồ sơ đã đủ điều kiện để thực hiện các bước thẩm định, phê duyệt tiếp theo. |

### 1.3 Luồng nghiệp vụ AS-IS tổng quan
1. Admin/Manager tiếp nhận danh sách khách hàng đầu vào dưới dạng file Excel.
2. Admin/Manager thực hiện phân bổ lead (dữ liệu khách hàng) cho từng nhân viên Telesale.
3. Nhân viên Telesale tiến hành gọi điện và tư vấn chi tiết cho khách hàng.
4. Telesale cập nhật kết quả xử lý một cách thủ công vào file Excel hoặc file theo dõi riêng của cá nhân/nhóm.
5. Khi khách hàng đồng ý vay, Telesale chuyển thông tin phối hợp sang cho bộ phận Courier.
6. Courier liên hệ trực tiếp với khách hàng để hẹn lịch và đi thu hồ sơ giấy.
7. Trường hợp hồ sơ bị thiếu chứng từ, Courier và Telesale phải trao đổi qua lại với nhau để yêu cầu khách hàng bổ sung.
8. Nếu hồ sơ đã đầy đủ, thông tin và chứng từ được chuyển tiếp sang hệ thống BPM.
9. Định kỳ, Manager và Teamlead phải tự tổng hợp báo cáo thủ công từ nhiều nguồn và nhiều file khác nhau.

### 1.4 Vấn đề tồn tại của quy trình AS-IS
Quy trình hiện tại phụ thuộc quá nhiều vào các thao tác thủ công và các công cụ lưu trữ rời rạc. Dữ liệu khách hàng, trạng thái xử lý hồ sơ, kết quả cuộc gọi và tình trạng giao nhận của Courier nằm rải rác ở nhiều file Excel và nhiều kênh chat khác nhau. Sự phân mảnh này dẫn đến việc theo dõi (tracking) trạng thái hồ sơ bị thiếu nhất quán, dễ xảy ra sai sót dữ liệu và gây khó khăn lớn cho công tác kiểm soát vận hành.

---

## 2. Nỗi đau vận hành (Pain Points)

### 2.1 Pain point chính
Nỗi đau lớn nhất và cốt lõi nhất của quy trình hiện tại là **thiếu một hệ thống quản lý tập trung để tracking trạng thái hồ sơ**. 

Do một hồ sơ phải đi qua rất nhiều điểm chạm vận hành (từ import lead, Telesale xử lý, chuyển giao Courier, thu hồ sơ giấy thực địa cho đến khi gửi sang hệ thống BPM) nhưng lại thiếu một công cụ quản trị xuyên suốt, Manager và Teamlead hoàn toàn bị động, không thể nắm bắt được hồ sơ đang kẹt ở bước nào, ai đang chịu trách nhiệm và tiến độ xử lý cụ thể ra sao.

### 2.2 Danh sách Pain Points chi tiết
| Pain Point | Mô tả thực trạng | Ảnh hưởng đến vận hành |
| :--- | :--- | :--- |
| **Quản lý bằng Excel rời rạc** | Dữ liệu khách hàng và trạng thái hồ sơ nằm phân mảnh ở nhiều file khác nhau. | Dễ dẫn đến sai lệch thông tin, nhầm lẫn dữ liệu và cực kỳ khó kiểm soát phiên bản (version) file. |
| **Khó tracking trạng thái** | Không có một màn hình hay công cụ tập trung để tra cứu xem hồ sơ đang dừng ở bước nào. | Ban quản lý (Manager) không thể theo dõi tiến độ công việc để điều phối kịp thời. |
| **Dễ trùng dữ liệu khách hàng** | Thiếu bước tự động kiểm tra trùng số điện thoại hoặc số CCCD/CMND trước khi tạo hồ sơ mới. | Phát sinh tình trạng tạo trùng lead, trùng hồ sơ trên hệ thống, gây lãng phí tài nguyên và trùng chéo khách hàng. |
| **Cập nhật thủ công mất thời gian** | Đội ngũ Telesale và Admin phải tốn nhiều thời gian để nhập liệu và cập nhật dữ liệu qua lại trên nhiều file báo cáo riêng. | Làm tăng khối lượng công việc (workload) không đáng có và rất dễ xảy ra sai sót con người. |
| **Thiếu kiểm soát đội Courier** | Trạng thái thu hồ sơ giấy ngoài thực địa của Courier không được cập nhật tập trung và kịp thời về tổng đài. | Khó phát hiện sớm các hồ sơ bị quá hạn thu thập hoặc các trường hợp khẩn cấp cần bổ sung chứng từ. |
| **Báo cáo không realtime** | Cấp quản lý phải đợi tổng hợp số liệu thủ công từ nhiều nguồn khác nhau vào cuối ngày hoặc cuối tuần. | Thông tin báo cáo bị chậm, không phản ánh đúng thực tế thời điểm hiện tại, gây chậm trễ trong việc ra quyết định vận hành. |
| **Khó audit lịch sử xử lý** | Hệ thống file không lưu lại timeline thay đổi trạng thái một cách rõ ràng. | Khi xảy ra lỗi hoặc thất thoát hồ sơ, rất khó để truy vết xem ai đã cập nhật, cập nhật nội dung gì và vào thời điểm nào. |

### 2.3 Pain Point ưu tiên xử lý trong MVP
Để tối ưu hóa nguồn lực và mang lại giá trị nhanh nhất cho doanh nghiệp, giai đoạn MVP này tập trung giải quyết dứt điểm 3 nỗi đau lớn sau:
1. Tracking trạng thái hồ sơ tập trung xuyên suốt luồng vận hành.
2. Thiết lập tính năng Import danh sách khách hàng gắn liền với bộ lọc kiểm tra dữ liệu đầu vào (Validation).
3. Hệ thống hóa quy trình chuyển giao và theo dõi tiến độ xử lý hồ sơ của đội Courier.

Việc tập trung vào 3 điểm này sẽ giúp doanh nghiệp lập tức lấy lại quyền kiểm soát luồng đi của hồ sơ, kiểm soát chặt chẽ chất lượng dữ liệu đầu vào và nâng cao hiệu suất làm việc của các bên.

---

## 3. Giải pháp mục tiêu (TO-BE Solution)

### 3.1 Giải pháp đề xuất
Xây dựng hệ thống **CRM Web App** đóng vai trò là nền tảng quản trị tập trung độc nhất, quản lý toàn bộ vòng đời của một hồ sơ vay Telesale. 

Hệ thống mới sẽ tự động hóa các khâu từ import danh sách khách hàng, validate dữ liệu, kiểm tra trùng chéo, phân bổ lead thông minh cho Telesale, ghi nhận chi tiết lịch sử cuộc gọi, chuyển giao hồ sơ sang bộ phận Courier, giám sát tiến độ thu chứng từ thực địa cho đến xuất bản hệ thống báo cáo vận hành theo thời gian thực.

### 3.2 Luồng TO-BE tổng quan
1. Admin/Manager thực hiện upload danh sách khách hàng trực tiếp lên hệ thống CRM.
2. CRM tự động kiểm tra định dạng file, kiểm tra các trường thông tin bắt buộc và phát hiện dữ liệu lỗi.
3. CRM tự động quét trùng số điện thoại, số CCCD/CMND với dữ liệu hiện tại trên CRM và kiểm tra trạng thái hồ sơ trên hệ thống BPM.
4. Hệ thống chỉ phê duyệt import đối với các bản ghi hoàn toàn hợp lệ.
5. Lead hợp lệ được phân bổ ngay cho nhân viên Telesale theo quy tắc thiết lập sẵn.
6. Telesale thực hiện cuộc gọi trực tiếp, cập nhật kết quả cuộc gọi và thông tin khoản vay lên màn hình CRM.
7. Khi khách hàng đồng ý vay, hệ thống hỗ trợ chuyển nhanh toàn bộ thông tin sang cho bộ phận Courier.
8. Bộ phận Courier tiếp nhận thông tin, tiến hành thu hồ sơ giấy và cập nhật trạng thái xử lý trực tiếp lên hệ thống.
9. Hồ sơ sau khi tích lũy đủ điều kiện sẽ được đẩy tự động hoặc chuyển giao sang hệ thống BPM.
10. Cấp quản lý (Manager/Teamlead) theo dõi toàn bộ hoạt động vận hành thông qua hệ thống Dashboard và báo cáo Realtime.

### 3.3 Các chức năng chính trong hệ thống TO-BE
| Tên chức năng | Mô tả chi tiết | Giá trị mang lại cho doanh nghiệp |
| :--- | :--- | :--- |
| **Dashboard** | Hiển thị trực quan các chỉ số tổng quan về lượng lead mới, hồ sơ đang ở Courier, hồ sơ đã sang BPM, hồ sơ cần bổ sung chứng từ hoặc đã hủy. | Giúp cấp quản lý nắm bắt toàn diện sức khỏe vận hành của dự án chỉ trong vài giây. |
| **Import khách hàng** | Tính năng upload file Excel tích hợp bộ công cụ validate dữ liệu, check trùng tự động và phân loại bản ghi lỗi. | Loại bỏ hoàn toàn việc nhập liệu thủ công, ngăn chặn dữ liệu rác và dữ liệu trùng lặp ngay từ cửa ngõ. |
| **Danh sách hồ sơ** | Màn hình tìm kiếm, lọc thông tin đa điều kiện và tracking trạng thái động của toàn bộ hồ sơ. | Tạo ra một nguồn dữ liệu tập trung, nhất quán cho toàn bộ các phòng ban. |
| **Chi tiết hồ sơ** | Nơi xem và cập nhật toàn bộ thông tin khách hàng, chi tiết khoản vay, lịch sử cuộc gọi và timeline thay đổi trạng thái. | Chuẩn hóa quy trình làm việc của Telesale, đảm bảo tính minh bạch thông tin. |
| **Chuyển Courier** | Tính năng duyệt và chuyển giao hàng loạt hồ sơ đủ điều kiện sang cho bộ phận Courier thu giấy tờ. | Cắt giảm hoàn toàn các bước bàn giao thủ công bằng file lẻ hoặc chat chit ngoài luồng. |
| **Theo dõi Courier** | Màn hình giám sát chi tiết trạng thái xử lý của Courier, cảnh báo hồ sơ quá hạn hoặc xử lý các ca exception. | Tăng năng lực kiểm soát rủi ro thực địa, giảm tỷ lệ thất thoát hồ sơ giấy. |
| **Báo cáo xử lý** | Hệ thống báo cáo tự động hiển thị năng suất làm việc theo từng nhân sự Telesale, theo nhóm hoặc theo tỷ lệ chuyển đổi trạng thái. | Cung cấp số liệu chính xác để tối ưu hóa quy trình vận hành và đánh giá hiệu suất (KPI). |

### 3.4 Ma trận trạng thái hồ sơ trên CRM
| Trạng thái | Ý nghĩa nghiệp vụ |
| :--- | :--- |
| **Mới phân bổ** | Hồ sơ khách hàng mới được import và phân phối xuống cho nhân viên Telesale nhưng chưa được xử lý. |
| **Đang xử lý** | Nhân viên Telesale đang trong quá trình liên hệ, gọi điện tư vấn hoặc chăm sóc khách hàng. |
| **Đồng ý vay** | Khách hàng đã hoàn thành việc tư vấn và đồng ý tiếp tục các bước tiếp theo của quy trình vay. |
| **Đã chuyển Courier** | Hồ sơ đã được Admin duyệt và chuyển giao thông tin sang cho đội Courier để chuẩn bị đi thu chứng từ giấy. |
| **Yêu cầu bổ sung** | Hồ sơ đang bị kẹt do thiếu thông tin hoặc tài liệu chứng từ giấy từ phía khách hàng, cần bổ sung gấp. |
| **Đã gửi BPM** | Hồ sơ đã hoàn thành việc thu thập chứng từ hợp lệ và đã được đẩy thành công sang hệ thống BPM để thẩm định. |
| **Hủy hồ sơ** | Hồ sơ dừng xử lý hoàn toàn do khách hàng từ chối vay, không đủ điều kiện hoặc không thể liên hệ được sau nhiều lần. |

### 3.5 Ma trận trạng thái xử lý của Courier
| Trạng thái Courier | Ý nghĩa nghiệp vụ |
| :--- | :--- |
| **Chờ nhận hồ sơ** | Hồ sơ đã được CRM chuyển giao sang nhưng nhân viên Courier chưa bấm tiếp nhận để xử lý. |
| **Đang thu hồ sơ** | Nhân viên Courier đang chủ động liên hệ hẹn lịch hoặc đang di chuyển đến gặp khách hàng để lấy chứng từ. |
| **Thu hồ sơ thành công**| Courier đã gặp được khách hàng và kiểm tra thu đủ toàn bộ danh mục hồ sơ giấy theo quy định. |
| **Yêu cầu bổ sung** | Quá trình đi thu gặp vấn đề do khách hàng cung cấp thiếu hoặc sai lệch giấy tờ, cần làm việc lại để bổ sung. |
| **Không liên hệ được** | Courier đã cố gắng liên hệ với khách hàng nhiều lần theo quy định quy trình nhưng không bắt máy hoặc thuê bao. |
| **Khách hủy thu hồ sơ**| Khách hàng thay đổi quyết định, chủ động báo hủy lịch hẹn và không muốn tiếp tục nộp hồ sơ vay nữa. |

### 3.6 Lợi ích kỳ vọng mang lại
*   **Về mặt Vận hành:** Cắt giảm tối đa các thao tác thủ công lặp đi lặp lại, giải phóng doanh nghiệp khỏi sự phụ thuộc vào các file Excel thủ công.
*   **Về mặt Dữ liệu:** Triệt tiêu hoàn toàn các lỗi sai sót do nhập liệu, loại bỏ dữ liệu trùng lặp, đảm bảo tính toàn vẹn và sạch sẽ của kho dữ liệu.
*   **Về mặt Tracking:** Giúp ban quản lý giám sát chặt chẽ luồng đi của từng bộ hồ sơ theo thời gian thực (Realtime), phát hiện và xử lý ngay các điểm nghẽn.
*   **Về mặt Phối hợp:** Gắn kết các bộ phận Telesale, Courier và Quản lý vào chung một màn hình làm việc duy nhất, triệt tiêu việc lệch pha thông tin.
*   **Về mặt Kiểm soát rủi ro:** Hệ thống hóa việc cảnh báo hồ sơ bị ngâm quá hạn, hồ sơ thiếu chứng từ, nâng cao tỷ lệ hồ sơ duyệt thành công.

---

## 4. Sơ đồ quy trình nghiệp vụ (BPMN)

### 4.1 Sơ đồ AS-IS BPMN
Sơ đồ AS-IS BPMN phản ánh chi tiết quy trình xử lý hồ sơ hiện tại khi dữ liệu khách hàng được quản lý thủ công bằng Excel. Sơ đồ chỉ rõ các điểm nghẽn (bottlenecks) lớn như: thiếu cơ chế tracking tập trung, luồng trao đổi thông tin giữa Telesale và Courier bị đứt gãy, và việc quản lý tiến độ thu hồ sơ giấy hoàn toàn nằm ngoài tầm kiểm soát của ban quản lý.

*<img width="1661" height="721" alt="image" src="https://github.com/user-attachments/assets/204a2f66-1525-426c-b4f3-870aea0236ec" />*

### 4.2 Sơ đồ TO-BE BPMN
Sơ đồ TO-BE BPMN chuẩn hóa quy trình sau khi áp dụng giải pháp CRM Web App. Hệ thống CRM đóng vai trò điều phối trung tâm: tự động validate dữ liệu, tự động phân bổ lead, quản lý chặt chẽ ma trận trạng thái hồ sơ, kết nối trực tiếp thông tin sang cho bộ phận Courier và tự động hóa luồng chuyển giao dữ liệu sang hệ thống BPM.

*<img width="2781" height="831" alt="image" src="https://github.com/user-attachments/assets/33248502-5769-4293-b674-c65ebc588b58" />*

### 4.3 Luồng quy trình cấp cao (TO-BE High-Level Process)
Sơ đồ quy trình cấp cao tóm tắt luồng đi cốt lõi của một hồ sơ trên hệ thống mới ở mức tổng quan nhất. Giúp các bên liên quan (Stakeholders) và đội ngũ phát triển (Developers) nhanh chóng nắm bắt được kiến trúc vận hành chính của sản phẩm: từ khâu Import lead đầu vào, xử lý qua Telesale, bàn giao Courier thu chứng từ cho đến bước cuối cùng là đẩy dữ liệu sang hệ thống BPM.

*<img width="1781" height="731" alt="image" src="https://github.com/user-attachments/assets/13c95548-ea41-4948-9dcb-af5248e65faa" />*
