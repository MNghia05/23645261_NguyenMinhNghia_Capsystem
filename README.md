# CAB System - Nền Tảng Đặt Xe Trực Tuyến

---

## 1. Xác Định Yêu Cầu Hệ Thống

### 1.1. Yêu Cầu Kinh Doanh (Business Requirements)

Nền tảng **CAB System** được phát triển nhằm chuyển đổi toàn bộ mô hình vận hành đặt xe của doanh nghiệp ABC từ thủ công sang tự động hóa, giúp quản lý tập trung thông tin thanh toán, phương tiện, khách hàng, tài xế và lịch sử giao dịch trên một hệ thống duy nhất[cite: 1]. Nền tảng hướng tới mục tiêu:
* **Tối ưu hóa điều phối:** Tự động ghép chuyến theo thời gian thực dựa trên vị trí và trạng thái hoạt động của tài xế[cite: 1].
* **Nâng cao trải nghiệm:** Cung cấp thông tin minh bạch, rõ ràng cho khách hàng xuyên suốt hành trình[cite: 1].
* **Phân tích & Quản trị:** Cung cấp hệ thống báo cáo phân tích toàn diện (doanh thu, số lượng chuyến, tỷ lệ hoàn thành/hủy) phục vụ Ban giám đốc ra quyết định[cite: 1].
* **Mở rộng linh hoạt:** Kiến trúc dạng mô-đun chịu tải cao, đảm bảo hoạt động ổn định trong giờ cao điểm và sẵn sàng tích hợp các dịch vụ hay phương thức kinh doanh mới trong tương lai[cite: 1].

---

### 1.2. Yêu Cầu Chức Năng (Functional Requirements)

#### a. Khách hàng (Customer)
* **Tài khoản:** Đăng ký, đăng nhập và cập nhật thông tin cá nhân[cite: 1].
* **Đặt xe:** Nhập điểm đón/đến, chọn loại xe và gửi yêu cầu chuyến đi[cite: 1].
* **Theo dõi hành trình:** Theo dõi trạng thái chuyến đi real-time (tìm tài xế, thông tin tài xế nhận chuyến, thời gian dự kiến đến - ETA, trạng thái di chuyển)[cite: 1].
* **Lịch sử & Cước phí:** Xem lịch sử các chuyến đi và chi tiết số tiền phải trả[cite: 1].
* **Thanh toán:** Thanh toán linh hoạt bằng tiền mặt hoặc thanh toán điện tử; hỗ trợ xử lý lại nếu giao dịch thất bại[cite: 1].
* **Đánh giá:** Gửi đánh giá/phản hồi về tài xế sau khi hoàn thành chuyến đi[cite: 1].

#### b. Tài xế (Driver)
* **Tài khoản & Phương tiện:** Đăng ký tài khoản (hoặc nhờ nhân viên vận hành khởi tạo), cập nhật hồ sơ và thông tin xe[cite: 1].
* **Trạng thái làm việc:** Bật/tắt trạng thái sẵn sàng nhận chuyến[cite: 1].
* **Điều phối chuyến:** Nhận thông báo yêu cầu chuyến đi phù hợp; thực hiện chấp nhận hoặc từ chối chuyến[cite: 1].
* **Cập nhật tiến trình:** Cập nhật trạng thái chuyến đi theo thứ tự: *Đã đến điểm đón* $\rightarrow$ *Đã đón khách* $\rightarrow$ *Đang di chuyển* $\rightarrow$ *Hoàn thành chuyến*[cite: 1].
* **Vị trí địa lý:** Tự động gửi dữ liệu định vị (GPS) theo thời gian thực về hệ thống[cite: 1].

#### c. Thuật toán & Phân công chuyến (Dispatching & Matching)
* Tự động xác định tài xế phù hợp dựa trên vị trí, trạng thái sẵn sàng và các tiêu chí vận hành[cite: 1].
* Tự động chuyển giao yêu cầu cho tài xế tiếp theo nếu tài xế đầu tiên từ chối hoặc không phản hồi mà không bắt khách hàng thao tác lại[cite: 1].
* Thông báo rõ ràng cho khách hàng trong trường hợp không tìm thấy tài xế phù hợp[cite: 1].

