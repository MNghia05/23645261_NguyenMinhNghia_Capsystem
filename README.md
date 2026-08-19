# CAB System - Nền Tảng Đặt Xe Trực Tuyến
## 1. Lý Do Phát Triển Dự Án (Why CAB System?)

Sự phát triển mạnh mẽ của kinh tế số cùng nhu cầu di chuyển đô thị ngày càng tăng đã bộc lộ rõ những hạn chế của mô hình vận hành đặt xe truyền thống. Việc điều phối thủ công qua tổng đài không chỉ làm tăng chi phí vận hành (OpEx) mà còn khiến khách hàng gặp khó khăn khi không thể biết trước cước phí hay theo dõi vị trí tài xế. Tình trạng này dẫn đến thời gian chờ đợi kéo dài, tỷ lệ hủy chuyến cao và thời gian chạy xe rỗng lớn. Bên cạnh đó, việc quản lý thanh toán tiền mặt và đối soát hoa hồng thủ công dễ gây thất thoát tài chính và khiến doanh nghiệp thiếu dữ liệu thời gian thực để ra quyết định kinh doanh kịp thời.

**CAB System** ra đời như một giải pháp công nghệ toàn diện nhằm tự động hóa hoàn toàn quy trình vận hành. Nhờ thuật toán ghép chuyến thông minh theo bán kính định vị GPS, hệ thống kết nối khách hàng với tài xế gần nhất trong chưa đầy 30 giây, giúp tối ưu hóa quãng đường di chuyển và cắt giảm tối đa chi phí trung gian. Việc minh bạch hóa giá cước cố định (Upfront Pricing), tích hợp đa dạng cổng thanh toán điện tử, tự động hóa trích xuất hoa hồng vào Ví tài xế và cung cấp công cụ theo dõi hành trình thời gian thực không chỉ nâng cao trải nghiệm người dùng mà còn đảm bảo dòng tiền được quản lý chính xác, minh bạch. Đây là nền tảng công nghệ hiện đại, có khả năng mở rộng linh hoạt, giúp doanh nghiệp tối ưu hóa nguồn lực và bứt phá lợi thế cạnh tranh trên thị trường.

7. vẽ usecase diagram
8. đặc tả
9. phân tích quy trình nghiệp vụ 
10. phân tích quy tắc nghiệp vụ (business rules)
    
---

## Các Tác Nhân Của Hệ Thống (System Actors)

| Tác nhân | Loại | Mô tả vai trò |
| :--- | :--- | :--- |
| **Khách hàng** *(Customer)* | Human | Người dùng cuối đăng ký/đăng nhập, tạo yêu cầu đặt xe, theo dõi hành trình, thanh toán, xem lịch sử và đánh giá chất lượng tài xế[cite: 1]. |
| **Tài xế** *(Driver)* | Human | Người điều khiển phương tiện, cập nhật thông tin xe/hồ sơ, bật/tắt trạng thái nhận chuyến, tiếp nhận chuyến và cập nhật tiến trình chuyến đi real-time[cite: 1]. |
| **Nhân viên vận hành** *(Operations Staff)* | Human | Sử dụng giao diện Admin để quản lý dữ liệu hệ thống, tạo tài khoản tài xế, giám sát chuyến đi, xử lý sự cố và tra cứu giao dịch[cite: 1]. |
| **Ban giám đốc** *(Management)* | Human | Theo dõi hệ thống báo cáo thống kê (doanh thu, tỷ lệ hoàn thành/hủy, hiệu suất) để quản trị và đưa ra định hướng chiến lược[cite: 1]. |
| **Nhà cung cấp thanh toán** *(External Payment Provider)* | External System | Hệ thống bên thứ ba xử lý giao dịch thanh toán điện tử an toàn, giúp loại bỏ việc lưu trữ dữ liệu thẻ nhạy cảm trên CAB System[cite: 1]. |
| **Nhà cung cấp thông báo** *(External Notification Provider)* | External System | Hệ thống bên thứ ba đảm nhận việc truyền tải thông báo (SMS, Push Notification, Email) đến khách hàng và tài xế[cite: 1]. |

---

## 2. Các Bên Liên Quan (Stakeholders)
## Các Bên Liên Quan (Stakeholders)

