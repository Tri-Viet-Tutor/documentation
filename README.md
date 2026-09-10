# VietTriTutor System Documentation

Tài liệu thiết kế hệ thống và quy tắc nghiệp vụ cho dự án **Trung tâm Gia sư VietTriTutor**.

---

## Thư mục Tài liệu Nghiệp vụ (`01-Business-Logic`)

Hệ thống được chuẩn hóa với các Quy tắc nghiệp vụ (Business Rules) cốt lõi bao gồm:

1. **[01. Vai trò Người dùng & Logic Gợi ý Gia sư](file:///c:/Edisk/dow/Tai_lieu/ky7/sba/viettritutor/documentation/01-Business-Logic/01-User-Roles-and-Permissions.md)**
   - Phân quyền: Admin Trung tâm, Gia sư Hệ thống (Official), Gia sư Tự do (Freelance), Phụ huynh/Học viên.
   - Thuật toán ưu tiên Recommend Gia sư thuộc Trung tâm.
   - Cơ chế mua Gói dịch vụ (Subscription Package).

2. **[02. Quy tắc Tính Học Phí & Gói Dịch Vụ](file:///c:/Edisk/dow/Tai_lieu/ky7/sba/viettritutor/documentation/01-Business-Logic/02-Pricing-and-Subscription-Rules.md)**
   - Công thức tính học phí tự động: Lớp 1-1 vs Lớp Nhóm (Nhóm 5 học viên).
   - Hệ số giảm giá cho học viên & tăng thu nhập cho gia sư theo quy mô nhóm.
   - Phân biệt đơn giá Online (giảm 15%) vs Offline.

3. **[03. Quản lý Lịch Học, Validation Trùng Lịch & Dời Lịch](file:///c:/Edisk/dow/Tai_lieu/ky7/sba/viettritutor/documentation/01-Business-Logic/03-Scheduling-and-Conflict-Validation.md)**
   - Hard Conflict Validation: Thuật toán bắt trùng lịch khi Gia sư / Học viên đăng Post.
   - Quy trình xin nghỉ & dời lịch (Reschedule Workflow) theo mốc 24 tiếng.
   - Vai trò can thiệp xếp lịch bù của Trung tâm Admin.

4. **[04. Quy trình Khớp Lớp & Lộ trình Tính năng Video Call](file:///c:/Edisk/dow/Tai_lieu/ky7/sba/viettritutor/documentation/01-Business-Logic/04-Matching-and-Class-Management.md)**
   - Vòng đời lớp học từ Lúc Đăng bài $\to$ Xếp lịch $\to$ Điểm danh $\to$ Hoàn thành.
   - Phân biệt điểm danh Lớp Online & Offline.
   - Lộ trình phát triển Video Call: MVP (Third-party SDK: Agora/Jitsi/Daily) $\to$ Nâng cao (Tự build Mediasoup SFU + Whiteboard + Cloud Recording).