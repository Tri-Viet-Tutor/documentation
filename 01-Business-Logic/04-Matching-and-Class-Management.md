# Business Rule 04: Class Management & Video Call Roadmap

## 1. Vòng Đời Lớp Học & Khóa Học (Course & Class Lifecycle)

```mermaid
stateDiagram-v2
    [*] --> DRAFT: Admin tạo Khóa học & Thiết lập giá/ca học
    DRAFT --> PUBLISHED: Mở đăng ký cho Học viên
    PUBLISHED --> ENROLLING: Học viên đăng ký & Thanh toán tiền Khóa học
    ENROLLING --> ASSIGNED: Admin xếp Gia sư Trung tâm vào Ca học (Bắt Trùng Lịch)
    ASSIGNED --> IN_PROGRESS: Khai giảng lớp học (Đủ điều kiện sĩ số 2-8 HV)
    IN_PROGRESS --> COMPLETED: Hoàn thành toàn bộ các buổi học trong khóa
```

---

## 2. Quy tắc Lớp Học Online vs Offline (Online & Offline Attendance)

- **Lớp Offline (Tại Trung tâm / Tại nhà)**: Điểm danh qua mã QR hoặc Gia sư xác nhận Check-in trên ứng dụng.
- **Lớp Online**: Học viên và Gia sư tham gia phòng Video Call được tích hợp sẵn trong ứng dụng VietTriTutor. Hệ thống tự động điểm danh khi thời gian tham gia phòng $\ge 70\%$ thời lượng ca học.

---

## 3. Lộ Trình Kỹ Thuật Video Call (Video Call Roadmap)

- **Giai đoạn 1 (MVP)**: Sử dụng SDK bên thứ 3 (Agora.io, Jitsi Meet API, Zoom SDK, Daily.co) để tích hợp nhanh tính năng phòng học ảo (Video/Audio, Screen Share, Chat).
- **Giai đoạn 2 (Nâng cao)**: Tự phát triển Media Server riêng (sử dụng Mediasoup SFU WebRTC) kết hợp Bảng trắng tương tác (Interactive Whiteboard) và Cloud Recording để lưu bài giảng cho học viên xem lại.