| Stakeholder | Vai Trò |
| :--- | :--- |
| **Ban giám đốc** | Nhóm định hướng chiến lược, đưa ra các kỳ vọng kinh doanh, theo dõi báo cáo thống kê (doanh thu, số chuyến, hiệu quả hoạt động) và quyết định phê duyệt dự án. |
| **Khách hàng** | Người dùng cuối trực tiếp đặt xe, chọn loại dịch vụ, theo dõi hành trình, thực hiện thanh toán, xem lịch sử chuyến đi và đánh giá chất lượng dịch vụ của tài xế. |
| **Tài xế** | Người trực tiếp cung cấp dịch vụ vận chuyển, cập nhật thông tin hồ sơ/phương tiện, bật/tắt trạng thái làm việc, nhận/từ chối chuyến và cập nhật tiến trình chuyến đi theo thời gian thực. |
| **Nhân viên vận hành** | Nhóm quản trị hệ thống hàng ngày, thực hiện tạo tài khoản cho tài xế, kiểm tra trạng thái hoạt động, hỗ trợ xử lý sự cố/chuyến lỗi và tra cứu thông tin giao dịch. |
| **Chuyên viên phân tích nghiệp vụ** | Người đóng vai trò cầu nối, chịu trách nhiệm làm rõ các yêu cầu chưa chốt (cách tính cước, tiêu chí phân công, chính sách hủy chuyến...) với các bên liên quan và xác định phạm vi, quy trình nghiệp vụ cho đội ngũ phát triển. |
| **Đội ngũ phát triển** | Nhóm kỹ thuật chịu trách nhiệm thiết kế kiến trúc linh hoạt, xây dựng và triển khai sản phẩm CAB System theo đúng các yêu cầu nghiệp vụ và kỹ thuật. |


| **Nhà cung cấp thanh toán bên ngoài** | Đối tác bên thứ ba chịu trách nhiệm tiếp nhận và xử lý bảo mật các giao dịch thanh toán điện tử cho khách hàng. |
| **Nhà cung cấp dịch vụ thông báo** | Đối tác bên thứ ba hỗ trợ chuyển tải thông báo (SMS, Push Notification...) đến khách hàng và tài xế qua các kênh hạ tầng. |

## Ma Trận Stakeholder Metrix 

```mermaid
quadrantChart
    title Stakeholder Matrix - CAB System
    x-axis Low Power --> High Power
    y-axis Low Interest --> High Interest
    quadrant-1 Key Player - Quản lý chặt chẽ
    quadrant-2 Keep Informed - Cung cấp thông tin
    quadrant-3 Monitor - Theo dõi
    quadrant-4 Keep Satisfied - Giữ hài lòng

    Ban Lãnh Đạo: [0.85, 0.85]
    Khách Hàng: [0.35, 0.85]
    Tài Xế: [0.35, 0.75]
    Nhân Viên Vận Hành: [0.42, 0.80]
    Nhà Cung Cấp Thanh Toán: [0.75, 0.35]
    Nhà Cung Cấp Thông Báo: [0.25, 0.35]

```
## 3. Đơn Vị Nghiệp Vụ (Business Units) & Vai Trò Trong Hệ Thống

