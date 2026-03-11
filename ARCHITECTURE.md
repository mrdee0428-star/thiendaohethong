# 🏗️ Kiến Trúc Hệ Thống (ARCHITECTURE.md)

Hệ thống Sáng Thế của chúng ta được chia làm 3 Tầng Giới (Layers): **Tầng Chỉ Huy (Master Layer)**, **Tầng Chấp Hành (Worker Layer)**, và **Tầng Nền Tảng (Data Layer)**.

## 1. Sơ Đồ Tổng Quan (Data Flow)

```mermaid
graph TD
    QC([Quân Chủ / Người Dùng]) -->|Ban Hạt Giống| LK(Lãng Khách - Master Agent)
    LK -->|Giao Task| LHD((Luân Hồi Điện - Async Task Queue))
    
    subgraph Worker Layer (Ngũ Đại Khí Linh)
        LHD -->|Spawn| DT(Đông Tử - Character)
        LHD -->|Spawn| TCT(Thiên Cơ Tử - Worldbuilding)
        LHD -->|Spawn| MY(Mộng Yểm - Plot)
        LHD -->|Spawn| HT(Huyết Thủ - Writer)
        LHD -->|Spawn| CN(Chân Nhân - Reviewer)
    end
    
    subgraph Data Layer (Vạn Tượng Tàng Kinh Các)
        LK <-->|Đọc/Ghi qua Mutex Lock| Markdown[Thư Mục Local Markdown]
        LK <-->|Top-K Search| VectorDB[(ChromaDB - Local Vector Store)]
        Ollama[Ollama: nomic-embed-text] -.->|Tạo Embeddings| VectorDB
    end

    DT -.->|Trả JSON kết quả| LK
    TCT -.->|Trả JSON kết quả| LK
    MY -.->|Trả JSON kết quả| LK
    HT -.->|Trả Bản Nháp| CN
    
    CN -->|Đạt 80+ Điểm| LK
    CN -->|Dưới 80 Điểm (Max 3 lần)| HT
    CN -->|Trượt 3 lần| Manual[PENDING_APPROVAL.md chờ Quân Chủ]
    Manual -.->|Force Pass/Rewrite| LK
```

## 2. Giải Thích Các Trận Pháp Lõi

### A. Luân Hồi Điện (Task Queue & Concurrency)
- Hệ thống không bắt Đông Tử chờ Thiên Cơ Tử làm xong mới được nặn nhân vật. 
- Lãng Khách đẩy task vào Queue. Nếu Task không có Dependencies (Ràng buộc trước sau), chúng sẽ được kích hoạt song song (`async.gather`).
- Output của Khí Linh trả về Lãng Khách để thực hiện **Sequential Merge** (Hợp nhất tuần tự) nhằm tránh Conflict.

### B. Thần Thức Tỏa (Mutex Lock)
- Khí Linh không bao giờ được phép trực tiếp sửa file Markdown.
- Mọi thao tác `Write` phải nạp qua Lãng Khách. Lãng Khách áp dụng khóa `Lock()` trên file `characters/nhan_vat_A.md` để đảm bảo không bị ghi đè dữ liệu.

### C. Tinh Thần Hải (ChromaDB + Ollama)
- Mọi file Markdown khi cập nhật sẽ kích hoạt event tạo Embedding bằng model `nomic-embed-text` (chạy qua Ollama localhost).
- Lưu trữ vào ChromaDB. Khi Huyết Thủ cần viết, Lãng Khách gửi Query: *"Main dùng vũ khí gì để đánh kẻ thù hệ Thủy?"* ➔ ChromaDB trả về 3 Chunk liên quan nhất để nạp vào Prompt của Huyết Thủ.