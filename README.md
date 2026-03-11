# 🗡️ Xianxia Agentic Writer: Thiên Đạo Hệ Thống (V3: Đại Thừa Cảnh)

![Status](https://img.shields.io/badge/Status-Active-success)
![Style](https://img.shields.io/badge/Style-Nhĩ_Căn_DNA-darkred)
![Architecture](https://img.shields.io/badge/Architecture-Master--Worker_SubAgents-blue)
![Database](https://img.shields.io/badge/VectorDB-Chroma%20%2B%20Ollama%20(Local)-brightgreen)
![Framework](https://img.shields.io/badge/Framework-OpenClaw_V3-orange)

Một framework AI sáng tác tiểu thuyết Tiên Hiệp siêu dài kỳ (1000+ chương), được thiết kế đặc biệt để **tiêu diệt triệt để hội chứng "mù ngữ cảnh" (hallucination)** của LLM khi xử lý cốt truyện đồ sộ. Dự án mang đậm tinh thần **"DNA Nhĩ Căn"**: Tàn khốc, logic nhân quả chặt chẽ, không "bàn tay vàng", và sức mạnh luôn đi kèm với huyết lệ.

Bản V3 (Đại Thừa Cảnh) được nâng cấp toàn diện dựa trên chỉ dụ của **Quân Chủ (Dũng Meow)**, tập trung vào **Local Vector Search**, **Xử lý xung đột đồng thời (Concurrency Control)** và **Đo lường Đạo Tâm (Metrics)**.

---

## ⚙️ Kiến Trúc Hệ Thống (System Architecture)

> Xem chi tiết sơ đồ tại: [ARCHITECTURE.md](ARCHITECTURE.md)

Hệ thống hoạt động theo mô hình **Master-Worker (Tổng Quản - Phân Thân)**, kết hợp **Async Task Queue (Luân Hồi Điện)**.

1. **Master Agent (Lãng Khách):** Trọng tài tối cao, bộ định tuyến (Router), và người giữ chìa khóa khóa (Mutex Lock) vào cơ sở dữ liệu.
2. **Worker Agents (Ngũ Đại Khí Linh):** `Đông Tử` (Character), `Thiên Cơ Tử` (Worldbuilding), `Mộng Yểm` (Plot), `Huyết Thủ` (Writer), `Chân Nhân` (Reviewer). Các Khí Linh chạy song song, giao tiếp qua JSON Schema khép kín (xem [API.md](API.md)).

---

## 📜 Tinh Thần Hải (Vectorized Database & Semantic Search)

Markdown file chỉ là giao diện hiển thị. Cốt lõi của Tàng Kinh Các đã được nâng cấp thành **Tinh Thần Hải** để chống "Mù Ngữ Cảnh" với chi phí = 0:

- **Vector Database:** `ChromaDB` (Chạy local, không lưu trữ đám mây, bảo mật tuyệt đối).
- **Embedding Model:** `nomic-embed-text` thông qua `Ollama` (Local 100%, tốn 0 đồng, tốc độ cực cao).
- **Cơ chế Truy Vấn (Top-K Retrieval):** Khi Huyết Thủ cần viết cảnh giao tranh, Lãng Khách chỉ quét Vector DB và lấy ra 3-5 mẩu thông tin (chunks) liên quan nhất (ví dụ: vũ khí, kẻ thù hiện tại), giúp giảm tải Context Window xuống dưới 1000 tokens/lần gọi.
- **Thần Thức Tỏa (Mutex Lock):** Chống Race Condition. Khi Đông Tử đang ghi dữ liệu vào 1 file, các Khí Linh khác phải vào hàng chờ (Queue), Lãng Khách sẽ hợp nhất (Merge) tuần tự.

---

## ⚖️ Luật Đạo Tranh & Trảm Đứt Vòng Lặp (Conflict Resolution)

- **Trọng Tài Mâu Thuẫn:** Dữ liệu trong `docs/database/` (Vector DB) là **Canonical Source of Truth**. Nếu Plot (Mộng Yểm) mâu thuẫn với Worldbuilding (Thiên Cơ Tử), Lãng Khách sẽ vả mặt Mộng Yểm, ép Plot phải tuân theo thiết lập thế giới.
- **Đạo Kiếp Giới Hạn (Max Retries = 3):** Chân Nhân (Reviewer) chỉ được quyền bắt Huyết Thủ (Writer) sửa tối đa 3 lần. Nếu lần 4 vẫn trượt bài test logic, tiến trình sinh chương bị đóng băng ➔ Chuyển sang file `PENDING_APPROVAL.md` chờ Quân Chủ định đoạt sinh tử.

---

## 📊 Mệnh Bàn & Đạo Tâm Đo Lường (Logging & Metrics)

- **Mệnh Bàn (Streamlit Dashboard):** Giao diện UI local đọc từ `logs/system_state.jsonl`. Quân Chủ có thể theo dõi realtime Khí Linh nào đang chạy, tốn bao nhiêu token, và trạng thái chương đang viết.
- **Thước Đo Đạo Tâm (Metrics):**
  - *Logic Consistency Score (0-100):* LLM-as-a-judge (Chân Nhân) chấm điểm dựa trên Vector DB. Dưới 80 điểm (sai tên, lôi đồ không có trong inventory ra xài) ➔ Bắt viết lại.
  - *Writing Quality Score (0-100):* Đếm mật độ từ vựng cổ phong, phạt điểm nếu lặp lại các câu sáo rỗng ("hít một ngụm khí lạnh").

---

## 🛠️ Khởi Động Kỷ Nguyên Mới (Quick Start)

1. Cài đặt Python dependencies: `pip install -r requirements.txt`
2. Cài đặt và bật [Ollama](https://ollama.ai/), pull model: `ollama pull nomic-embed-text`
3. Xem mẫu Hạt Giống Sáng Thế tại: `examples/PROJECT_DNA_sample.md`
4. Khởi chạy Mệnh Bàn: `streamlit run dashboard.py` (Script đang được kiến tạo)

*"Đạo pháp tự nhiên, nhưng Tu tiên là Nghịch thiên!"*