| Business Unit | Chức năng chính | Phạm vi Dữ liệu & Công cụ | Stakeholders liên quan |
| :--- | :--- | :--- | :--- |
| **Khối Vận hành** *(Operations)* | • Giám sát & điều phối chuyến đi thời gian thực.<br>• Quản lý danh sách, hồ sơ & trạng thái tài xế.<br>• Xử lý các sự cố phát sinh trên đường. | • Live Map Dashboard.<br>• Quản lý Chuyến đi, Tài xế, Định vị GPS. | Nhân viên vận hành, Tài xế |
| **Khối Tài chính & Thanh toán** *(Finance & Billing)* | • Quản lý dòng tiền, tích hợp cổng thanh toán.<br>• Cấu hình bảng cước phí, tỷ lệ chiết khấu.<br>• Đối soát giao dịch & thanh toán cho tài xế. | • Bảng cấu hình Cước phí (Pricing Policy).<br>• Lịch sử giao dịch, Hóa đơn, Ví tài xế. | Ban lãnh đạo, Nhà cung cấp thanh toán, Tài xế |
| **Khối Chăm sóc Khách hàng** *(Customer Support - CS)* | • Tiếp nhận & xử lý khiếu nại của khách hàng/tài xế.<br>• Xử lý yêu cầu hoàn tiền, đền bù chuyến đi.<br>• Quản lý hệ thống đánh giá & phản hồi. | • Hệ thống Quản lý Ticket (CS Portal).<br>• Lịch sử khiếu nại, Đánh giá (Rating/Review). | Khách hàng, Tài xế |
| **Khối Quản trị & Chiến lược** *(Executive Management)* | • Theo dõi chỉ số tăng trưởng & báo cáo BI.<br>• Phê duyệt chính sách giá, khuyến mãi, ngân sách.<br>• Cấu hình các tham số vận hành toàn hệ thống. | • Executive Dashboard (Revenue, Growth).<br>• System Configuration, Audit Logs. | Ban lãnh đạo |

---

### Sơ Đồ Tương Tác Giữa Các Business Units

```mermaid
graph LR
    Management["Khối Quản trị & Chiến lược"] -->|Cấu hình giá & chính sách| Finance["Khối Tài chính & Thanh toán"]
    Management -->|Ban hành quy trình vận hành| Ops["Khối Vận hành"]
    
    Ops -->|Chuyển sự cố thanh toán| Finance
    CS["Khối Chăm sóc Khách hàng"] -->|Chuyển sự cố chuyến đi/tài xế| Ops
    CS -->|Yêu cầu duyệt hoàn tiền| Finance

    style Management fill:#fff7ed,stroke:#fb923c,stroke-width:2px
    style Finance fill:#fdf4ff,stroke:#e879f9,stroke-width:2px
    style Ops fill:#f5f3ff,stroke:#a78bfa,stroke-width:2px
    style CS fill:#eef2ff,stroke:#818cf8,stroke-width:2px
```
## 4. Phạm Vi Dự Án & Lộ Trình Triển Khai 7 Tuần (MVP Scope & Roadmap)

Để đưa **CAB System** vào hoạt động thực tế đúng hạn trong **7 tuần**, dự án áp dụng chiến lược **MVP (Minimum Viable Product)**: tập trung xây dựng luồng nghiệp vụ cốt lõi (Đặt xe - Ghép chuyến - Theo dõi - Thanh toán) và hoãn lại các tính năng nâng cao sang giai đoạn 2.

---

### 4.1. Bảng Tóm Tắt Phạm Vi (In-Scope vs. Out-of-Scope)

| Hạng mục | Trong phạm vi MVP (7 tuần) | Giai đoạn 2 (Out-of-Scope) |
| :--- | :--- | :--- |
| **Đặt xe & Ghép chuyến** | • Đặt xe tức thì (Book now).<br>• Tìm & phân công tài xế gần nhất (bán kính cố định). | • Đặt xe theo lịch (Schedule ride).<br>• Đi chung xe (Ride sharing / Pooling). |
| **Định vị & Theo dõi** | • Cập nhật vị trí GPS tài xế thời gian thực.<br>• Tính quãng đường & thời gian dự kiến (Google Maps API). | • Tối ưu hóa lộ trình đa điểm dừng (Multi-stop).<br>• Cảnh báo lệch tuyến thông minh. |
| **Tính cước & Thanh toán** | • Bảng giá cố định theo km + thời gian chờ.<br>• Tích hợp 01 cổng thanh toán điện tử (VNPay/Momo) + Tiền mặt. | • Thuật toán tăng giá theo cầu (Surge Pricing).<br>• Mã giảm giá/Khuyến mãi phức tạp. |
| **Quản trị & Vận hành** | • Admin Dashboard: Quản lý Tài xế, Khách hàng, Chuyến đi.<br>• Tra cứu lịch sử & xử lý sự cố cơ bản. | • Hệ thống BI/Analytics chuyên sâu.<br>• Tự động hóa đối soát tài chính nâng cao. |
| **Thông báo & Đánh giá** | • Gửi Push Notification (Firebase) & SMS OTP.<br>• Đánh giá sao (1-5★) + nhận xét ngắn sau chuyến. | • Chương trình Khách hàng thân thiết (Loyalty Point).<br>• Chat trực tiếp trong ứng dụng (In-app Chat). |