#### d. Tính cước & Thanh toán (Pricing & Payment)
* Tự động tính toán tổng cước phí sau khi hoàn thành chuyến đi dựa trên dịch vụ và thông tin hành trình[cite: 1].
* Tích hợp cổng thanh toán điện tử bên ngoài để xử lý các giao dịch trực tuyến an toàn[cite: 1].

#### e. Quản trị & Vận hành (Operations & Management)
* **Giao diện Admin:** Cho phép nhân viên vận hành quản lý dữ liệu khách hàng, tài xế, phương tiện và danh sách chuyến đi[cite: 1].
* **Giám sát & Hỗ trợ:** Xem danh sách chuyến đi đang diễn ra, kiểm tra trạng thái tài xế và hỗ trợ xử lý chuyến lỗi/sự cố[cite: 1].
* **Phân quyền & Kiểm soát:** Tra cứu lịch sử giao dịch và phân quyền người dùng (giới hạn thao tác nhạy cảm đối với nhân viên thông thường)[cite: 1].
* **Báo cáo thống kê:** Xuất báo cáo chi tiết cho Ban lãnh đạo về tổng số chuyến, doanh thu, tỷ lệ hoàn thành/hủy, hiệu suất tài xế[cite: 1].

#### f. Thông báo (Notifications)
* **Khách hàng:** Nhận thông báo tiếp nhận yêu cầu, tài xế nhận chuyến, tài xế đến điểm đón, hoàn thành chuyến và kết quả thanh toán[cite: 1].
* **Tài xế:** Nhận thông báo chuyến mới hoặc các thay đổi liên quan đến chuyến đang thực hiện[cite: 1].

---

### 1.3. Yêu Cầu Phi Chức Năng (Non-Functional Requirements)

| Nhóm yêu cầu | Chi tiết yêu cầu |
| :--- | :--- |
| **Hiệu năng & Mở rộng** | • Hệ thống vận hành ổn định, chịu tải tốt trong giờ cao điểm.<br>• Kiến trúc dạng mô-đun cho phép mở rộng độc lập từng thành phần khi tải tăng[cite: 1]. |
| **Độ tin cậy & Sẵn sàng**| • Khả năng cách ly sự cố (lỗi ở mô-đun thanh toán/thông báo không ngưng trệ việc đặt xe).<br>• Triển khai cập nhật tính năng mới từng phần, hạn chế tối đa gián đoạn hệ thống[cite: 1]. |
| **Bảo mật (Security)** | • Bắt buộc xác thực tài khoản trước khi truy cập tính năng cá nhân.<br>• Phân quyền truy cập nghiêm ngặt cho các thao tác quản trị.<br>• Bảo vệ an toàn dữ liệu cá nhân, thông tin phương tiện, vị trí và giao dịch.<br>• **Không lưu trực tiếp** thông tin thẻ/tài khoản thanh toán nhạy cảm trên nền tảng[cite: 1]. |
| **Tính kiểm toán** | • Lưu vết nhật ký (logs) đầy đủ đối với các thao tác quan trọng để tra cứu khi có sự cố[cite: 1]. |
| **Tính linh hoạt** | • Kiến trúc linh hoạt, dễ dàng tích hợp thêm cổng thanh toán, kênh thông báo hoặc dịch vụ mới mà không cần tái cấu trúc toàn bộ ứng dụng[cite: 1]. |

---

## 2. Các Tác Nhân Của Hệ Thống (System Actors)

| Tác nhân | Loại | Mô tả vai trò |
| :--- | :--- | :--- |
| **Khách hàng** *(Customer)* | Human | Người dùng cuối đăng ký/đăng nhập, tạo yêu cầu đặt xe, theo dõi hành trình, thanh toán, xem lịch sử và đánh giá chất lượng tài xế[cite: 1]. |
| **Tài xế** *(Driver)* | Human | Người điều khiển phương tiện, cập nhật thông tin xe/hồ sơ, bật/tắt trạng thái nhận chuyến, tiếp nhận chuyến và cập nhật tiến trình chuyến đi real-time[cite: 1]. |
| **Nhân viên vận hành** *(Operations Staff)* | Human | Sử dụng giao diện Admin để quản lý dữ liệu hệ thống, tạo tài khoản tài xế, giám sát chuyến đi, xử lý sự cố và tra cứu giao dịch[cite: 1]. |
| **Ban giám đốc** *(Management)* | Human | Theo dõi hệ thống báo cáo thống kê (doanh thu, tỷ lệ hoàn thành/hủy, hiệu suất) để quản trị và đưa ra định hướng chiến lược[cite: 1]. |
| **Nhà cung cấp thanh toán** *(External Payment Provider)* | External System | Hệ thống bên thứ ba xử lý giao dịch thanh toán điện tử an toàn, giúp loại bỏ việc lưu trữ dữ liệu thẻ nhạy cảm trên CAB System[cite: 1]. |
| **Nhà cung cấp thông báo** *(External Notification Provider)* | External System | Hệ thống bên thứ ba đảm nhận việc truyền tải thông báo (SMS, Push Notification, Email) đến khách hàng và tài xế[cite: 1]. |
3.	Stalkholder
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

