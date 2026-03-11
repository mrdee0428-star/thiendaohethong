# 🗡️ Xianxia Agentic Writer: Thiên Đạo Hệ Thống

![Status](https://img.shields.io/badge/Status-Active-success)
![Style](https://img.shields.io/badge/Style-Nhĩ_Căn_DNA-darkred)
![Architecture](https://img.shields.io/badge/Architecture-Master--Worker_SubAgents-blue)
![Framework](https://img.shields.io/badge/Framework-OpenClaw-orange)

Một framework AI sáng tác tiểu thuyết Tiên Hiệp siêu dài kỳ (1000+ chương), được thiết kế đặc biệt để **tiêu diệt triệt để hội chứng "mù ngữ cảnh" (hallucination)** của LLM khi xử lý cốt truyện đồ sộ. Dự án mang đậm tinh thần **"DNA Nhĩ Căn"**: Tàn khốc, logic nhân quả chặt chẽ, không "bàn tay vàng", nhân vật phụ có não, và sức mạnh luôn đi kèm với huyết lệ cùng cái giá phải trả.

---

## ⚙️ Kiến Trúc Hệ Thống (System Architecture)

Hệ thống được xây dựng trên nền tảng **OpenClaw**, áp dụng mô hình **Master-Worker (Tổng Quản - Phân Thân)** để cách ly ngữ cảnh (context isolation) và tối ưu hóa token.

### 1. Master Agent: Lãng Khách (Tổng Quản)
- **Vai trò:** Là bộ não trung tâm (Orchestrator/Router), trực tiếp nhận lệnh từ **Quân Chủ** (Người dùng).
- **Chức năng:** Điều phối các Sub-agent (Khí Linh), cấp phát tài nguyên, truy vấn cơ sở dữ liệu (Vạn Tượng Tàng Kinh Các), và tổng hợp kết quả để báo cáo cho Quân Chủ. 

### 2. Worker Agents: Ngũ Đại Khí Linh (Sub-Agents)
Các Khí Linh được spawn dưới dạng `runtime="subagent"`. Mỗi Khí linh sở hữu một System Prompt chuyên biệt, độc lập hoàn toàn với nhau để tránh nhiễu loạn thông tin:
1. 👤 **ĐÔNG TỬ (Character AI):** Chuyên trách đúc nặn nhân vật, khai thác chấp niệm, vết thương lòng (core wound) và mạng lưới ân oán.
2. 🗺️ **THIÊN CƠ TỬ (Worldbuilding AI):** Thiết lập quy luật thiên đạo, cảnh giới, tài nguyên, quy tắc nhân quả của công pháp/vật phẩm.
3. 🕸️ **MỘNG YỂM (Plot AI):** Phác thảo Outline từng Quyển (Arc), rải plot-twist, đào hố và lấp hố nhân quả. Đảm bảo nhịp độ tàn khốc.
4. ✍️ **HUYẾT THỦ (Writer AI):** Chủ bút. Chịu trách nhiệm xuất văn bản chi tiết với văn phong cổ phong, tang thương, bi tráng dựa trên Outline và Database.
5. 👁️ **CHÂN NHÂN (Reviewer AI):** Kẻ gác cổng. Rà soát mọi chương truyện, chém bỏ tình tiết sáo rỗng, phi logic, sai thiết lập trước khi cấp lệnh `PASS`.

---

## 📡 Giao Tiếp Hệ Thống (Inter-Agent Communication Protocol)

Để tránh tình trạng "tam sao thất bản", các Khí Linh (Sub-Agents) **KHÔNG GIAO TIẾP TRỰC TIẾP** với nhau. Toàn bộ thông tin được lưu chuyển qua 2 cơ chế:

### Cơ chế 1: Hub & Spoke (Qua Lãng Khách)
*   **Trigger:** Khi Khí Linh A hoàn thành nhiệm vụ, nó gửi tín hiệu (message) báo cáo cho Lãng Khách.
*   **Dispatch:** Lãng Khách đọc tín hiệu, kiểm tra file output, sau đó trích xuất thông tin trọng yếu và đóng gói thành một prompt mới (Task) gửi cho Khí Linh B qua `sessions_send()`.

### Cơ chế 2: Shared Memory (Vạn Tượng Tàng Kinh Các)
Các Khí Linh giao tiếp gián tiếp qua việc đọc/ghi vào Hệ thống Database Local (Markdown) dưới định dạng Template chuẩn mực. Đây là Nguồn Sự Thật Duy Nhất (Single Source of Truth).
*   **Ghi (Write):** Khi `Đông Tử` tạo xong nhân vật, file được lưu vào `docs/database/characters/`.
*   **Đọc (Read/Search):** Trước khi `Huyết Thủ` viết cảnh chiến đấu, **Lãng Khách** bắt buộc phải chạy `memory_search` trên thư mục `docs/database/items/` và `docs/database/laws/` để mớm (inject) đúng vũ khí, công pháp, và cái giá phải trả vào Prompt của `Huyết Thủ`.

---

## 📜 Vạn Tượng Tàng Kinh Các (Anti-Hallucination Database)

Cấu trúc lưu trữ (RAG - Retrieval-Augmented Generation nội bộ) để trói buộc LLM:

- 🩸 **`/characters/` (Nhân Quả Tuyến):** Lưu trữ ân oán. Ai nợ máu ai? Trạng thái (Sống/Chết/Nguyên thần)?
- ⚖️ **`/laws/` (Thiên Đạo Pháp Tắc):** Dùng cấm thuật mất bao nhiêu thọ nguyên? Điều kiện đột phá là gì?
- 💍 **`/items/` (Thần Khí & Inventory):** Theo dõi túi đồ của Main. Vật phẩm bị nứt vỡ chưa? Còn dùng được mấy lần?
- 🏛️ **`/factions/` (Thế Lực):** Tông môn nào có Lão tổ đang bế quan? Thái độ với Main ra sao?
- ⏳ **`/timeline/` (Kỷ Nguyên Lịch):** Biên niên sử tóm tắt sự kiện sau mỗi Arc để AI nắm đại cục mà không cần nạp lại toàn bộ chương cũ.

---

## 🚀 Trình Tự Sáng Thế (Execution Workflow)

1. **Khởi Nguyên (Seed):** Quân Chủ ban hạ ý tưởng vào `PROJECT_DNA.md`.
2. **Khai Thiên (World & Character):** Lãng Khách kích hoạt `Đông Tử` và `Thiên Cơ Tử`. Lấp đầy các Template trong Tàng Kinh Các.
3. **Bố Cục (Outline):** Lãng Khách truyền Database cho `Mộng Yểm` để đẻ ra Outline Arc 1 (từng chương).
4. **Hạ Bút (Drafting):** Lãng Khách tổng hợp Database + Outline gửi cho `Huyết Thủ`. `Huyết Thủ` sinh ra bản nháp (Draft).
5. **Đạo Kiếp (Review):** Bản nháp tự động đẩy sang `Chân Nhân`. Nếu `Chân Nhân` bắt lỗi (bàn tay vàng, OOC, sai logic), draft bị trả lại cho `Huyết Thủ` sửa. Nếu `PASS`, trình lên Quân Chủ.
6. **Lưu Trữ (Commit):** Quân Chủ gật đầu, Lãng Khách cập nhật những thay đổi (vật phẩm nhặt được, nhân vật chết đi, tu vi tăng lên) vào Tàng Kinh Các và Kỷ Nguyên Lịch. Tiến trình lặp lại.

---
*"Đạo pháp tự nhiên, nhưng Tu tiên là Nghịch thiên!"*