---

### 4.2. Lộ Trình Triển Khai Chi Tiết Trong 7 Tuần (7-Week Roadmap)

```mermaid
gantt
    title Lộ trình triển khai CAB System (7 Tuần)
    dateFormat  YYYY-MM-DD
    axisFormat  Tuần %W

    section Tuần 1
    Phân tích & Kiến trúc (Yêu cầu, CSDL, Dev Env) :done, w1, 2026-08-17, 7d
    section Tuần 2
    Xác thực & User Service (Auth, OTP, Hồ sơ User) :active, w2, after w1, 7d
    section Tuần 3
    Booking Core (Đặt xe, Thuật toán tìm tài xế) :w3, after w2, 7d
    section Tuần 4
    GPS & Fare Engine (Tracking Websocket, Tính cước) :w4, after w3, 7d
    section Tuần 5
    Integration (Cổng thanh toán, Firebase Notification) :w5, after w4, 7d
    section Tuần 6
    Operations & QA (Web Admin, E2E Testing) :w6, after w5, 7d
    section Tuần 7
    Deployment (UAT, Fix bugs, Go-Live Production) :w7, after w6, 7d
```
## 5. Yêu Cầu Nghiệp Vụ (Business Requirements - BRD)

---

### 5.1. Nhóm Yêu Cầu: Đặt Xe & Điều Phối Chuyến Đi (Booking & Matching)

| Mã BR | Tên Yêu Cầu Nghiệp Vụ | Mô Tả Nghiệp Vụ & Quy Tắc Kinh Doanh | Mục Tiêu Kinh Doanh / KPI |
| :--- | :--- | :--- | :--- |
| **BR-BOOK-01** | **Tạo yêu cầu đặt xe tức thì** | • Khách hàng chọn điểm đi, điểm đến và xem trước giá cước trị giá cố định trước khi xác nhận.<br>• Hệ thống chỉ cho phép tạo chuyến nếu khách hàng không có chuyến đi nào đang dở dang. | Tối ưu trải nghiệm đặt xe, tỉ lệ hoàn tất thao tác đặt xe trong **< 15 giây**. |
| **BR-BOOK-02** | **Tự động ghép chuyến theo bán kính** | • Hệ thống tự động quét và gửi thông báo mời nhận chuyến cho tài xế rảnh gần nhất trong bán kính $R$ (mặc định 3km).<br>• Nếu tài xế từ chối hoặc quá 15 giây không phản hồi, tự động chuyển sang tài xế tiếp theo. | Đạt tỉ lệ ghép chuyến thành công **> 85%** trong lần quét đầu tiên; thời gian chờ tài xế **< 30 giây**. |
| **BR-BOOK-03** | **Quản lý vòng đời chuyến đi** | • Chuyến đi trải qua các trạng thái bắt buộc: *Đã đặt $\rightarrow$ Tài xế nhận $\rightarrow$ Đã đến điểm đón $\rightarrow$ Đang di chuyển $\rightarrow$ Hoàn thành (hoặc Hủy)*.<br>• Cho phép hủy chuyến miễn phí trong 2 phút đầu sau khi tài xế nhận chuyến. | Minh bạch luồng vận hành, giảm tỉ lệ tranh chấp hủy chuyến dưới **5%**. |

---

### 5.2. Nhóm Yêu Cầu: Giá Cước & Thanh Toán (Pricing & Settlement)

