1.	Xác định yêu cầu hệ thống
1.1.	Yêu cầu kinh doanh
Nền tảng CAB System được phát triển nhằm thay đổi toàn bộ mô hình vận hành đặt xe của doanh nghiệp ABC từ thủ công sang tự động hóa, giúp quản lý tập trung toàn bộ thông tin thanh toán, phương tiện,
khách hàng, tài xế và lịch sử giao dịch trên một hệ thống duy nhất. Nền tảng hướng tới mục tiêu tối ưu hóa quy trình điều phối và ghép chuyến tự động theo thời gian thực dựa trên vị trí và trạng thái tài xế,
nâng cao trải nghiệm minh bạch cho khách hàng, đồng thời cung cấp hệ thống báo cáo phân tích toàn diện (doanh thu, số chuyến, tỷ lệ hoàn thành/hủy) cho ban giám đốc. Với kiến trúc linh hoạt,
mở rộng độc lập và có tính chịu tải cao, hệ thống đảm bảo khả năng phục vụ số lượng lớn người dùng ở các mốc cao điểm và sẵn sàng cho việc mở rộng quy mô, tích hợp các dịch vụ hay phương thức kinh doanh mới trong tương lai.

1.2.	Yêu cầu chức năng
a.	Khách hàng (Customer)
Đăng ký, đăng nhập và quản lý/cập nhật thông tin cá nhân. 
Tạo yêu cầu chuyến đi: nhập điểm đón/đến, chọn loại xe và gửi yêu cầu. 
Theo dõi chuyến đi theo thời gian thực: trạng thái tìm tài xế, thông tin tài xế nhận chuyến, thời gian dự kiến đến và trạng thái hành trình. 
Xem lịch sử chuyến đi và chi tiết số tiền phải trả. 
Thanh toán chuyến đi (tiền mặt hoặc thanh toán điện tử) và xử lý lại nếu giao dịch điện tử thất bại. 
Đánh giá tài xế sau khi hoàn thành chuyến đi. 
b.	Tài xế (Driver)
Đăng ký tài khoản (hoặc được nhân viên vận hành tạo) và cập nhật hồ sơ, thông tin phương tiện. 
Bật/tắt trạng thái sẵn sàng làm việc/nhận chuyến. 
Nhận thông báo yêu cầu chuyến đi phù hợp; thực hiện chấp nhận hoặc từ chối chuyến. 
Cập nhật tiến trình/trạng thái chuyến đi: Đã đến điểm đón, Đã đón khách, Đang di chuyển, Hoàn thành chuyến. 
Tự động gửi/cập nhật dữ liệu vị trí địa lý theo thời gian thực về hệ thống. 
c.	Thuật toán & Phân công chuyến (Dispatching & Matching)
Tự động xác định tài xế phù hợp dựa trên vị trí, trạng thái sẵn sàng và tiêu chí vận hành. 
Tự động chuyển giao yêu cầu cho tài xế khác nếu tài xế đầu tiên từ chối hoặc không phản hồi mà không bắt khách hàng tạo lại yêu cầu. 
Thông báo rõ ràng cho khách hàng trong trường hợp không tìm được tài xế phù hợp. 
d.	Tính cước & Thanh toán (Pricing & Payment)
Tự động tính toán số tiền cước sau khi hoàn thành chuyến đi dựa trên thông tin chuyến đi và loại dịch vụ. 
Tích hợp cổng thanh toán điện tử bên ngoài để xử lý giao dịch trực tuyến. 
e.	Quản trị & Vận hành (Operations & Management)
Giao diện quản trị viên cho nhân viên vận hành quản lý khách hàng, tài xế, phương tiện và chuyến đi. 
Xem danh sách các chuyến đi đang diễn ra, kiểm tra trạng thái tài xế và hỗ trợ xử lý sự cố/chuyến lỗi. 
Tra cứu lịch sử giao dịch và phân quyền người dùng (giới hạn các thao tác nhạy cảm đối với nhân viên thông thường). 
Xuất báo cáo thống kê cho ban lãnh đạo về tổng số chuyến, doanh thu, tỷ lệ hoàn thành/hủy chuyến, hiệu quả làm việc của tài xế. 
f.	Thông báo (Notifications)
Gửi thông báo đến khách hàng: tiếp nhận yêu cầu, tài xế nhận chuyến, tài xế đến điểm đón, hoàn thành chuyến, kết quả thanh toán. 
Gửi thông báo đến tài xế: có chuyến mới, thay đổi thông tin liên quan đến chuyến đang thực hiện.
1.3.	Yêu cầu phi chức năng
a.	Hiệu năng & Khả năng mở rộng (Performance & Scalability):
Hệ thống hoạt động ổn định, chịu tải tốt vào các thời điểm cao điểm. 
Kiến trúc dạng mô-đun/thành phần cho phép mở rộng độc lập từng phần khi lưu lượng truy cập tăng. 
b.	Độ tin cậy & Độ sẵn sàng (Reliability & Availability):
Thiết kế có khả năng cách ly sự cố: lỗi ở mô-đun thanh toán hoặc thông báo không làm ngưng trệ toàn bộ hệ thống đặt xe. 
Triển khai cập nhật chức năng mới theo từng phần, hạn chế gián đoạn các tính năng đang hoạt động. 
c.	Bảo mật (Security):
Yêu cầu xác thực tài khoản bắt buộc đối với khách hàng và tài xế trước khi truy cập các tính năng cá nhân. 
Phân quyền truy cập nghiêm ngặt đối với các thao tác quản trị chuyên sâu. 
Bảo vệ an toàn dữ liệu cá nhân, thông tin phương tiện, vị trí và lịch sử giao dịch. 
Không lưu trữ trực tiếp các thông tin thẻ/tài khoản thanh toán nhạy cảm trên hệ thống CAB (ủy quyền cho nhà cung cấp thanh toán bên ngoài). 

