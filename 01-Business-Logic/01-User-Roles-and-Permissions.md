# Business Rule 01: User Roles, System Status & Recommendation Logic

## 1. Tổng quan các vai trò trong hệ thống (User Roles)

Hệ thống VietTriTutor định nghĩa 4 nhóm người dùng chính:

| Vai trò (Role) | Mã định danh | Mô tả & Trách nhiệm |
| :--- | :--- | :--- |
| **Admin Trung Tâm** | `ROLE_ADMIN` | Đại diện cho Trung tâm gia sư. Quản trị hệ thống, phê duyệt gia sư, hỗ trợ xếp lịch, can thiệp xử lý tranh chấp/dời lịch, quản lý gói dịch vụ và cài đặt tỷ lệ tính tiền. |
| **Gia sư Hệ thống** | `ROLE_OFFICIAL_TUTOR` | Gia sư thuộc quản lý trực tiếp của Trung tâm (đã kiểm định bằng cấp, hợp đồng, hồ sơ). Được hệ thống **ưu tiên hiển thị (Recommend)** khi phụ huynh/học viên tìm kiếm hoặc đăng bài. |
| **Gia sư Tự do** | `ROLE_FREELANCE_TUTOR` | Gia sư tự do đăng ký trên nền tảng. Quản lý lịch rảnh cá nhân, mua các gói dịch vụ (Service Package) để có quyền nhận lớp/đăng bài. |
| **Người học / Phụ huynh** | `ROLE_STUDENT` | Người có nhu cầu tìm gia sư cho bản thân hoặc con em. Tạo yêu cầu tìm gia sư (Post), xem lịch rảnh gia sư, đặt lịch học và thanh toán. |

---

## 2. Quy tắc Gói dịch vụ & Quyền hạn Gia sư (Subscription & Monetization Rules)

### 2.1. Mô hình doanh thu từ Gia sư
- Gia sư (đặc biệt là Gia sư tự do) **phải mua Gói dịch vụ (Subscription Package / Token Credit)** để sử dụng các tính năng cao cấp.
- **Quy tắc mua gói**:
  1. **Gói dùng thử / Miễn phí (Free Tier)**: Giới hạn nhận 1 lớp/tháng, chỉ đăng bài rảnh cơ bản.
  2. **Gói Theo Tháng / Theo Lượt (Service Package)**: 
     - Mở khóa tính năng ứng tuyển/nhận lớp không giới hạn.
     - Cho phép kích hoạt tính năng **Độ ưu tiên hiển thị (Priority Listing)**.
     - Cho phép đăng post mở lớp nhóm (Group Class).

### 2.2. Phân biệt Gia sư Hệ thống vs Gia sư Tự do
- **Gia sư Hệ thống (`OFFICIAL`)**:
  - Được Trung tâm gia sư bảo chứng chất lượng (badge "Gia sư Trung tâm").
  - Được hỗ trợ xếp lịch trực tiếp từ Admin nếu Học viên nhờ Trung tâm tìm giúp.
  - Được cộng điểm trọng số trong thuật toán Recommend.
- **Gia sư Tự do (`FREELANCE`)**:
  - Tự quản lý lịch rảnh 100%.
  - Cần duy trì Gói dịch vụ còn hiệu lực (`ACTIVE`) mới được ứng tuyển/nhận bài đăng từ Học viên.

---

## 3. Thuật toán & Quy tắc Recommend Gia sư (Recommendation Business Logic)

Khi Phụ huynh / Học viên tìm kiếm gia sư hoặc tạo một yêu cầu tìm gia sư (Post), hệ thống trả về danh sách gợi ý theo thứ tự ưu tiên (Ranking Score):

$$\text{Total Score} = W_1 \cdot \text{OfficialStatus} + W_2 \cdot \text{ScheduleMatch} + W_3 \cdot \text{RatingScore} + W_4 \cdot \text{PackageTier}$$

### Quy tắc xếp hạng (Ranking Rules):
1. **Trọng số Gia sư Hệ thống ($W_1 = 40\%$)**: 
   - Gia sư thuộc Trung tâm (`OFFICIAL`) tự động nhận điểm tối đa cho tiêu chí này.
2. **Khớp Lịch Học ($W_2 = 30\%$)**:
   - Khớp 100% khung giờ rảnh phụ huynh yêu cầu $\to$ Điểm tối đa.
   - Nếu bị trùng lịch dù chỉ 1 buổi $\to$ Loại khỏi danh sách Recommend (Score = 0).
3. **Đánh giá & Review ($W_3 = 20\%$)**:
   - Số sao trung bình (1-5 stars) và tỷ lệ hoàn thành lớp học.
4. **Gói Dịch Vụ / Badge Vip ($W_4 = 10\%$)**:
   - Gia sư tự do có mua gói dịch vụ cao cấp được ưu tiên đẩy bài hiển thị trên gia sư tự do gói thường.
