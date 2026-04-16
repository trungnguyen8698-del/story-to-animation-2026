---
name: 03-generating-visual-images
description: Bước 3 — Đọc visuals.json và tạo prompts cho từng visual asset, sau đó chạy script Python để generate ảnh tự động. Output là ./visuals/*.png
---

# Bước 3 — Generate Hình Ảnh Visual (EnigmaMind)

## Đầu vào
File `visuals.json` từ Bước 2.

## Visual Identity EnigmaMind — BẮT BUỘC áp dụng 100%

Core Style DNA:
black and white marble statue, Classical Greek Roman sculpture style,
rough unpolished stone texture, visible chisel marks,
cinematic chiaroscuro lighting, pure black background,
monochromatic palette, timeless philosophical mood,
photorealistic stone material, museum quality sculpture photography

Negative Keywords — LUÔN bao gồm:
--no polished marble, shiny surface, colorful, vivid colors,
modern CGI, 3D render, fantasy, floating text, watermark,
photographic background, landscape, other figures, cartoon, anime,
over-smooth, perfect skin, idealized beauty, white background

## Prompt Template

Cho bust (tượng bán thân):
[POSE_DESCRIPTION], marble bust sculpture, Classical Greek Roman style,
rough stone texture with visible chisel marks, [LIGHTING_TYPE] chiaroscuro lighting,
pure black background, black and white, cinematic composition,
philosophical contemplative mood, museum photography
--ar 16:9 --v 6.1 --style raw --no polished marble, shiny, colorful, CGI, watermark

Cho full_figure (toàn thân):
[POSE_DESCRIPTION], full marble figure sculpture, Classical Greek Roman style,
rough unpolished stone, [LIGHTING_TYPE] dramatic lighting, pure black background,
monochromatic, cinematic wide shot, stoic philosophical mood
--ar 16:9 --v 6.1 --style raw --no polished marble, shiny, colorful, CGI, watermark

Cho hands (chỉ bàn tay):
[POSE_DESCRIPTION], marble hands sculpture detail, Classical Greek Roman style,
rough stone texture, [LIGHTING_TYPE] directional light, pure black background,
extreme close-up, black and white, symbolic composition
--ar 16:9 --v 6.1 --style raw --no polished marble, shiny, colorful, CGI, watermark

Cho two_figures (hai tượng):
[POSE_DESCRIPTION], two marble figures sculpture, Classical Greek Roman style,
rough stone texture, [LIGHTING_TYPE] chiaroscuro, pure black background,
monochromatic, cinematic framing, tension and contrast
--ar 16:9 --v 6.1 --style raw --no polished marble, shiny, colorful, CGI, watermark

Cho abstract_fragment:
[POSE_DESCRIPTION], marble sculpture fragment detail, Classical Greek Roman style,
rough broken stone, [LIGHTING_TYPE] dramatic lighting, pure black background,
abstract close-up, black and white, philosophical symbolism
--ar 16:9 --v 6.1 --style raw --no polished marble, shiny, colorful, CGI, watermark

## Lighting Type

enlightenment = single overhead directional
conflict = harsh side-angle single source
darkness = minimal low-key under-lit
dawn = soft gradual side-sweeping

## Tạo visuals_with_prompts.json

Đọc visuals.json, điền prompt cho từng item, lưu thành visuals_with_prompts.json.

Ví dụ một item:
visual_id: v001
statue_type: bust
pose: head bowed, eyes closed, expression of quiet despair
lighting: conflict
prompt: marble bust sculpture, head bowed with eyes closed, expression of quiet despair, Classical Greek Roman style, rough stone texture with visible chisel marks, harsh side-angle single source chiaroscuro lighting, pure black background, black and white, cinematic composition, philosophical contemplative mood --ar 16:9 --v 6.1 --style raw --no polished marble, shiny surface, colorful, modern CGI, 3D render, fantasy, watermark
used_in_scenes: scene_001, scene_003
image_url: (để trống, script sẽ điền)

## Chạy Script Generate

cd /path/to/your/project
python ~/.claude/skills/03-generating-visual-images/scripts/generate_images.py

Script sẽ:
1. Đọc visuals_with_prompts.json
2. Gọi kie.ai API để generate từng ảnh
3. Lưu vào ./visuals/v001.png, ./visuals/v002.png, ...
4. Cập nhật image_url trong JSON

## Kiểm Tra Kết Quả
- Nền đen tuyệt đối
- Tượng đá thô, có dấu đục
- Ánh sáng chiaroscuro đúng hướng
- Không có màu sắc lạ

Nếu ảnh nào không đạt thêm negative keywords cụ thể và retry.

## Sau khi hoàn thành
Hỏi: "Tất cả [X] visual đã generate xong. Bạn có muốn xem lại hoặc redo visual nào không trước khi sang Bước 4?"
