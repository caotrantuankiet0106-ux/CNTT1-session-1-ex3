# Phần 1: Phân tích cơ chế BPE và lý do Mẫu B tốn gấp 2.4 lần Token
Cơ chế cắt từ của BPE: LLM đếm theo các đơn vị từ nhỏ (sub-word units). Do dữ liệu tiếng Việt trong giai đoạn Pre-training rất ít, thuật toán BPE không nhận diện được các từ có dấu mà phải "băm" nhỏ từ tiếng Việt thành các ký tự gốc hoặc dấu thanh riêng lẻ.

Nguyên nhân chênh lệch:

Mẫu A (Tiếng Anh): Các từ phổ biến khớp trực tiếp với từ vựng của LLM, tốn ít token (1.18 Tokens/từ).

Mẫu B (Tiếng Việt): Các từ có dấu bị vỡ thành nhiều sub-word, đẩy tỷ lệ lên 2.85 Tokens/từ (cao gấp ~2.4 lần so với Mẫu A). Thắc mắc của Hoàng về việc "đếm trùng" là không chính xác; nguyên nhân thực chất là do cách chia mảnh ký tự của BPE.

# Phần 2: Hai kỹ thuật Prompt Tiếng Việt tối ưu Token (Tiết kiệm 30-40%)
Kỹ thuật dùng từ khóa kết hợp (Keyword-driven Prompting): Giữ lại các từ khóa chuyên ngành/tên riêng bằng tiếng Anh (mật độ token tối ưu) và lược bỏ từ nối rườm rà.

Ví dụ: "Viết ad copy MartX: organic vegetables, fresh, best quality."

Kỹ thuật cấu trúc tối giản (Markdown Table/Bullet Points): Yêu cầu AI trả kết quả dạng gạch đầu dòng cô đọng để hạn chế tối đa các từ diễn giải chứa dấu thanh gây vỡ token.
