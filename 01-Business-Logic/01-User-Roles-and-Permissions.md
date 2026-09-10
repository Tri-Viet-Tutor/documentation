# Business Rule 01: User Roles & Core Management Logic

## 1. Tổng quan các vai trò trong hệ thống (User Roles)

Hệ thống VietTriTutor định nghĩa 3 nhóm người dùng chính (Tất cả gia sư đều thuộc quản lý của Trung tâm):

| Vai trò (Role) | Mã định danh | Mô tả & Trách nhiệm |
| :--- | :--- | :--- |
| **Admin Trung Tâm** | `ROLE_ADMIN` | Đại diện cho Trung tâm gia sư. Tạo và quản lý Khóa học, cấu hình học phí Khóa học, phân công/xếp gia sư vào các ca học của lớp, trả lương tháng cho Gia sư, can thiệp xử lý dời lịch/xin nghỉ. |
| **Gia sư Trung Tâm** | `ROLE_TUTOR` | Gia sư thuộc quản lý 100% của Trung tâm. Đã được kiểm định bằng cấp/hợp đồng. Quản lý lịch rảnh cá nhân, nhận phân công ca dạy từ Trung tâm, thực hiện giảng dạy và điểm danh. Hưởng lương cứng/lương theo tháng từ Trung tâm. |
| **Học viên / Phụ huynh** | `ROLE_STUDENT` | Tìm kiếm và đăng ký các Khóa học do Trung tâm mở. Chọn ca học (Lịch 2-4-6 hoặc 3-5-7, ca theo giờ), thanh toán học phí theo Khóa học và tham gia lớp. |

---

## 2. Mô hình Quản lý & Doanh thu Trung tâm

### 2.1. Quản lý Gia sư Tập trung (Centralized Tutor Management)
- **Không có Gia sư Tự do (Freelance)** trên hệ thống.
- Trung tâm chịu trách nhiệm xét duyệt tuyển dụng, phân công giảng dạy và chi trả **Lương cố định theo tháng** cho Gia sư dựa trên số ca dạy hoặc hợp đồng lao động.

### 2.2. Mô hình Khóa học & Đóng Học phí
- **Không bán gói dịch vụ (Subscription)** cho gia sư.
- Doanh thu Trung tâm đến từ **Học phí Khóa học** do Học viên đóng khi đăng ký.
- Admin Trung tâm có toàn quyền khởi tạo Khóa học, thiết lập tổng học phí Khóa học, thời lượng (số tháng/số buổi) và tạo các Ca học (Slots).
