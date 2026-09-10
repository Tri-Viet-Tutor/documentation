# Business Rule 02: Pricing Engine & Subscription Packages

## 1. Mô hình Phí & Gói Dịch Vụ cho Gia Sư (Subscription / Credit Rules)

Gia sư kiếm tiền thông qua nhận lớp, nhưng cần duy trì **Gói dịch vụ (Subscription)** hoặc trả **Phí kết nối (Platform Fee)** cho Trung tâm.

### 1.1. Cấu trúc Gói Dịch Vụ (Service Packages)
Trung tâm đại diện Admin cung cấp các loại gói dịch vụ sau:

| Tên gói dịch vụ | Loại phí | Quyền lợi & Hạn ngạch | Đối tượng áp dụng |
| :--- | :--- | :--- | :--- |
| **Basic / Free** | 0 VNĐ | - Nhận tối đa 1 lớp/tháng.<br>- Phí hoa hồng kết nối: 15% / tổng giá trị hợp đồng lớp học. | Gia sư Tự do mới đăng ký |
| **Pro Tutor (Tháng)** | 200,000 VNĐ / tháng | - Nhận lớp không giới hạn.<br>- Giảm phí hoa hồng kết nối xuống 5%.<br>- Ưu tiên xuất hiện trên bảng tin tìm kiếm. | Gia sư Tự do chuyên nghiệp |
| **Official Tutor VIP** | Miễn phí gói (Do TT cấp) | - Nhận lớp ưu tiên từ Trung tâm xếp.<br>- Phí hoa hồng kết nối: 0% (Ăn lương trực tiếp từ Trung tâm hoặc hưởng 100% học phí theo quy ước hợp đồng Trung tâm). | Gia sư thuộc Hệ thống |

---

## 2. Công Thức Tính Học Phí Lớp Học (Pricing Logic)

Học phí được tính toán tự động theo công thức đa biến dựa trên các tham số: **Số lượng học viên (Lớp 1-1 hay Lớp Nhóm)**, **Hình thức (Online hay Offline)**, **Cấp độ bài học/Môn học** và **Trình độ gia sư**.

### 2.1. Đơn giá cơ bản theo giờ (Base Hourly Rate - $P_{\text{base}}$)
- Đơn giá cơ bản $P_{\text{base}}$ được thiết lập dựa trên cấp độ lớp (VD: Cấp 1, Cấp 2, Cấp 3, Luyện thi ĐH) và danh hiệu Gia sư (Sinh viên, Giảng viên/Giáo viên, Gia sư Hệ thống VIP).

### 2.2. Công thức tổng quát tính Học phí 1 buổi ($T_{\text{session}}$)

$$T_{\text{session}} = P_{\text{base}} \times K_{\text{mode}} \times K_{\text{group}}$$

Trong đó:
- $P_{\text{base}}$: Đơn giá gốc cho 1 học viên / 1 giờ học (Offline).
- $K_{\text{mode}}$: Hệ số hình thức học (Online / Offline).
- $K_{\text{group}}$: Hệ số quy mô nhóm học viên.

---

### 2.3. Chi tiết các Hệ số Tính toán (Pricing Multipliers)

#### A. Hệ số Hình Thức Học ($K_{\text{mode}}$)
- **Offline (Học trực tiếp tại nhà/trung tâm)**: $K_{\text{mode}} = 1.0$ (Bao gồm chi phí đi lại của gia sư).
- **Online (Học qua Video Call hệ thống)**: $K_{\text{mode}} = 0.85$ (Giảm 15% chi phí do không mất phí di chuyển).

#### B. Hệ số Quy Mô Lớp Học ($K_{\text{group}}$)
Quy tắc tính học phí theo quy mô lớp áp dụng nguyên tắc **Chiết khấu theo số lượng (Volume Discount for Students & Increased Tutor Yield)**:
- **Lớp 1-on-1 (1 Học viên)**: 
  - $K_{\text{group}} = 1.0$
  - Mỗi bên trả/nhận đúng 100% đơn giá gốc.

- **Lớp Nhóm (Group Class - Ví dụ: Nhóm 5 học viên)**:
  - **Tổng học phí cả nhóm trả ($T_{\text{group}}$)**: Áp dụng công thức lũy tiến giảm dần cho từng học viên bổ sung.
  - Hệ số tổng nhóm $K_{\text{group}}(N) = 1 + (N - 1) \times \alpha$ (với $\alpha = 0.5$ là hệ số tăng thêm cho mỗi học viên thứ 2 trở đi).
  - **Ví dụ với Nhóm 5 học viên ($N = 5$)**:
    $$K_{\text{group}}(5) = 1 + (5 - 1) \times 0.5 = 3.0$$
  - **Tính tiền cụ thể**:
    - **Tổng học phí lớp nhận từ 5 học viên**: $3.0 \times P_{\text{base}}$ (Gia sư thu gấp 3 lần so với dạy 1-1).
    - **Học phí MỖI HỌC VIÊN phải trả**: 
      $$\text{Fee Per Student} = \frac{3.0 \times P_{\text{base}}}{5} = 0.6 \times P_{\text{base}}$$
      *(Mỗi học viên trong nhóm 5 chỉ cần trả **60%** giá tiền so với học 1-1 $\to$ Tiết kiệm 40% chi phí).*

---

## 3. Bảng Ví Dụ Minh Họa Tính Tiền (Pricing Matrix Case Study)

*Giả định Đơn giá gốc $P_{\text{base}} = 200,000$ VNĐ/giờ (Lớp Cấp 3).*

| Số lượng HV ($N$) | Hình thức | $K_{\text{mode}}$ | $K_{\text{group}}$ | Tổng học phí Lớp/Giờ | Học phí mỗi HV trả/Giờ | Thu nhập Gia sư/Giờ (Basic) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **1 (Lớp 1-1)** | Offline | 1.0 | 1.0 | 200,000 VNĐ | **200,000 VNĐ** | 170,000 VNĐ (trừ 15% phí) |
| **1 (Lớp 1-1)** | Online | 0.85 | 1.0 | 170,000 VNĐ | **170,000 VNĐ** | 144,500 VNĐ (trừ 15% phí) |
| **5 (Nhóm 5)** | Offline | 1.0 | 3.0 | 600,000 VNĐ | **120,000 VNĐ** (-40%) | 510,000 VNĐ (trừ 15% phí) |
| **5 (Nhóm 5)** | Online | 0.85 | 3.0 | 510,000 VNĐ | **102,000 VNĐ** (-40%) | 433,500 VNĐ (trừ 15% phí) |
