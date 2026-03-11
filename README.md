# 🗡️ Xianxia Agentic Writer: Thiên Đạo Hệ Thống

![Status](https://img.shields.io/badge/Status-Active-success)
![Style](https://img.shields.io/badge/Style-Nhĩ_Căn_DNA-darkred)
![Architecture](https://img.shields.io/badge/Architecture-Multi--Agent-blue)

Một framework AI sáng tác tiểu thuyết Tiên Hiệp siêu dài kỳ (1000+ chương), được thiết kế đặc biệt để **tiêu diệt triệt để hội chứng "mù ngữ cảnh" (hallucination)** của các mô hình LLM khi xử lý cốt truyện đồ sộ. 

Dự án được thai nghén với tinh thần **"DNA Nhĩ Căn"**: Tàn khốc, logic nhân quả chặt chẽ, không "bàn tay vàng" (buff bẩn) vô lý, nhân vật phụ có não, và sức mạnh luôn đi kèm với huyết lệ cùng cái giá phải trả.

---

## ⚙️ Kiến Trúc Hệ Thống (Đại Đạo Quy Tắc)

Hệ thống không dùng một Prompt duy nhất để viết truyện, mà chia nhỏ thành một **Mô hình Phân quyền (Multi-Agent)** được điều phối bởi AI Tổng quản (Lãng Khách) và giám sát tối cao bởi **Quân Chủ** (Tác giả/Human).

### 🎭 Ngũ Đại Khí Linh (Sub-Agents)
Mỗi Khí linh chỉ đảm nhận một nhiệm vụ duy nhất để tối ưu hóa context:
1. 👤 **ĐÔNG TỬ (Character AI):** Chuyên trách đúc nặn nhân vật, khai thác chấp niệm, core wound (vết thương lòng) và mạng lưới ân oán.
2. 🗺️ **THIÊN CƠ TỬ (Worldbuilding AI):** Thiết lập quy luật thiên đạo, cảnh giới, tài nguyên, và đặc biệt là "cái giá phải trả" của từng loại công pháp.
3. 🕸️ **MỘNG YỂM (Plot AI):** Phác thảo Outline từng Quyển (Arc), rải plot-twist, đào hố và lấp hố nhân quả.
4. ✍️ **HUYẾT THỦ (Writer AI):** Chủ bút. Chịu trách nhiệm xuất văn bản chi tiết với văn phong cổ phong, tang thương, bi tráng.
5. 👁️ **CHÂN NHÂN (Reviewer AI):** Kẻ gác cổng tàn khốc. Rà soát mọi chương truyện, chém bỏ tình tiết sáo rỗng, phi logic, sai thiết lập trước khi trình lên Quân Chủ.

---

## 📜 Vạn Tượng Tàng Kinh Các (Anti-Hallucination Database)

Điểm yếu chí mạng của AI viết truyện là "quên" (quên vật phẩm đã dùng, quên nhân vật phụ, mâu thuẫn sức mạnh). Framework này giải quyết bằng hệ thống Database Local (Markdown) bắt buộc truy vấn trước khi viết:

- 🩸 **`/characters/` (Nhân Quả Tuyến):** Lưu trữ ân oán. Ai nợ máu ai? Ai còn sống/chết/chỉ còn nguyên thần?
- ⚖️ **`/laws/` (Thiên Đạo Pháp Tắc):** Luật lệ tu luyện. Dùng cấm thuật mất bao nhiêu thọ nguyên? Điều kiện đột phá là gì?
- 💍 **`/items/` (Thần Khí & Inventory):** Theo dõi túi đồ của Main. Vật phẩm bị nứt vỡ chưa? Còn dùng được mấy lần?
- 🏛️ **`/factions/` (Thế Lực):** Tông môn nào có Lão tổ đang bế quan? Thái độ với Main ra sao?
- ⏳ **`/timeline/` (Kỷ Nguyên Lịch):** Biên niên sử tóm tắt sự kiện sau mỗi Arc để AI nắm đại cục mà không cần nạp lại 500 chương cũ.

---

## 🚀 Quy Trình Vận Hành (Workflow)

1. **Khởi nguyên:** Quân Chủ cung cấp ý tưởng cốt lõi (Hạt giống) vào `PROJECT_DNA.md`.
2. **Thiết lập:** Tổng quản Lãng Khách gọi `Đông Tử` và `Thiên Cơ Tử` lấp đầy Database.
3. **Bố cục:** `Mộng Yểm` lên Outline Arc 1.
4. **Hạ bút & Đạo kiếp:** `Huyết Thủ` viết Chương ➔ `Chân Nhân` rà soát ➔ Quân Chủ phê duyệt (Pass).
5. **Cập nhật:** Lưu biến động vào Tàng Kinh Các sau mỗi chương/Arc.

---
*"Thiên địa bất nhân, dĩ vạn vật vi sô cẩu. Đạo pháp tự nhiên, nhưng Tu tiên là Nghịch thiên!"*
