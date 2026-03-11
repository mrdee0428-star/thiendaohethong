# 📜 Khế Ước Khí Linh (API.md & Agent Contracts)

Để tránh tình trạng "Tam Sao Thất Bản" và lỗi Parse (mù ngữ cảnh cấu trúc), toàn bộ Khí Linh giao tiếp qua chuẩn JSON Schema khắt khe (Pydantic models).

## 1. Đông Tử ➔ Lãng Khách (Character Schema)
Mỗi khi Đông Tử nặn xong 1 nhân vật, bắt buộc phải trả về cục JSON sau:
```json
{
  "name": "Thanh Dạ",
  "status": "Alive",
  "cultivation_level": "Ngưng Niệm Tầng 1",
  "core_wound": "Bị thế giới lãng quên, chạm vào là gây giảm thọ",
  "obsession": "Được công nhận sự tồn tại",
  "inventory": [],
  "karma_links": [
    {
      "target": "Lão Mù",
      "relation": "Ân nhân",
      "status": "Chưa trả nợ"
    }
  ],
  "trump_cards": [
    {
      "name": "Thuật Rứt Hồn",
      "cost": "10 năm thọ nguyên"
    }
  ]
}
```

## 2. Thiên Cơ Tử ➔ Lãng Khách (Law/Faction Schema)
```json
{
  "entity_name": "Thuật Rứt Hồn",
  "category": "Cấm Thuật",
  "mechanism": "Rút linh hồn kẻ địch thành chất dinh dưỡng",
  "cost_and_backlash": "Mất 10 năm thọ nguyên, chịu đau đớn như ngàn vạn kiến cắn",
  "weakness": "Không có tác dụng với kẻ có linh hồn cường đại hơn 1 đại cảnh giới"
}
```

## 3. Mộng Yểm ➔ Lãng Khách (Plot Outline Schema)
```json
{
  "arc_name": "Đám Tang Cô Châu",
  "chapter_number": 3,
  "summary": "Thanh Dạ quan sát đám tang, gặp thiếu nữ giống hệt giấc mơ",
  "required_context_queries": ["Thanh Dạ có năng lực gì?", "Lão Mù là ai?"],
  "plot_twists": "Thiếu nữ đó không thể nhìn thấy Thanh Dạ, nhưng lại rơi nước mắt",
  "karma_changes": {
    "new_encounters": ["Thiếu nữ Tống gia"],
    "items_gained": []
  }
}
```

## 4. Chân Nhân ➔ Lãng Khách (Review Result Schema)
Điểm số đánh giá Đạo Tâm. Nếu `is_passed = false`, Huyết Thủ phải nhận lấy feedback và viết lại.
```json
{
  "chapter_number": 3,
  "logic_score": 85,
  "writing_score": 90,
  "is_passed": true,
  "feedback_for_writer": "Đã tả tốt sự lạnh lẽo. Điểm trừ nhỏ: Thiếu miêu tả kỹ hơn về bóng tối xung quanh.",
  "violations_found": []
}
```