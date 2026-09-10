# VietTriTutor System Documentation

Tài liệu thiết kế hệ thống và quy tắc nghiệp vụ cho dự án **Trung tâm Gia sư VietTriTutor**.

## Cấu trúc Thư mục Tài liệu (Directory Structure)

```text
documentation/
├── README.md
├── 00-Product-Definition/
└── 01-Business-Logic/
    ├── 01-User-Roles-and-Permissions.md
    ├── 02-Pricing-and-Subscription-Rules.md
    ├── 03-Scheduling-and-Conflict-Validation.md
    └── 04-Matching-and-Class-Management.md
```

### Mô tả Thư mục & Tài liệu:

- **`00-Product-Definition/`**: Thư mục chứa tài liệu định nghĩa sản phẩm, tầm nhìn và yêu cầu bài toán tổng quan.
- **`01-Business-Logic/`**: Thư mục chứa các quy tắc nghiệp vụ cốt lõi:
  - **`01-User-Roles-and-Permissions.md`**: Định nghĩa vai trò (Admin Trung tâm, Gia sư Trung tâm, Học viên) và mô hình quản lý tập trung.
  - **`02-Pricing-and-Subscription-Rules.md`**: Quy tắc giá Khóa học, cơ chế lương tháng cho Gia sư và quy mô lớp nhóm (2 - 8 học viên).
  - **`03-Scheduling-and-Conflict-Validation.md`**: Quy tắc lịch học (2-4-6, 3-5-7), thuật toán chặn trùng lịch khi xếp gia sư và quy trình dời lịch.
  - **`04-Matching-and-Class-Management.md`**: Vòng đời khóa học, điểm danh Online/Offline và lộ trình tính năng Video Call.