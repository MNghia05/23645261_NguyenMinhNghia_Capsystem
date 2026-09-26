# CONTEXT DỰ ÁN CAB – PHÂN RÃ SUBDOMAIN (DDD)
### Phạm vi đầy đủ theo README_Final.md — trình bày theo form GPT-context.md

---

## 1. Bối cảnh dự án

Tài liệu này phân rã Subdomain cho hệ thống CAB dựa trên **toàn bộ phạm vi nghiệp vụ trong `README_Final.md`**: 13 Use Case (UC01–UC13), 15 Business Requirement (nhóm BR-BOOK, BR-FIN, BR-TRK, BR-OPS, BR-NOTI) và các quy tắc nghiệp vụ ở Bước 10.

Khác với file trước (dựa trên `GPT-context.md`, chỉ 21 FR và 4 service đã chốt), file này giữ **nguyên phạm vi rộng của README**: có Rating, Reporting, Notification, SOS, Location Tracking — những phần không có trong 21 FR đã chốt.

Role: Khách hàng, Tài xế, Nhân viên vận hành, Ban giám đốc, Nhà cung cấp thanh toán, Nhà cung cấp dịch vụ thông báo.

Mục tiêu tài liệu:

1. Functional Requirements (FR) — chuẩn hóa lại từ 13 UC
2. Phân rã Subdomain theo DDD, tiêu chí high-cohesion
3. Đề xuất Service tương ứng cho từng Subdomain
4. Cấu trúc API Documentation dự kiến

---

## 2. Functional Requirements đã chuẩn hóa

Hệ thống có **24 FR**, gom từ 13 UC và 15 BR trong README.

| BR | ID | Chức năng | Mô tả | Role |
|---|---|---|---|---|
| BR-AUTH | FR-01 | Đăng ký tài khoản | Khách hàng hoặc tài xế tạo tài khoản mới. | Khách hàng, Tài xế |
| BR-AUTH | FR-02 | Đăng nhập | Xác thực thông tin để truy cập hệ thống. | Khách hàng, Tài xế, NV vận hành, Ban giám đốc |
| BR-AUTH | FR-03 | Xác thực người dùng | Kiểm tra người dùng đã đăng nhập trước khi dùng chức năng cần tài khoản. | Hệ thống |
| BR-AUTH | FR-04 | Phân quyền | Kiểm soát quyền truy cập chức năng theo vai trò. | Hệ thống |
| BR-AUTH | FR-05 | Cập nhật thông tin cá nhân | Khách hàng, tài xế xem và cập nhật thông tin cá nhân. | Khách hàng, Tài xế |
| BR-BOOK-01 | FR-06 | Đặt xe | Nhập điểm đón, điểm đến, chọn loại xe, xác nhận đặt xe. | Khách hàng |
| BR-BOOK-02 | FR-07 | Tìm tài xế | Xác định tài xế sẵn sàng, phù hợp vị trí và loại xe. | Hệ thống |
| BR-BOOK-02 | FR-08 | Phân công tài xế | Gửi yêu cầu nhận chuyến; nếu từ chối/không phản hồi thì tìm tài xế khác; nếu không còn tài xế thì báo khách hàng. | Hệ thống |
| BR-BOOK-02 | FR-09 | Xử lý yêu cầu chuyến | Tài xế chấp nhận hoặc từ chối yêu cầu chuyến. | Tài xế |
| BR-BOOK-03 | FR-10 | Quản lý chuyến đi | Tạo và cập nhật trạng thái chuyến từ đón khách đến hoàn thành hoặc hủy. | Tài xế, Khách hàng, NV vận hành |
| BR-TRK-01 | FR-11 | Theo dõi hành trình | Hiển thị trạng thái, vị trí tài xế và thời gian dự kiến đến. | Khách hàng, Tài xế, NV vận hành |
| BR-FIN-01 | FR-12 | Tính cước | Tính số tiền dựa trên thông tin chuyến và bảng giá, sau khi chuyến hoàn thành. | Hệ thống |
| BR-FIN-02 | FR-13 | Thanh toán | Hỗ trợ thanh toán tiền mặt hoặc điện tử. | Khách hàng, Nhà cung cấp thanh toán |
| BR-FIN-03 | FR-14 | Quản lý giao dịch | Lưu kết quả thanh toán, xử lý giao dịch thất bại. | Hệ thống |
| BR-NOTI-01 | FR-15 | Gửi thông báo | Gửi thông báo khi có sự kiện quan trọng (đặt xe, nhận chuyến, đến điểm đón, hoàn thành, thanh toán). | Hệ thống, Nhà cung cấp thông báo |
| BR-TRK-02 | FR-16 | Hỗ trợ khẩn cấp (SOS) | Khách hàng hoặc tài xế gửi yêu cầu SOS kèm vị trí hiện tại. | Khách hàng, Tài xế |
| BR-OPS-01 | FR-17 | Quản lý tài xế và phương tiện | Nhân viên vận hành quản lý hồ sơ, phương tiện, trạng thái tài xế. | NV vận hành |
| BR-OPS-02 | FR-18 | Đánh giá chuyến đi | Khách hàng chấm điểm và phản hồi sau khi chuyến hoàn thành. | Khách hàng |
| BR-OPS-03 | FR-19 | Quản lý hỗ trợ / xử lý sự cố | Tiếp nhận, xử lý yêu cầu SOS, chuyến lỗi, giao dịch cần kiểm tra; cập nhật kết quả. | NV vận hành |
| BR-OPS-04 | FR-20 | Xem báo cáo | Tổng hợp số chuyến, doanh thu, tỷ lệ hoàn thành/hủy, hiệu quả tài xế. | Ban giám đốc |

