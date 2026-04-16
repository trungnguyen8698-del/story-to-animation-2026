---
name: 02-extracting-scenes-and-visuals
description: Bước 2 — Đọc script.md và trích xuất danh sách cảnh (scenes) cùng visual concept cho từng cảnh. Output là scenes.json và visuals.json để dùng ở Bước 3.
---

# Bước 2 — Trích Xuất Cảnh và Visual Concept (EnigmaMind)

## Đầu vào
File `script.md` từ Bước 1.

## Nhiệm vụ

### A. Phân tích script thành các cảnh (scenes)
Mỗi cảnh = một đơn vị visual, thường tương ứng với 1–3 câu trong script hoặc một ý tưởng hoàn chỉnh.

Trung bình một video 7–8 phút cần **25–40 cảnh**.

### B. Xác định visual concept cho từng cảnh

Với mỗi cảnh, xác định:
- **Cảm xúc cốt lõi** (emotion): cô đơn / mâu thuẫn / khai ngộ / bình thản / v.v.
- **Loại tượng** (statue_type):
  - `bust` — tượng bán thân, tập trung vào khuôn mặt
  - `full_figure` — toàn thân
  - `hands` — chỉ bàn tay
  - `abstract_fragment` — mảnh vỡ, chi tiết trừu tượng
  - `two_figures` — hai tượng tương tác
- **Tư thế / trạng thái** (pose): mô tả ngắn gọn bằng tiếng Anh
- **Ánh sáng** (lighting):
  - `enlightenment` — ánh sáng từ trên xuống (khai ngộ)
  - `conflict` — ánh sáng từ bên hông (mâu thuẫn)
  - `darkness` — ánh sáng từ dưới hoặc rất yếu (tối tăm)
  - `dawn` — ánh sáng lan dần từ một phía (bình minh nhận thức)

## Output Format

### scenes.json
```json
[
  {
    "scene_id": "scene_001",
    "script_section": "HOOK",
    "script_text": "[câu script tương ứng]",
    "duration_seconds": 8,
    "emotion": "isolation",
    "statue_type": "bust",
    "pose": "head bowed, eyes closed, expression of quiet despair",
    "lighting": "conflict",
    "visual_note": "gợi cảm giác nặng nề, câu hỏi chưa có lời giải"
  }
]
```

### visuals.json
Danh sách các **visual asset duy nhất** cần tạo (gộp các cảnh dùng cùng visual):
```json
[
  {
    "visual_id": "v001",
    "statue_type": "bust",
    "pose": "head bowed, eyes closed, expression of quiet despair",
    "lighting": "conflict",
    "used_in_scenes": ["scene_001", "scene_003"]
  }
]
```

**Lưu ý quan trọng:** Gộp các cảnh có visual giống nhau để tiết kiệm số lần generate ảnh. Một video 35 cảnh thường chỉ cần 15–20 visual asset khác nhau.

## Quy tắc Visual EnigmaMind
- KHÔNG có nhân vật có tên, không có background phức tạp
- Tất cả background đều là **pure black** — không cần tạo background riêng
- Tượng KHÔNG bao giờ nhìn thẳng vào camera
- Vết nứt (cracks) trên tượng = biểu tượng transformation → dùng cho climax
- Ánh sáng = ý nghĩa: trên = khai ngộ, bên = mâu thuẫn, dưới = tối tăm

## Sau khi tạo xong
Hiển thị bảng tóm tắt:
| Scene | Section | Emotion | Visual ID | Duration |
|-------|---------|---------|-----------|----------|

Hỏi: **"Bạn có muốn điều chỉnh visual concept nào trước khi generate ảnh (Bước 3) không?"**