| Mã BR | Tên Yêu Cầu Nghiệp Vụ | Mô Tả Nghiệp Vụ & Quy Tắc Kinh Doanh | Mục Tiêu Kinh Doanh / KPI |
| :--- | :--- | :--- | :--- |
| **BR-FIN-01** | **Tính cước phí tự động** | • Công thức tính cước: `Tổng giá = Giá mở cửa + (Số km x Đơn giá/km) + Phí chờ` (nếu có).<br>• Bảng giá có thể điều chỉnh linh hoạt theo khung giờ (Giờ cao điểm / Giờ đêm) bởi Khối Vận hành. | Đảm bảo tính cước chính xác 100%, không xảy ra sai lệch giữa ứng dụng và máy chủ. |
| **BR-FIN-02** | **Hỗ trợ đa dạng thanh toán** | • Hỗ trợ 2 hình thức: **Tiền mặt** và **Thanh toán điện tử** (Cổng VNPay/MoMo).<br>• Với thanh toán điện tử, hệ thống giữ tiền (Hold/Pre-auth) hoặc thu tiền ngay khi hoàn thành chuyến đi. | Giảm tỷ lệ giao dịch thất bại xuống **< 1%**; đối soát dòng tiền chính xác trong ngày (T+0). |
| **BR-FIN-03** | **Tự động trích xuất hoa hồng tài xế** | • Hệ thống tự động khấu trừ % chiết khấu (ví dụ: 20%) trên mỗi chuyến đi hoàn thành vào Ví điện tử của Tài xế.<br>• Tài xế phải duy trì số dư tối thiểu trong ví để tiếp tục nhận chuyến. | Tự động hóa đối soát tài chính, loại bỏ 100% công đoạn tính toán thủ công. |

---

### 5.3. Nhóm Yêu Cầu: Giám Sát Hành Trình & An Toàn (Tracking & Safety)

| Mã BR | Tên Yêu Cầu Nghiệp Vụ | Mô Tả Nghiệp Vụ & Quy Tắc Kinh Doanh | Mục Tiêu Kinh Doanh / KPI |
| :--- | :--- | :--- | :--- |
| **BR-TRK-01** | **Theo dõi vị trí thời gian thực** | • Khách hàng và Khối Vận hành theo dõi được vị trí di chuyển thực tế của tài xế trên bản đồ với độ trễ tối đa 3-5 giây.<br>• Tự động tính toán lại thời gian dự kiến đến (ETA). | Tăng mức độ an tâm cho khách hàng; độ chính xác định vị sai số **< 10m**. |
| **BR-TRK-02** | **Cảnh báo và xử lý sự cố khẩn cấp** | • Cung cấp nút hỗ trợ khẩn cấp / báo sự cố trên ứng dụng cho cả Khách hàng và Tài xế.<br>• Tự động bắn cảnh báo ưu tiên cao về màn hình giám sát của Khối Vận hành. | Thời gian phản hồi sự cố khẩn cấp của bộ phận Vận hành **< 3 phút**. |

---

### 5.4. Nhóm Yêu Cầu: Đánh Giá & Vận Hành Khách Hàng (Customer Experience & Ops)

| Mã BR | Tên Yêu Cầu Nghiệp Vụ | Mô Tả Nghiệp Vụ & Quy Tắc Kinh Doanh | Mục Tiêu Kinh Doanh / KPI |
| :--- | :--- | :--- | :--- |
| **BR-OPS-01** | **Duyệt hồ sơ & Quản lý đối tác tài xế** | • Tài xế chỉ được phép bật chế độ "Sẵn sàng nhận chuyến" sau khi bộ phận Vận hành thẩm định và duyệt đầy đủ: *Bằng lái, Căn cước, Đăng ký xe, Bảo hiểm*.<br>• Tự động khóa tài khoản nếu tài xế bị đánh giá dưới 3.0★. | Đảm bảo 100% tài xế lưu thông trên hệ thống hợp pháp và đạt chuẩn chất lượng. |
| **BR-OPS-02** | **Đánh giá và Tiếp nhận phản hồi** | • Cho phép khách hàng chấm điểm (1-5 sao) và chọn lý do phản hồi sau khi kết thúc chuyến.<br>• Tự động tạo ticket xử lý cho CS khi nhận đánh giá 1-2 sao hoặc có phản ánh thái độ/phụ phí. | Duy trì điểm hài lòng trung bình của dịch vụ (CSAT) **$\ge$ 4.5/5.0★**. |

---

## 6. Phân Rã Chi Tiết Yêu Cầu Chức Năng (Functional Requirements Breakdown)

---

## 📑 Danh Sách Chức Năng Hệ Thống (Feature Matrix)