**Bốn FR bổ sung (README có mô tả nhưng chưa tách UC riêng — xem mục 8):**

| BR | ID | Chức năng | Mô tả | Role |
|---|---|---|---|---|
| (chưa có mã) | FR-21 | Bật/tắt trạng thái sẵn sàng | Tài xế chuyển sang sẵn sàng nhận chuyến. | Tài xế |
| (chưa có mã) | FR-22 | Gửi vị trí tài xế | Tài xế cung cấp vị trí để hệ thống tìm tài xế và theo dõi hành trình. | Tài xế |
| (chưa có mã) | FR-23 | Quản lý khách hàng | Nhân viên vận hành xem và quản lý thông tin khách hàng. | NV vận hành |
| (chưa có mã) | FR-24 | Tra cứu lịch sử giao dịch | Nhân viên vận hành tra cứu giao dịch thanh toán. | NV vận hành |

FR-21–24 chưa có UC hoặc BR riêng trong README (chỉ xuất hiện ở mục d.2, d.3, BR-FIN-03), nên đánh dấu để xác nhận trước khi triển khai, đúng nguyên tắc "không tự thêm requirement" trong `GPT-context.md`.

---

## 3. Các quyết định quan trọng về FR

## Khác biệt so với GPT-context.md (bản 21 FR)

* README hỗ trợ **cả tiền mặt và điện tử** (BR-FIN-02), không chỉ tiền mặt.
* README có **Rating (FR-18)**, **Reporting (FR-20)**, **SOS (FR-16)**, **Location Tracking (FR-11, FR-22)** — các phần này không có trong 21 FR đã chốt.
* README có thêm actor **Ban giám đốc**, **Nhà cung cấp thanh toán**, **Nhà cung cấp dịch vụ thông báo**.

## Đánh giá cước và thanh toán

Giữ tách FR-12 (Tính cước) và FR-13 (Thanh toán) làm hai FR riêng, vì README đã tách thành hai BR khác nhau (BR-FIN-01 và BR-FIN-02), khác với context.md gộp tính cước vào bước đặt xe.

## Không tự thêm requirement

Không thêm: hủy chuyến có phí (chỉ có "hủy" đơn giản ở UC04 ngoại lệ 2.1, chưa có chính sách phí — xem mục 10.12), khuyến mãi, điểm thưởng, đăng xuất riêng biệt (README không nêu UC đăng xuất).

---

## 4. Nguyên tắc phân rã Subdomain

**Ba loại Subdomain**

| Loại | Ý nghĩa | Cách xử lý |
|---|---|---|
| Core | Tạo lợi thế cạnh tranh, logic phức tạp | Tự xây, đầu tư thiết kế kỹ nhất |
| Supporting | Cần thiết nhưng không tạo khác biệt | Xây đơn giản |
| Generic | Bài toán chung đã có lời giải chuẩn | Dùng giải pháp có sẵn |

**Năm tiêu chí High-Cohesion:** ngôn ngữ thống nhất; cùng lý do thay đổi; bất biến nghiệp vụ nằm chung; mỗi dữ liệu một chủ sở hữu; giao tiếp qua sự kiện/API, không chạm model nội bộ nhau.

