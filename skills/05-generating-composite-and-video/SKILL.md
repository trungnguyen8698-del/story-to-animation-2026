---
name: 05-generating-composite-and-video
description: Bước 5 — Đọc shots.json, chạy script để generate video clips từng shot qua kie.ai Veo, rồi merge thành video hoàn chỉnh. Output cuối là final_video.mp4
---

# Bước 5 — Generate Video + Merge (EnigmaMind)

## Đầu vào
- shots.json từ Bước 4
- ./visuals/*.png từ Bước 3

## Workflow

### 5A. Generate Video Clips

Generate từng shot một (khuyến nghị lần đầu):
python ~/.claude/skills/05-generating-composite-and-video/scripts/generate_videos.py --shot shot_001
python ~/.claude/skills/05-generating-composite-and-video/scripts/generate_videos.py --shot shot_002

Generate tất cả cùng lúc:
python ~/.claude/skills/05-generating-composite-and-video/scripts/generate_videos.py

Script sẽ:
1. Đọc shots.json
2. Upload ảnh từ ./visuals/ lên imgbb để lấy public URL
3. Gọi kie.ai Veo API với image_url và veo_prompt
4. Download clip về ./clips/shot_001.mp4, ./clips/shot_002.mp4, ...

### 5B. Kiểm Tra Từng Clip
- Chuyển động camera đúng hướng (push in / orbit / tilt)
- Nền vẫn đen tuyệt đối, không bị màu
- Tượng không bị biến dạng quá nhiều
- Thời lượng đúng với duration_seconds

Nếu clip không đạt, chỉnh veo_prompt trong shots.json và retry:
python ~/.claude/skills/05-generating-composite-and-video/scripts/generate_videos.py --shot shot_001 --force

### 5C. Merge Thành Video Cuối

python ~/.claude/skills/05-generating-composite-and-video/scripts/merge_clips.py

Script merge sẽ:
1. Đọc thứ tự từ shots.json
2. Ghép các clip với transition theo trường transition
3. Output: final_video.mp4

## Cấu Trúc Thư Mục Cuối

my-enigmamind-video/
├── .env
├── script.md
├── scenes.json
├── visuals.json
├── visuals_with_prompts.json
├── shots.json
├── visuals/
│   ├── v001.png
│   └── v002.png
├── clips/
│   ├── shot_001.mp4
│   └── shot_002.mp4
└── final_video.mp4

## Tips Riêng Cho EnigmaMind

Về timing:
- Clip dài hơn voiceover 1–2 giây để tạo cảm giác thở
- Phần HOOK: clip ngắn 5–6 giây, cắt nhanh hơn
- Phần RESOLUTION: clip dài 8–10 giây, chậm rãi

Về chất lượng Veo:
- Prompt ngắn gọn dưới 150 từ cho kết quả tốt hơn
- Luôn đặt slow motion và cinematic vào prompt
- Tránh mô tả quá nhiều chuyển động

Về màu sắc:
- Nếu Veo ra clip có màu nhẹ, xử lý desaturate trong CapCut
- Trong CapCut: Filters → B&W → chọn filter phù hợp

Retry an toàn:
- Script bỏ qua file đã tồn tại, re-run không bị overwrite
- Dùng --force để override clip cụ thể

## Post-Production trong CapCut

1. Import final_video.mp4
2. Thêm voiceover từ tool TTS của bạn
3. Sync voiceover với từng shot theo voiceover_text trong shots.json
4. Thêm nhạc nền: ambient cinematic instrumental, volume 20%
5. Color grade: tăng contrast, giảm brightness nhẹ
6. Export: 1080p 30fps

## Sau khi hoàn thành
"Video hoàn chỉnh đã xuất tại final_video.mp4. Pipeline EnigmaMind đã chạy xong toàn bộ 5 bước!"
