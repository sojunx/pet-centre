# Pet Health Centre (Clinic Management System)

> Ref URL: https://pethealthcentre.vn

## General

### Who Uses This?

- **Guest** – Người dùng chưa đăng ký, muốn tìm hiểu thông tin phòng khám, đội ngũ bác sĩ và các dịch vụ.
- **Customer** – Chủ thú cưng đã có tài khoản, cần đặt lịch khám và theo dõi hồ sơ sức khỏe của pet.
- **Staff** – Lễ tân/Quản lý phòng khám: Điều phối lịch hẹn, gán ca cho bác sĩ, quản lý kho thuốc và thanh toán viện phí.
- **Vet** – Bác sĩ thú y: Khám bệnh, ghi nhận hồ sơ bệnh án và kê đơn thuốc.

### What Is the Problem?

- Khách hàng gọi điện đặt lịch thủ công dễ dẫn đến sai sót, trùng lịch hoặc phải chờ đợi lâu khi đến phòng khám.
- Sổ khám bệnh vật lý dễ bị mất, bác sĩ khó tra cứu lại lịch sử bệnh nền hoặc các loại thuốc thú cưng đã dùng trước đó (nguy cơ dị ứng thuốc).
- Quy trình tính tiền thủ công (cộng tiền khám + tiền thuốc) mất thời gian và khó kiểm soát doanh thu/tồn kho.

### Why Is This Useful?

- **Trải nghiệm mượt mà:** Khách chủ động đặt lịch theo khung giờ, phòng khám điều phối bác sĩ hợp lý để giảm thời gian chờ.
- **Bệnh án điện tử (EHR):** Lưu trữ tập trung mọi chỉ số sức khỏe, chẩn đoán, đơn thuốc của thú cưng qua từng lần khám.
- **Minh bạch tài chính & Tồn kho:** Mọi dịch vụ và thuốc kê đơn đều tự động đổ về một Hóa đơn (Invoice) duy nhất để thanh toán chính xác, đồng thời tự động trừ tồn kho.

---

## Tech Stack

| Layer      | Technology                        |
|------------|-----------------------------------|
| Frontend   | Next.js                           |
| Backend    | Go                                |
| Database   | PostgreSQL                        |
| Auth       | JWT                               |
| Deployment | Homelab, AWS                      |

---

## Specifications

### Roles

| Role       | Description |
|------------|-------------|
| Guest      | Khách vãng lai; xem thông tin chung và bảng giá dịch vụ |
| Customer   | Khách hàng; quản lý pet, đặt lịch khám, xem bệnh án và hóa đơn |
| Staff      | Lễ tân; duyệt lịch, gán bác sĩ, xuất hóa đơn, quản lý kho thuốc |
| Vet        | Bác sĩ; xem lịch làm việc, khám bệnh, điền bệnh án, kê đơn |

---

### User Stories

#### Guest
- Tôi muốn xem thông tin phòng khám (địa chỉ, giờ mở cửa, liên hệ).
- Tôi muốn xem danh sách các dịch vụ (Khám tổng quát, Tiêm phòng, Triệt sản...) và bảng giá tham khảo.

#### Customer
- Tôi muốn đăng ký/đăng nhập để sử dụng dịch vụ.
- Tôi muốn tạo và quản lý hồ sơ thú cưng (tên, loài, giống, tuổi, cân nặng ban đầu).
- Tôi muốn đặt lịch khám (chọn Dịch vụ + Ngày giờ) để không phải chờ đợi.
- Tôi muốn xem lại Lịch sử khám bệnh (Triệu chứng, Bác sĩ chẩn đoán, Đơn thuốc) của pet nhà tôi.
- Tôi muốn xem chi tiết Hóa đơn viện phí sau khi khám xong.