Không cắt theo actor, theo từng UC riêng lẻ, hoặc theo 5 nhóm BR nguyên trạng — vì BR-OPS gộp bốn việc không liên quan (tài xế, đánh giá, hỗ trợ, báo cáo) và BR-TRK gộp vị trí với SOS, đều làm giảm cohesion.

---

## 5. Subdomain đã chốt (10)

| # | Subdomain | Loại | FR |
|---|---|---|---|
| 1 | Identity & Access | Generic | FR-01, 02, 03, 04, 05 |
| 2 | Trip Management | Core | FR-06, 09, 10 |
| 3 | Driver Dispatch | Core | FR-07, 08, 21 |
| 4 | Pricing | Supporting | FR-12 |
| 5 | Payment | Supporting | FR-13, 14, 24 |
| 6 | Driver & Vehicle | Supporting | FR-17 |
| 7 | Location Tracking | Supporting | FR-11, 22 |
| 8 | Support & Safety | Supporting | FR-16, 19 |
| 9 | Rating | Supporting | FR-18 |
| 10 | Reporting | Supporting | FR-20 |

Notification (FR-15) và Customer Profile (FR-05, FR-23) được xử lý riêng — xem mục 6.

---

## 6. Vì sao không tạo Subdomain riêng cho một số phần

## Không tách Notification thành Subdomain nghiệp vụ độc lập

FR-15 chỉ chuyển tiếp sự kiện đến Nhà cung cấp dịch vụ thông báo (actor bên ngoài), không chứa logic nghiệp vụ đặt xe hay thanh toán. Đây là **Generic Subdomain hạ tầng**: các Subdomain khác phát sự kiện, Notification chỉ lắng nghe và gửi. Vẫn liệt kê là 1 module/service riêng để dễ thay nhà cung cấp, nhưng không nằm trong 10 Subdomain nghiệp vụ ở mục 5.

## Customer Profile không tách khỏi Identity & Access

README không có UC riêng cho "quản lý khách hàng" của Nhân viên vận hành (chỉ nhắc ở mục d.3, chưa có BR/UC), và FR-05 (khách tự cập nhật) là thao tác đơn giản trên cùng một entity tài khoản. Gộp vào Identity & Access; nếu sau này "quản lý khách hàng" (FR-23) phát triển thêm nghiệp vụ riêng (ví dụ: khóa tài khoản, phân loại khách hàng), nên tách ra.

## Không có Operation Subdomain

Nhân viên vận hành là **Actor**, dùng lại các Subdomain đã có: Driver & Vehicle (FR-17, 23), Trip Management (theo dõi chuyến), Support & Safety (FR-19), Payment (FR-24 tra cứu).

---

## 7. Chi tiết Subdomain và dữ liệu sở hữu

| Subdomain | Sở hữu | Ghi chú cohesion |
|---|---|---|
| Identity & Access | Tài khoản, đăng nhập, vai trò, quyền, hồ sơ cá nhân cơ bản | Không giữ dữ liệu nghiệp vụ khác |
| Trip Management | Chuyến đi, trạng thái vòng đời, điểm đón/đến; chỉ giữ ID khách và tài xế | Cùng máy trạng thái, cùng bất biến "một chuyến mở tại một thời điểm" |
| Driver Dispatch | Yêu cầu ghép, lời mời, danh sách ứng viên, trạng thái sẵn sàng của tài xế | Tách khỏi Trip vì đổi thường xuyên (tiêu chí ưu tiên, timeout) |
| Pricing | Bảng giá, cước từng chuyến | Đổi theo chính sách kinh doanh, khác lý do đổi của Payment |
| Payment | Giao dịch (tiền mặt/điện tử), trạng thái, không lưu dữ liệu thẻ | Không biết cách tính cước, chỉ nhận số tiền |
| Driver & Vehicle | Hồ sơ tài xế, phương tiện, trạng thái hồ sơ (hoạt động/khóa) | Khác "trạng thái sẵn sàng" (thuộc Dispatch) |
| Location Tracking | Dòng vị trí, hành trình, ETA | Dữ liệu tần suất cao, chính sách lưu trữ riêng |
| Support & Safety | Vụ việc (SOS, chuyến lỗi, giao dịch cần kiểm tra), trạng thái xử lý | Cùng vòng đời "tiếp nhận → xử lý → kết quả" |
| Rating | Đánh giá gắn tripId/driverId, điểm tổng hợp | Vòng đời ngắn, sau khi chuyến hoàn thành |
| Reporting | Read model: số chuyến, doanh thu, tỷ lệ, hiệu quả tài xế | Chỉ đọc, cập nhật qua sự kiện, không có bất biến nghiệp vụ |

