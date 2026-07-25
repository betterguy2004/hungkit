# Patterns cần tránh

## 1. Cụm từ sáo rỗng (HIGH severity)

| Cụm từ | Vấn đề |
|--------|--------|
| đóng vai trò quan trọng | Sáo rỗng, không cụ thể |
| mang tính đột phá | Phóng đại |
| thay đổi cuộc chơi | Marketing |
| có ảnh hưởng sâu rộng | Mơ hồ |
| vô cùng quan trọng | Phóng đại |
| không thể thiếu | Tuyệt đối hóa |
| là yếu tố quyết định | Phóng đại |
| có tầm quan trọng đặc biệt | Sáo rỗng |

## 2. Cụm mở đầu rỗng (MEDIUM severity)

| Cụm từ | Action |
|--------|--------|
| Cần lưu ý rằng... | Bỏ, nói thẳng |
| Điều đáng chú ý là... | Bỏ, nói thẳng |
| Có thể thấy rằng... | Bỏ, nói thẳng |
| Tóm lại... | Bỏ nếu không tóm tắt thực sự |
| Nhìn chung... | Bỏ, nói thẳng |
| Trong bối cảnh hiện nay... | Bỏ hoặc "Hiện nay" |
| Với sự phát triển không ngừng của... | "Khi X phát triển" |
| Không thể phủ nhận rằng... | Bỏ |
| Như chúng ta đã biết... | Bỏ |
| Thực tế cho thấy... | "Theo [cite]" |
| Đáng chú ý là... | Bỏ |
| Có thể nói rằng... | Bỏ, khẳng định thẳng |

## 3. Từ vựng phóng đại (MEDIUM severity)

| Pattern | Alternative |
|---------|-------------|
| bức tranh toàn cảnh | tình hình, hiện trạng |
| quan trọng then chốt | cần thiết |
| mang tính bước ngoặt | đáng chú ý |
| đào sâu vào | phân tích |
| minh chứng rõ ràng | cho thấy |
| sống động, phong phú | đa dạng |
| toàn diện | đầy đủ |
| triệt để | hoàn toàn |

## 4. Marketing Verbs (MEDIUM severity)

| Pattern | Alternative |
|---------|-------------|
| đóng vai trò là | là |
| mang đến, mang lại | có, tạo ra |
| góp phần vào | giúp |
| phục vụ cho mục đích | dùng để |
| thể hiện vai trò của | cho thấy |
| tự hào với | có |

## 5. Vague Attribution (HIGH severity)

| Pattern | Fix |
|---------|-----|
| Các chuyên gia cho rằng | Theo [Author] (Year) |
| Nhiều nghiên cứu chỉ ra | [Author1], [Author2] chỉ ra |
| Theo các nhà nghiên cứu | Theo [Author] (Year) |
| Có ý kiến cho rằng | Nêu rõ ai |
| Một số người tin rằng | Cite hoặc bỏ |
| Các tài liệu cho thấy | [Author] (Year) trình bày |

## 6. Structural Patterns (LOW severity)

**Rule of Three liên tục:**
Pattern: "X, Y, và Z" xuất hiện nhiều lần.
Fix: Vary lengths (2, 4, 5 items).

**Negative Parallelism:**
Pattern: "Không chỉ X mà còn Y", "Không đơn thuần là X".
Fix: Nói thẳng "X và Y".

**Challenges & Future formula:**
Pattern: "Mặc dù còn hạn chế, X có tiềm năng lớn..."
Fix: Nêu cụ thể limitations và hướng fix.

## Detection Rules

**HIGH:** ≥2 cụm sáo rỗng hoặc vague attribution trong cùng section.
**MEDIUM:** ≥3 cụm mở đầu rỗng hoặc marketing verbs.
**LOW:** Issues lẻ tẻ, structural patterns.
