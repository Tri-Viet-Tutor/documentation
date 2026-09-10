# Business Rule 02: Course Pricing, Payroll & Group Class Rules

## 1. Cơ chế Học Phí Khóa Học (Course Fee Structure)

### 1.1. Giá Khóa học do Admin Thiết lập (Admin-Defined Pricing)
- Học phí được tính **theo trọn gói Khóa học** (Một khóa học kéo dài nhiều tháng, bao gồm tổng số buổi học nhất định).
- Admin Trung tâm trực tiếp cấu hình Giá tiền cho từng Khóa học ($P_{\text{course}}$) dựa trên Cấp học (Cấp 1, Cấp 2, Cấp 3), Môn học và Quy mô lớp.
- Học viên thanh toán 100% Học phí Khóa học khi đăng ký mua khóa học.

### 1.2. Công thức Học phí cho Lớp Nhóm (Group Class Pricing)
Đơn giá Khóa học ($P_{\text{course}}$) áp dụng các quy tắc quy mô lớp như sau:

- **Lớp 1-on-1 (1 Học viên)**: Học viên đóng 100% Giá Khóa học 1-1 chuẩn.
- **Lớp Nhóm (Group Class - Từ 2 đến 8 Học viên)**:
  - Học phí trên mỗi Học viên ($P_{\text{student}}$) được chiết khấu giảm dần theo quy mô nhóm so với lớp 1-1:
    $$P_{\text{student}} = P_{\text{1on1\_base}} \times \left(1 - \text{Discount}_{\text{group}}\right)$$
  - *Quy định chiết khấu nhóm*:
    - **Lớp 2 - 3 Học viên**: Chiết khấu 20% học phí/học viên.
    - **Lớp 4 - 8 Học viên**: Chiết khấu 35% - 40% học phí/học viên.

---

## 2. Quy tắc Quy mô Lớp Nhóm (Group Class Capacity Rules)

Dự án quy định chặt chẽ giới hạn sĩ số cho mọi Lớp Nhóm mở trên hệ thống:

| Chỉ số Quy mô | Giá trị | Quy tắc Xử lý Nghiệp vụ |
| :--- | :---: | :--- |
| **Sĩ số Tối đa (Max Capacity)** | **8 Học viên** | Hệ thống tự động khóa đăng ký (Full Slot) khi lớp đạt đủ 8 học viên. Không cho phép nhận thêm. |
| **Sĩ số Tối thiểu (Min Capacity)** | **2 Học viên** | Đến mốc thời hạn chốt mở lớp (vd: 3 ngày trước ngày khai giảng):<br>- Nếu sĩ số $\ge 2$: Lớp đủ điều kiện kích hoạt, Trung tâm phân công Gia sư.<br>- Nếu sĩ số $< 2$ (chỉ có 1 HV): Hệ thống báo cho Admin để dời ngày khai giảng hoặc hoàn tiền/chuyển lớp cho học viên. |

---

## 3. Quy tắc Lương Gia Sư (Tutor Payroll Rules)

- **Hình thức trả lương**: Gia sư nhận **Lương cố định theo tháng** từ Trung tâm.
- Lương tháng của gia sư được tính bằng:
  $$\text{Lương Tháng} = \text{Lương Cứng Hợp Đồng} + \left(\text{Số Ca Dạy Thực Tế} \times \text{Đơn Giá Ca Dạy}\right)$$
- Không phụ thuộc vào việc lớp học đó là Cấp 1, Cấp 2 hay Cấp 3 (vì giá khóa học đã do Admin quản lý và thu về Trung tâm).