---

## 8. Sự kiện chính giữa các Subdomain

```text
Trip: yêu cầu đặt xe tạo ──► Driver Dispatch, Notification
Driver Dispatch: đã ghép / không tìm được ──► Trip, Notification
Trip: chuyến hoàn thành ──► Pricing, Rating, Reporting, Notification
Trip: chuyến hủy/lỗi ──► Pricing (phí hủy, nếu có), Support, Reporting
Pricing: đã tính cước ──► Payment
Payment: kết quả thanh toán ──► Notification, Reporting, Support (nếu cần kiểm tra)
Location Tracking: vị trí cập nhật ──► Driver Dispatch
Driver & Vehicle: tài xế bị khóa/đổi xe ──► Driver Dispatch
Rating: tài xế được đánh giá ──► Reporting
```

Ngoại lệ: khi tạo SOS (FR-16), Support & Safety truy vấn trực tiếp vị trí hiện tại từ Location Tracking, không qua sự kiện.

---

## 9. Cấu trúc API Docs dự kiến (nếu theo microservices)

Nếu áp dụng đúng cấu trúc `GPT-context.md` (mỗi service một file OpenAPI), phạm vi README cần nhiều hơn 4 service. Đề xuất nhóm 10 Subdomain thành **7 service**:

```text
api-docs/
├── auth.openapi.yaml         (Identity & Access)
├── user.openapi.yaml         (Driver & Vehicle, Customer Profile)
├── booking.openapi.yaml      (Trip Management giai đoạn đặt xe, Driver Dispatch, Pricing)
├── trip.openapi.yaml         (Trip Management giai đoạn thực hiện, Location Tracking, Payment)
├── support.openapi.yaml      (Support & Safety, Rating)
├── notification.openapi.yaml (Notification)
└── reporting.openapi.yaml    (Reporting)
```

Đây là đề xuất, chưa phải quyết định chốt — cần xác nhận trước khi tách nhiều hơn 4 service so với `GPT-context.md` hiện tại (xem mục 10).

---

## 10. Vấn đề cần làm rõ

Từ mục 10.12 của README, cộng thêm các điểm phát sinh khi phân rã:

1. Công thức tính cước cụ thể — thuộc Pricing.
2. Tiêu chí ưu tiên tài xế, thời gian phản hồi, số lần tìm lại — thuộc Driver Dispatch.
3. Chính sách hủy chuyến và phí hủy — điều kiện hủy thuộc Trip Management, phí hủy thuộc Pricing.
4. Cách xử lý khi mất kết nối mạng — Location Tracking và Trip Management.
5. Thời gian lưu trữ dữ liệu — từng Subdomain, ưu tiên Location Tracking.
6. Quyền chi tiết của từng loại nhân viên vận hành — Identity & Access.
7. **FR-21–24 chưa có UC/BR gốc** — cần xác nhận trước khi đưa vào thiết kế chính thức.
8. **Có tách thành 7 service hay giữ 4 service** (gộp Rating/Reporting/Notification/Support vào Trip Service như context.md đã làm với phạm vi hẹp hơn) — cần quyết định trước khi viết OpenAPI.

---

## 11. Trạng thái hiện tại của công việc

Đã hoàn thành:

* [x] Chuẩn hóa 24 FR từ 13 UC và 15 BR trong README
* [x] Phân rã 10 Subdomain theo 5 tiêu chí high-cohesion
* [x] Xác định sự kiện chính giữa các Subdomain
* [x] Đề xuất nhóm 10 Subdomain vào 7 service
* [x] Liệt kê 8 điểm cần làm rõ

Đang chờ xác nhận:

* [ ] Có mở rộng từ 4 service (theo GPT-context.md) lên 7 service hay không
* [ ] Nguồn gốc FR-21–24 (bật/tắt sẵn sàng, gửi vị trí, quản lý khách hàng, tra cứu giao dịch)
* [ ] 8 điểm ở mục 10.12 gốc

## Điểm tiếp tục lần sau

Nếu chọn mở rộng theo bản này (7 service), viết API docs theo thứ tự: `auth` → `user` → `booking` → `trip` → `support` → `notification` → `reporting`.

Nếu giữ đúng 4 service đã chốt trong `GPT-context.md`, dùng file `CAB-DDD-Subdomain-Final.md` (bản 8 subdomain, 21 FR) làm chuẩn, và coi các Subdomain thêm ở đây (Rating, Reporting, Notification, SOS, Location Tracking) là mở rộng dự phòng khi có thêm requirement.
