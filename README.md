# EnigmaMind Video Pipeline

Biến một chủ đề triết học thành video YouTube hoàn chỉnh cho kênh EnigmaMind trong 5 bước, chạy trực tiếp với Claude Code + kie.ai.

---

## Pipeline Overview

Chủ đề → script.md → scenes.json / visuals.json → ảnh tượng đá → shots.json → video clips → final_video.mp4
  Bước 1     Bước 2           Bước 3 (script)          Bước 4        Bước 5 (script)

| Bước | Skill | Công cụ | Output |
|------|-------|---------|--------|
| 1 | 01-generating-script-from-topic | Claude | script.md |
| 2 | 02-extracting-scenes-and-visuals | Claude | scenes.json, visuals.json |
| 3 | 03-generating-visual-images | Script + kie.ai | ./visuals/*.png |
| 4 | 04-creating-shot-list | Claude | shots.json |
| 5 | 05-generating-composite-and-video | Script + kie.ai | ./clips/*.mp4 → final_video.mp4 |

---

## Visual Identity EnigmaMind

Mọi hình ảnh đều theo phong cách thống nhất:
- Tượng đá cẩm thạch đen trắng, phong cách Hy Lạp / La Mã cổ điển
- Chiaroscuro cinematic — ánh sáng tương phản cao
- Nền đen tuyệt đối — pure black background
- Kết cấu thô — rough stone, visible chisel marks
- Tông triết học — trầm tư, nội tâm, timeless

---

## Yêu Cầu

- Python 3.8+
- FFmpeg
- API keys: kie.ai + imgbb

Cài dependencies:
pip install -r requirements.txt

Cài FFmpeg:
Mac: brew install ffmpeg
Windows: winget install ffmpeg

---

## Cài Đặt

1. Clone repo:
git clone https://github.com/trungnguyen8698-del/story-to-animation-2026.git
cd story-to-animation-2026

2. Cài dependencies:
pip install -r requirements.txt

3. Tạo file .env:
cp .env.example .env
Mở .env và điền KIE_API_TOKEN và IMGBB_API_KEY

4. Cài skills vào Claude Code:
cp -r skills/* ~/.claude/skills/

---

## Sử Dụng

Bước 1 và 2 — dùng Claude Code:
Nhắn với Claude: "Tạo script EnigmaMind về chủ đề [chủ đề của bạn]"
Claude tự động dùng skill, dừng lại chờ bạn duyệt sau mỗi bước.

Bước 3 — generate ảnh:
cd /path/to/your/project
python ~/.claude/skills/03-generating-visual-images/scripts/generate_images.py

Bước 4 — dùng Claude Code:
Nhắn: "Tạo shot list EnigmaMind từ scenes.json và visuals đã có"

Bước 5 — generate video:
Từng shot:
python ~/.claude/skills/05-generating-composite-and-video/scripts/generate_videos.py --shot shot_001

Tất cả cùng lúc:
python ~/.claude/skills/05-generating-composite-and-video/scripts/generate_videos.py

Merge thành video cuối:
python ~/.claude/skills/05-generating-composite-and-video/scripts/merge_clips.py

---

## Cấu Trúc Thư Mục Project

my-enigmamind-video/
├── .env
├── script.md
├── scenes.json
├── visuals.json
├── visuals_with_prompts.json
├── shots.json
├── visuals/
├── clips/
└── final_video.mp4

---

## Tips

- Kiểm tra từng bước trước khi tiếp tục — mỗi skill sẽ hỏi bạn duyệt
- Reuse visuals: nhiều cảnh có thể dùng cùng 1 ảnh để tiết kiệm API calls
- Per-shot mode: dùng --shot để xem từng clip trước khi merge
- CapCut: thêm voiceover và nhạc nền sau khi có final_video.mp4

---

## License

MIT — Fork từ ducloc99/story-to-animation-2026, chỉnh sửa cho kênh EnigmaMind.