Bảng tổng hợp chi tiết toàn bộ các chức năng hệ thống được trích xuất từ các **Yêu Cầu Nghiệp Vụ (BRD)**:

| Nhóm Nghiệp Vụ | Mã BR | Danh Sách Chức Năng Hệ Thống (Features) |
| :--- | :--- | :--- |
| **1. Đặt Xe & Ghép Chuyến**<br>*(Booking & Matching)* | **BR-BOOK-01** | • **Định vị & Chọn địa điểm:** Tự động lấy tọa độ hiện tại, tìm kiếm và ghim điểm đón/trả.<br>• **Kiểm tra trạng thái người dùng:** Chặn đặt xe mới nếu đang có chuyến đi chưa hoàn thành.<br>• **Xem trước cước phí & Lộ trình (Upfront Pricing):** Hiển thị cước phí cố định và thời gian di chuyển dự kiến (ETA) trước khi xác nhận.<br>• **Khởi tạo chuyến đi:** Tạo bản ghi chuyến đi ở trạng thái chờ (`PENDING`). |
| | **BR-BOOK-02** | • **Quét vị trí tài xế:** Tự động định vị và lọc danh sách tài xế rảnh (`AVAILABLE`) trong bán kính quy định (3km).<br>• **Thuật toán phân công tài xế:** Tự động sắp xếp và gửi thông báo mời nhận chuyến tới tài xế tối ưu nhất.<br>• **Quản lý đếm ngược & Chuyển chuyến:** Hiển thị màn hình chờ nhận chuyến 15s cho tài xế; tự động chuyển sang tài xế khác nếu bị từ chối hoặc hết giờ.<br>• **Xử lý ghép chuyến thất bại:** Tự động mở rộng bán kính quét hoặc thông báo không tìm thấy xe. |
| | **BR-BOOK-03** | • **Quản lý trạng thái chuyến đi (State Machine):** Chuyển đổi và kiểm soát chặt chẽ các trạng thái (*Đã đặt $\rightarrow$ Nhận chuyến $\rightarrow$ Đến điểm đón $\rightarrow$ Đang di chuyển $\rightarrow$ Hoàn thành*).<br>• **Hủy chuyến đi & Tính phí phạt:** Cho phép hủy chuyến miễn phí (trong 2 phút đầu) và tự động áp dụng phí phạt hủy chuyến muộn. |
| **2. Giá Cước & Thanh Toán**<br>*(Pricing & Settlement)* | **BR-FIN-01** | • **Tính cước phí tự động:** Tính toán tổng tiền theo công thức (Giá mở cửa + Số km $\times$ Đơn giá + Phí chờ).<br>• **Cấu hình bảng giá linh hoạt:** Cho phép quản trị viên điều chỉnh đơn giá theo khung giờ (Giờ cao điểm / Đêm).<br>• **Tính lại cước phí khi đổi lộ trình:** Tự động điều chỉnh giá tiền dựa trên số km thực tế khi kết thúc chuyến nếu đi sai lộ trình ban đầu. |
| | **BR-FIN-02** | • **Thanh toán tiền mặt:** Hiển thị số tiền phải thu cho tài xế và ghi nhận xác nhận thu tiền.<br>• **Thanh toán qua cổng điện tử (VNPay/MoMo):** Tự động giữ tiền (Hold/Pre-auth) khi đặt xe và trừ tiền thực tế (Capture) khi kết thúc chuyến.<br>• **Xử lý lỗi thanh toán:** Tự động chuyển đổi hình thức thanh toán sang tiền mặt khi cổng thanh toán gặp sự cố. |
| | **BR-FIN-03** | • **Trích xuất hoa hồng tự động:** Khấu trừ trực tiếp % chiết khấu hệ thống vào Ví điện tử của tài xế sau mỗi chuyến đi.<br>• **Kiểm soát hạn mức ví tài xế:** Tự động khóa quyền nhận chuyến nếu số dư ví của tài xế xuống dưới mức tối thiểu. |
| **3. Giám Sát & An Toàn**<br>*(Tracking & Safety)* | **BR-TRK-01** | • **Định vị GPS Realtime:** Thu thập và truyền tọa độ tài xế thời gian thực ($3-5\text{s}/lần$) qua kết nối WebSocket/MQTT.<br>• **Hiển thị bản đồ hành trình:** Cho phép Khách hàng và Khối Vận hành theo dõi vị trí xe di chuyển trên bản đồ.<br>• **Tự động cập nhật ETA:** Tính toán lại thời gian đến dự kiến dựa trên tốc độ thực tế. |
| | **BR-TRK-02** | • **Nút báo động khẩn cấp (SOS):** Cung cấp nút hỗ trợ khẩn cấp trên màn hình ứng dụng Khách hàng và Tài xế.<br>• **Cảnh báo sự cố ưu tiên:** Nổi cảnh báo đỏ/âm thanh trên màn hình giám sát của Vận hành và tự động gửi SMS vị trí tới số điện thoại người thân. |
| **4. Đánh Giá & Vận Hành**<br>*(Ops & Support)* | **BR-OPS-01** | • **Đăng ký & Tải hồ sơ tài xế:** Tiếp nhận ảnh chụp Căn cước, Bằng lái, Đăng ký xe, Bảo hiểm.<br>• **Thẩm định & Duyệt hồ sơ (Admin Portal):** Cho phép nhân viên Vận hành kiểm tra và duyệt hồ sơ trước khi kích hoạt tài khoản tài xế.<br>• **Tự động khóa tài khoản kém chất lượng:** Chạy tiến trình tự động khóa tài khoản nếu điểm đánh giá trung bình của tài xế rơi xuống dưới $3.0\star$. |
| | **BR-OPS-02** | • **Đánh giá & Chấm điểm (Rating):** Popup chấm điểm $1-5\star$, chọn lý do nhanh hoặc nhập phản hồi sau chuyến đi.<br>• **Tính điểm trung bình tích lũy:** Cập nhật điểm uy tín trung bình của tài xế tức thì.<br>• **Tự động tạo Ticket CSKH:** Khởi tạo yêu cầu hỗ trợ (Ticket) gán độ ưu tiên cao tới bộ phận CSKH khi nhận đánh giá $1-2\star$. |