#### Staff
- Tôi muốn xem danh sách lịch hẹn trong ngày để chủ động sắp xếp.
- Tôi muốn xác nhận lịch hẹn và **gán Bác sĩ (Assign Vet)** cho ca khám đó.
- Tôi muốn xem/cập nhật danh mục Thuốc & Vật tư y tế (tên thuốc, số lượng tồn kho, giá bán).
- Tôi muốn thu tiền khách hàng dựa trên Hóa đơn (gồm tiền dịch vụ + tiền thuốc) và chuyển trạng thái thành "Đã thanh toán".

#### Vet
- Tôi muốn xem danh sách các ca khám đã được Staff gán cho tôi trong ngày hôm nay.
- Tôi muốn xem lịch sử bệnh án của một thú cưng trước khi bắt đầu khám.
- Tôi muốn tạo Bệnh án mới sau khi khám xong (Ghi nhận cân nặng, nhiệt độ, triệu chứng, chẩn đoán).
- Tôi muốn kê đơn thuốc cho thú cưng (chọn từ danh mục kho thuốc của phòng khám).

---

## Features

### Must Have (MVP)

**1. Auth & Profiles**
- Register, Login, Logout (JWT).
- Quản lý thông tin cá nhân (Customer, Staff, Vet).

**2. Pet Management**
- CRUD Pet Profile (Tên, loài, giống, ngày sinh/tuổi).
- Liệt kê danh sách pet theo tài khoản Customer.

**3. Appointment & Workflow (Lõi hệ thống)**
- Khách hàng đặt lịch (Chọn Dịch vụ + Khung giờ).
- State Machine cho Lịch hẹn: `Pending` (Chờ duyệt) -> `Confirmed` (Đã gán Bác sĩ) -> `In_Progress` (Đang khám) -> `Completed` (Khám xong, chờ thanh toán).
- Staff quản lý lịch hẹn: Xác nhận, hủy, gán Bác sĩ.

**4. Medical Records & Pharmacy (Bệnh án & Thuốc)**
- Bảng danh mục Thuốc (Tên, đơn vị, giá, số lượng tồn - CRUD bởi Staff).
- Vet điền form Bệnh án: Sinh hiệu (Cân nặng, Nhiệt độ), Chẩn đoán, Lời khuyên.
- Vet kê đơn: Chọn thuốc từ DB, nhập số lượng, liều dùng (sáng 1 viên, tối 1 viên...).

**5. Billing & Invoicing (Viện phí)**
- Hệ thống tự động tạo Invoice khi lịch hẹn chuyển sang trạng thái `Completed`.
- Total = Phí dịch vụ khám + Tổng tiền đơn thuốc.
- Staff xác nhận thu tiền và đổi trạng thái Invoice thành `Paid`. Tự động trừ số lượng tồn kho của thuốc.

### Should Have (Phase 2)
- Tích hợp cổng thanh toán (VNPay / Momo) để khách trả viện phí online qua điện thoại lúc đang ngồi chờ.
- Upload file đính kèm cho bệnh án (Ảnh chụp X-Quang, file PDF kết quả xét nghiệm máu).
- Hệ thống Notification (Gửi email/SMS nhắc lịch khám ngày mai, nhắc lịch tiêm phòng định kỳ).
- Realtime chat (Staff ↔ Customer).

### Nice to Have (Future)
- Dashboard Thống kê cho Quản lý (Doanh thu theo ngày/tháng, số lượng ca khám, bác sĩ nào đông khách nhất).
- Quản lý ca làm việc (Shift Management) phức tạp cho đội ngũ Bác sĩ/Lễ tân.
- Hệ thống theo dõi nội trú (Dành cho thú cưng phải nằm viện qua đêm).

---

## Success Metrics

- [ ] Customer có thể thêm Pet và đặt lịch hẹn thành công.
- [ ] Staff thấy được lịch hẹn, có thể gán Vet phụ trách.
- [ ] Vet thấy lịch được gán, hoàn tất điền Bệnh án và kê Đơn thuốc.
- [ ] Hệ thống tự động sinh Hóa đơn (Invoice) chính xác dựa trên Dịch vụ và Đơn thuốc.
- [ ] Staff xác nhận thanh toán thành công và kho thuốc tự động trừ đi số lượng đã kê đơn.
