# 🗡️ Xianxia Agentic Writer: Thiên Đạo Hệ Thống (V2: Hóa Thần Cảnh)

![Status](https://img.shields.io/badge/Status-Active-success)
![Style](https://img.shields.io/badge/Style-Nhĩ_Căn_DNA-darkred)
![Architecture](https://img.shields.io/badge/Architecture-Master--Worker_SubAgents-blue)
![Framework](https://img.shields.io/badge/Framework-OpenClaw_V2-orange)

Một framework AI sáng tác tiểu thuyết Tiên Hiệp siêu dài kỳ (1000+ chương), được thiết kế đặc biệt để **tiêu diệt triệt để hội chứng "mù ngữ cảnh" (hallucination)** của LLM khi xử lý cốt truyện đồ sộ. Dự án mang đậm tinh thần **"DNA Nhĩ Căn"**: Tàn khốc, logic nhân quả chặt chẽ, không "bàn tay vàng", nhân vật phụ có não, và sức mạnh luôn đi kèm với huyết lệ cùng cái giá phải trả.

---

## ⚙️ Kiến Trúc Hệ Thống (System Architecture)

Hệ thống được xây dựng trên nền tảng **OpenClaw**, áp dụng mô hình **Master-Worker (Tổng Quản - Phân Thân)** để cách ly ngữ cảnh (context isolation) và tối ưu hóa token.

### 1. Master Agent: Lãng Khách (Tổng Quản)
- **Vai trò:** Là bộ não trung tâm (Orchestrator/Router), trực tiếp nhận lệnh từ **Quân Chủ** (Người dùng).
- **Chức năng:** Điều phối các Sub-agent (Khí Linh), cấp phát tài nguyên, truy vấn cơ sở dữ liệu, và tổng hợp kết quả để báo cáo cho Quân Chủ. Tích hợp **Luân Hồi Điện (Task Queue)** để xử lý bất đồng bộ (Async).

### 2. Worker Agents: Ngũ Đại Khí Linh (Sub-Agents)
Các Khí Linh được cấu trúc với **Khế Ước Ràng Buộc (Agent Contracts)** - mọi Input/Output đều được chuẩn hóa bằng JSON Schema/YAML để tránh đứt gãy dây chuyền (Chain Reaction).
1. 👤 **ĐÔNG TỬ (Character AI):** Chuyên trách đúc nặn nhân vật, khai thác chấp niệm.
2. 🗺️ **THIÊN CƠ TỬ (Worldbuilding AI):** Thiết lập quy luật thiên đạo, cảnh giới, cái giá phải trả.
3. 🕸️ **MỘNG YỂM (Plot AI):** Phác thảo Outline từng Quyển (Arc), rải plot-twist.
4. ✍️ **HUYẾT THỦ (Writer AI):** Chủ bút. Chịu trách nhiệm xuất văn bản với văn phong tang thương.
5. 👁️ **CHÂN NHÂN (Reviewer AI):** Kẻ gác cổng tàn khốc. Rà soát logic và thiết lập.

---

## 📡 Giao Tiếp & Giải Quyết Xung Đột (Inter-Agent Protocol)

Khắc phục tình trạng thắt cổ chai (Bottleneck) và mâu thuẫn logic của kỷ nguyên trước:

### 1. Luân Hồi Điện (Async Task Queue)
Lãng Khách không còn là điểm nghẽn cổ chai (Single Point of Failure). Các tác vụ không phụ thuộc nhau (như tạo Worldbuilding và tạo Nhân vật phụ) sẽ được đẩy vào Luân Hồi Điện để **chạy song song (Parallel Execution)**.

### 2. Trọng Tài Chi Thuật (Arbitration & Consensus)
Nếu Mộng Yểm (Plot) phác thảo một tình tiết mâu thuẫn với Thiên Cơ Tử (Worldbuilding), hệ thống sẽ không lặp vô hạn. Dữ liệu trong Tàng Kinh Các (Config Vault) được coi là **Canonical Source of Truth**. Lãng Khách sẽ làm Trọng Tài: Ép Plot phải uốn theo Worldbuilding, không có ngoại lệ.

### 3. Cửu Trọng Thiên Kiếp (Retry Limits)
Để tránh "Review Loop vô hạn" giữa Huyết Thủ (Viết) và Chân Nhân (Duyệt), hệ thống thiết lập **Max Retry = 3**. Nếu qua 3 lần sửa mà vẫn không đạt Đạo Tâm, tiến trình sẽ tạm ngưng và réo gọi **Quân Chủ (Manual Override)** định đoạt sinh tử của chương truyện đó.

---

## 📜 Vạn Tượng Tàng Kinh Các (Vectorized Database)

Bản nâng cấp tối thượng để đáp ứng quy mô 1000+ chương. Thư mục Markdown giờ đây chỉ là bề nổi (Frontend) cho con người đọc. Bên dưới, hệ thống được cường hóa bằng **Tinh Thần Hải (Vector DB / Embeddings)**.

*   **Semantic Search thay vì Keyword Search:** Khi truy vấn "kẻ thù hệ hỏa của main", hệ thống sẽ dùng Vector Search để lôi ra toàn bộ nhân quả, vũ khí, và pháp tắc liên quan cực kỳ nhanh chóng và chính xác, không sợ phình to dữ liệu.

- 🩸 **`/characters/` (Nhân Quả Tuyến)**
- ⚖️ **`/laws/` (Thiên Đạo Pháp Tắc)**
- 💍 **`/items/` (Thần Khí & Inventory)**
- 🏛️ **`/factions/` (Thế Lực)**
- ⏳ **`/timeline/` (Kỷ Nguyên Lịch)**

---

## 🚀 Trình Tự Sáng Thế (Execution Workflow)

1. **Khởi Nguyên:** Quân Chủ ban hạ ý tưởng vào `PROJECT_DNA.md`.
2. **Khai Thiên (Parallel):** Lãng Khách xuất lệnh đồng thời cho `Đông Tử` và `Thiên Cơ Tử`. Lấp đầy Tàng Kinh Các. Cấu trúc hóa thành Vector Embeddings.
3. **Bố Cục:** `Mộng Yểm` tải Embeddings để đẻ ra Outline Arc 1 (từng chương).
4. **Hạ Bút:** Lãng Khách mớm (inject) context từ Vector DB cho `Huyết Thủ`. `Huyết Thủ` sinh bản nháp.
5. **Đạo Kiếp:** Draft đẩy sang `Chân Nhân`. Nếu tẩu hỏa nhập ma, phạt sửa (Max 3 lần). Nếu thất bại, gọi Quân Chủ. Nếu PASS, lưu vào Kỷ Nguyên Lịch.
6. **Mệnh Bàn (Logging):** Toàn bộ trạng thái sống/chết, tiến độ của các Khí Linh được ghi log realtime để Quân Chủ theo dõi.

---
*"Đạo pháp tự nhiên, nhưng Tu tiên là Nghịch thiên! Chỉ có quy luật sắt đá mới chống lại được sự hỗn mang của Ký Ức!"*
