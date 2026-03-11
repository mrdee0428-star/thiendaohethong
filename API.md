# 📜 Khế Ước Khí Linh (API.md & Agent Contracts) - Bản Độ Kiếp V4

## 1. Chân Nhân ➔ Lãng Khách (Soft-Fail Review Schema)
Giải quyết tình trạng "Review Loop" mệt mỏi. Thay vì bắt Quân Chủ sửa tay, Chân Nhân có quyền gắn mác `warning_flag` để cho qua, nhưng ghi chú lại lỗi nhỏ.

```json
{
  "chapter_number": 3,
  "logic_score": 75,
  "writing_score": 85,
  "is_passed": true, 
  "soft_fail_reason": "Có chút OOC nhẹ ở đoạn Thanh Dạ nói chuyện. Lẽ ra nên im lặng hơn.",
  "action_taken": "Force-Pass with Warning (Đã sửa lại một vài câu trong bản Final).",
  "style_vault_candidates": [
    {
      "text": "Trích đoạn văn hay để ném vào Linh Cảm Khố",
      "tag": "Cô độc"
    }
  ]
}
```

## 2. Mộng Yểm ➔ Lãng Khách (Plot Outline Schema với Plot Threads)
Mộng Yểm phải kiểm tra các Hố (Threads) đang mở.
```json
{
  "arc_name": "Đám Tang Cô Châu",
  "chapter_number": 4,
  "summary": "...",
  "active_plot_threads_updated": [
    {
      "thread_name": "Bí mật Tống gia",
      "action": "Rải manh mối số 1 (Breadcrumb)"
    }
  ]
}
```