2.	Xác định các tác nhân của hệ thống
•	Khách hàng (Customer):
Người dùng cuối đăng ký, đăng nhập, nhập thông tin chuyến đi (điểm đón/đến, loại xe), gửi yêu cầu đặt xe, theo dõi hành trình và xem trạng thái chuyến đi. 
Thực hiện thanh toán (tiền mặt hoặc điện tử), xem lịch sử chuyến đi và đánh giá tài xế sau khi hoàn thành. 
•	Tài xế (Driver):
Người điều khiển phương tiện, cập nhật hồ sơ, thông tin xe và trạng thái hoạt động (sẵn sàng/không sẵn sàng nhận chuyến). 
Nhận thông báo chuyến mới, chấp nhận/từ chối chuyến và cập nhật các trạng thái chuyến đi (đã đến điểm đón, đã đón khách, đang di chuyển, hoàn thành). 
•	Nhân viên vận hành (Operations Staff / Admin):
Sử dụng giao diện quản trị để quản lý thông tin khách hàng, tài xế, phương tiện và danh sách chuyến đi. 
Hỗ trợ tạo tài khoản cho tài xế, kiểm tra trạng thái hoạt động, xử lý sự cố/lỗi chuyến đi và tra cứu lịch sử giao dịch. 
•	Ban giám đốc / Ban lãnh đạo (Management):
Xem các báo cáo thống kê về tổng số chuyến đi, doanh thu, tỷ lệ hoàn thành/hủy chuyến và hiệu quả hoạt động của tài xế để phục vụ quản lý, vận hành. 
•	Nhà cung cấp thanh toán bên ngoài (External Payment Provider):
Hệ thống bên thứ ba chịu trách nhiệm tiếp nhận giao dịch và xử lý thanh toán điện tử cho khách hàng nhằm tránh việc lưu trữ trực tiếp thông tin thẻ/tài khoản nhạy cảm trên nền tảng CAB. 
•	Nhà cung cấp dịch vụ thông báo (External Notification Provider):
Hệ thống bên thứ ba hỗ trợ gửi thông báo (SMS, Push Notification, Email...) đến khách hàng và tài xế qua các kênh thông báo. 

d.	Tính kiểm toán (Auditability):
Lưu vết đầy đủ nhật ký (logs) các thao tác quan trọng để phục vụ tra cứu, kiểm tra khi phát sinh sự cố. 
e.	Tính linh hoạt & Khả năng bảo trì (Flexibility & Maintainability):
Kiến trúc hệ thống linh hoạt, cho phép tích hợp thêm phương thức thanh toán mới, mở rộng kênh gửi thông báo hoặc bổ sung loại hình dịch vụ mới trong tương lai mà không phải đập đi xây lại toàn bộ ứng dụng. 

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
