---
name: 06-generating-short-video
description: Tạo video short 60 giây cho kênh EnigmaMind theo 2 mode: Mode A trích đoạn hay từ video dài có sẵn, Mode B nội dung độc lập hoàn toàn. Aspect ratio 9:16, 6–10 cảnh, cấu trúc Hook → Punch → Kết. Dùng skill này khi người dùng nhắc đến short, reels, 60 giây, trích đoạn, hoặc nội dung ngắn cho EnigmaMind.
---

# Bước 6 — Tạo Short Video 60 Giây (EnigmaMind)

## Đầu vào
Người dùng cung cấp một trong:
- script.md từ pipeline video dài (Mode A)
- Chủ đề / câu quote ngắn (Mode B)

## Xác Định Mode

Hỏi người dùng nếu chưa rõ:
"Bạn muốn làm short theo mode nào?
- Mode A: Trích đoạn hay từ video dài có sẵn
- Mode B: Nội dung độc lập hoàn toàn mới"

---

## MODE A — Trích Đoạn Từ Video Dài

### Nhiệm vụ
Đọc script.md → tìm đoạn hay nhất có thể đứng độc lập trong 60 giây.

### Tiêu chí chọn đoạn
- Có hook mạnh ngay câu đầu
- Chứa một insight hoàn chỉnh, không cần context trước đó
- Kết thúc có cảm giác đủ, không bị lửng
- Ưu tiên phần CONFLICT hoặc RESOLUTION — thường là đoạn cảm xúc nhất

### Xử lý sau khi chọn
1. Cắt và chỉnh sửa nhẹ để đoạn tự nhiên khi đứng độc lập
2. Thêm câu hook nếu đoạn gốc bắt đầu quá chậm
3. Thêm câu kết nếu đoạn gốc kết thúc lửng
4. Giữ nguyên tone và giọng văn EnigmaMind

---

## MODE B — Nội Dung Độc Lập

### Cấu trúc 60 giây (120 từ tối đa)

HOOK (0–5 giây) — 1 câu duy nhất, gây chấn động:
- Câu hỏi nghịch lý HOẶC
- Tuyên bố phản trực giác HOẶC
- Câu quote triết học mạnh

PUNCH (5–50 giây) — 1 insight duy nhất, đào sâu:
- Không cố nhồi nhiều ý
- 1 concept, giải thích rõ ràng trong 3–4 câu
- Ví dụ cụ thể hoặc trích dẫn Stoic / Jung

KẾT (50–60 giây) — 1 câu để lại:
- Câu hỏi mở hoặc
- Câu tuyên bố đóng lại bất ngờ
- Không CTA trực tiếp

---

## Thông Số Kỹ Thuật Short

Aspect ratio: 9:16 (dọc)
Số cảnh: 6–10
Thời lượng mỗi cảnh: 5–8 giây
Tổng: 60 giây

## Visual Cho Short

Giữ nguyên Visual Identity EnigmaMind:
- Tượng đá marble đen trắng
- Chiaroscuro cinematic
- Nền đen tuyệt đối

Khác biệt so với video dài:
- Ưu tiên bust và hands — close-up mạnh hơn cho màn hình dọc
- Camera move nhanh hơn nhẹ: slow_push_in là chủ đạo
- Mỗi cảnh ngắn hơn: 5–6 giây thay vì 8–10 giây
- Composition tập trung vào trung tâm màn hình — tránh chi tiết ở góc

## Prompt Điều Chỉnh Cho 9:16

Thêm vào tất cả prompts:
--ar 9:16

Thêm vào Veo prompts:
vertical composition, centered framing, portrait orientation

## Output

Tạo short_script.md với cấu trúc:
- Mode đang dùng (A hoặc B)
- Nội dung script 60 giây
- Ghi chú visual từng cảnh

Sau đó tạo short_scenes.json và short_shots.json theo cùng format của pipeline dài nhưng với thông số short.

## Sau khi hoàn thành
Hỏi: "Short script đã sẵn sàng. Bạn muốn dùng visual từ video dài có sẵn hay generate visual mới?"

Nếu dùng visual cũ: bỏ qua Bước 3, chạy thẳng Bước 4 và 5 với thông số 9:16
Nếu cần visual mới: chạy lại Bước 3 với --ar 9:16