## 4. Ma Trận Stakeholder Metrix 

---
config:
  layout: elk
---
graph TD
    subgraph Stakeholders["Stakeholders"]
        Customer["Khách hàng<br/>(Customer)"]
        Driver["Tài xế<br/>(Driver)"]
        Operator["Nhân viên vận hành<br/>(Operator)"]
        Management["Ban lãnh đạo<br/>(Management)"]
        PaymentProvider["Nhà cung cấp thanh toán<br/>(Payment Provider)"]
        NotificationProvider["Nhà cung cấp thông báo<br/>(Notification Provider)"]
    end

    subgraph CABSystem["CAB System"]
        RideRequest["Yêu cầu đặt xe<br/>(Ride Request)"]
        DriverMatching["Tìm và phân công tài xế<br/>(Driver Matching)"]
        RideTracking["Theo dõi chuyến đi<br/>(Ride Tracking)"]
        FareCalculation["Tính cước<br/>(Fare Calculation)"]
        Payment["Thanh toán<br/>(Payment)"]
        Notification["Thông báo<br/>(Notification)"]
        Rating["Đánh giá<br/>(Rating)"]
        AdminManagement["Quản trị<br/>(Admin Management)"]
    end

    Customer -->|Tạo yêu cầu| RideRequest
    Customer -->|Theo dõi| RideTracking
    Customer -->|Thanh toán| Payment
    Customer -->|Nhận thông báo| Notification
    Customer -->|Đánh giá| Rating

    Driver -->|Nhận chuyến| DriverMatching
    Driver -->|Cập nhật trạng thái| RideTracking
    Driver -->|Nhận thông báo| Notification

    Operator -->|Quản lý| AdminManagement
    Operator -->|Quản lý tài xế| Driver
    Operator -->|Quản lý khách hàng| Customer

    Management -->|Giám sát báo cáo| AdminManagement
    Management -->|Đặt chính sách| RideRequest
    Management -->|Đặt chính sách| FareCalculation

    RideRequest -->|Kích hoạt| DriverMatching
    DriverMatching -->|Cập nhật| RideTracking
    RideTracking -->|Hoàn thành| FareCalculation
    FareCalculation -->|Thực hiện| Payment
    Payment -->|Kết quả| Notification
    RideTracking -->|Gửi cập nhật| Notification
    RideRequest -->|Gửi xác nhận| Notification

    Payment -->|Tích hợp| PaymentProvider
    Notification -->|Tích hợp| NotificationProvider

    style Customer fill:#eef2ff,stroke:#818cf8,stroke-width:2px
    style Driver fill:#f0fdfa,stroke:#2dd4bf,stroke-width:2px
    style Operator fill:#f5f3ff,stroke:#a78bfa,stroke-width:2px
    style Management fill:#fff7ed,stroke:#fb923c,stroke-width:2px
    style PaymentProvider fill:#fdf4ff,stroke:#e879f9,stroke-width:2px
    style NotificationProvider fill:#ecfeff,stroke:#22d3ee,stroke-width:2px
    style RideRequest fill:#f0fdf4,stroke:#4ade80,stroke-width:2px
    style DriverMatching fill:#f0fdf4,stroke:#4ade80,stroke-width:2px
    style RideTracking fill:#f0fdf4,stroke:#4ade80,stroke-width:2px
    style FareCalculation fill:#fefce8,stroke:#facc15,stroke-width:2px
    style Payment fill:#fef2f2,stroke:#f87171,stroke-width:2px
    style Notification fill:#f0f9ff,stroke:#38bdf8,stroke-width:2px
    style Rating fill:#f7fee7,stroke:#a3e635,stroke-width:2px
    style AdminManagement fill:#fff1f2,stroke:#fb7185,stroke-width:2px
