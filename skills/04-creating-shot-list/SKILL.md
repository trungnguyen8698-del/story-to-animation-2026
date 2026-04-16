---
name: 04-creating-shot-list
description: Bước 4 — Kết hợp scenes.json và visuals_with_prompts.json để tạo shots.json hoàn chỉnh với Veo video prompts cho từng cảnh. Output là shots.json để dùng ở Bước 5.
---

# Bước 4 — Tạo Shot List + Veo Prompts (EnigmaMind)

## Đầu vào
- scenes.json từ Bước 2
- visuals_with_prompts.json từ Bước 3
- script.md để lấy voiceover text

## Nhiệm vụ
Tạo shots.json — file điều phối toàn bộ video, mỗi shot chứa đủ thông tin để:
1. Generate video clip từ ảnh
2. Ghép voiceover đúng thời điểm

## Output Format — shots.json

Mỗi shot có cấu trúc:
shot_id: shot_001
scene_id: scene_001
script_section: HOOK
voiceover_text: (câu script tiếng Việt cho cảnh này)
duration_seconds: 8
visual_id: v001
image_url: (url ảnh từ visuals_with_prompts.json)
camera_move: slow_push_in
veo_prompt: (xem format bên dưới)
transition: dissolve

## Camera Move Options

slow_push_in — tiến chậm vào chủ thể — dùng cho Hook, điểm nhấn
slow_orbit_right — bay vòng sang phải — dùng cho Reveal, introduce
gentle_tilt_up — ngước lên chậm — dùng cho Resolution, khai ngộ
static_light_shift — đứng yên ánh sáng thay đổi — dùng cho Contemplation
slow_pull_back — lùi ra xa — dùng cho Outro, kết thúc
static — hoàn toàn tĩnh — dùng khi voiceover nặng cần tập trung nghe

## Veo Prompt Template

[STATUE_DESCRIPTION] on pure black background, cinematic [CAMERA_MOVE] motion,
black and white marble sculpture aesthetic, Classical Greek Roman style,
chiaroscuro lighting with [LIGHTING_DIRECTION],
[ATMOSPHERIC_DETAIL], 4K cinematic quality, slow motion,
philosophical contemplative atmosphere, dust particles in light beam,
no color, monochromatic stone texture

## Atmospheric Details theo Emotion

isolation = silence and stillness, frozen in time
conflict = subtle light flicker suggesting inner turmoil
enlightenment = light intensifying gradually from above
despair = shadows deepening, minimal highlight
transformation = hairline crack forming on stone surface, light emerging
acceptance = warm light slowly washing over the figure
contemplation = dust motes floating gently in a single shaft of light

## Ví dụ Veo Prompt hoàn chỉnh

Marble bust sculpture with head bowed and eyes closed on pure black background,
cinematic slow push in motion, black and white marble sculpture aesthetic,
Classical Greek Roman style, chiaroscuro lighting with harsh side-angle single source,
silence and stillness frozen in time, 4K cinematic quality, slow motion,
philosophical contemplative atmosphere, dust particles in shaft of light,
no color, monochromatic rough stone texture

## Quy tắc Ghép Shot

- Đầu mỗi section (HOOK, CONCEPT, CONFLICT, RESOLUTION, OUTRO): dùng slow_push_in hoặc slow_orbit_right
- Giữa section: static hoặc static_light_shift để không phân tán khỏi voiceover
- Climax đỉnh điểm CONFLICT: static với atmospheric transformation
- Outro cuối cùng: slow_pull_back rồi fade to black

## Kiểm Tra Trước Khi Lưu
- Mỗi shot có đủ visual_id và image_url
- Tổng duration_seconds khớp với độ dài script
- Veo prompt không vượt quá 200 từ
- Transition: dissolve cho phần trầm tư, cut cho điểm nhấn mạnh

## Sau khi hoàn thành
Hiển thị bảng tóm tắt toàn bộ shot list:
| Shot | Section | Duration | Camera | Visual |

Hỏi: "Shot list đã sẵn sàng với [X] shots, tổng [Y] phút. Bạn muốn điều chỉnh gì không trước khi generate video (Bước 5)?"
