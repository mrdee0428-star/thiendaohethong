# 🗡️ Xianxia Agentic Writer: Thiên Đạo Hệ Thống (V4: Độ Kiếp Cảnh)

![Status](https://img.shields.io/badge/Status-Active-success)
![Style](https://img.shields.io/badge/Style-Nhĩ_Căn_DNA-darkred)
![Architecture](https://img.shields.io/badge/Architecture-Master--Worker_SubAgents-blue)

Bản V4 (Độ Kiếp Cảnh) đã khắc phục 3 Tâm Ma chí mạng: **Đứt Gãy Tương Lai (Foresight Decay)**, **Nhiễu Loạn Duyệt Bài (Review Loop Fatigue)**, và **Suy Thoái Văn Phong (Stylistic Collapse)**.

---

## 📜 1. Tinh Thần Hải Cường Hóa (Vector DB + Mưu Kế & Văn Phong)

Ngoài các database cơ bản, Tàng Kinh Các nay có thêm 2 Tầng Ngọc Giản:
- ♟️ **`/plot_threads/` (Thiên Đạo Kỳ Bàn):** Hệ thống theo dõi mục tiêu dài hạn (Long-term Goal Tracker). Lưu trữ các "hố" (plot twists), âm mưu nhiều lớp. Mộng Yểm bắt buộc phải kiểm tra Kỳ Bàn để "lấp hố" đúng thời điểm, chấm dứt tình trạng quên mạch truyện ngầm.
- 🖋️ **`/style_vault/` (Linh Cảm Khố):** Thư viện "Few-shot Example". Chân Nhân sẽ trích xuất những đoạn văn xuất sắc nhất (đậm chất Nhĩ Căn) lưu vào đây. Trước khi viết, Huyết Thủ sẽ bốc ngẫu nhiên 2 đoạn mẫu trong Khố để tự "căn chỉnh Đạo Tâm", duy trì văn phong tang thương đến tận chương 1000.

---

## ⚖️ 2. Trảm Đứt Vòng Lặp Bất Tận (Soft-Fail & Graceful Degradation)

Quân Chủ tạo ra AI để làm Sáng Thế Thần, không phải làm bảo mẫu. 
- Cơ chế **Đạo Kiếp (Max Retries = 3)** được nâng cấp thành **Đạo Kiếp Khoan Hồng (Soft-Fail)**.
- Nếu sau 3 lần sửa mà vẫn kẹt ở lỗi nhỏ (VD: điểm logic = 75/100), Chân Nhân sẽ **KHÔNG TẠM DỪNG** hệ thống. Nó sẽ tự động `Force-Pass` (Cưỡng ép thông qua), gắn cờ `Tâm Ma Ẩn Tàng (Warning Flag)` và ghi vào Log. Hệ thống vẫn chạy tiếp để đảm bảo tiến độ. Quân Chủ chỉ cần đọc Log lúc rảnh rỗi để soát lại.
- Trừ khi lỗi quá nặng (Main đột nhiên gọi ra súng máy, logic = 0), tiến trình mới bị đóng băng.

---
*Xem chi tiết API mới tại `API.md` và Cấu trúc Database tại thư mục `docs/database/`.*