```mermaid
graph LR
    %% Actors
    subgraph Actors
        Rider["👤 Khách hàng"]
        Driver["🚗 Tài xế"]
        Ops["🛠️ Nhân viên Vận hành"]
        CS["🎧 Nhân viên CSKH"]
        MapExt["🗺️ Hệ thống Bản đồ"]
        PayExt["💳 Cổng Thanh toán"]
    end

    %% Use Cases Boundary
    subgraph CAB_System ["HỆ THỐNG CAB SYSTEM"]
        UC01("(UC01: Đăng ký / Đăng nhập)")
        UC02("(UC02: Đăng ký & Upload hồ sơ)")
        UC03("(UC03: Phê duyệt hồ sơ Tài xế)")
        UC04("(UC04: Tìm địa điểm & Xem giá)")
        UC05("(UC05: Tạo yêu cầu đặt xe)")
        UC06("(UC06: Ghép chuyến tự động)")
        UC07("(UC07: Nhận / Từ chối chuyến)")
        UC08("(UC08: Hủy chuyến đi)")
        UC09("(UC09: Live Tracking GPS)")
        UC10("(UC10: Cập nhật trạng thái chuyến)")
        UC11("(UC11: Kích hoạt cảnh báo SOS)")
        UC12("(UC12: Thanh toán cước phí)")
        UC13("(UC13: Trích xuất hoa hồng Ví)")
        UC14("(UC14: Đánh giá & Feedback)")
        UC15("(UC15: Xử lý Ticket khiếu nại)")
    end

    %% Connections
    Rider --> UC01
    Rider --> UC04
    Rider --> UC05
    Rider --> UC08
    Rider --> UC09
    Rider --> UC11
    Rider --> UC12
    Rider --> UC14

    Driver --> UC01
    Driver --> UC02
    Driver --> UC07
    Driver --> UC08
    Driver --> UC10
    Driver --> UC11
    Driver --> UC13

    Ops --> UC03
    Ops --> UC09
    Ops --> UC11

    CS --> UC15

    UC04 -.-> MapExt
    UC09 -.-> MapExt
    UC12 -.-> PayExt
```
