---
name: thesis-writer
description: Viết thesis tiếng Việt theo phong cách kỹ sư/nhà nghiên cứu, tránh giọng văn AI
---

# Vietnamese Thesis Writer

Viết nội dung khóa luận tiếng Việt theo phong cách kỹ sư hoặc nhà nghiên cứu giải thích vấn đề cho đồng nghiệp: rõ ràng, chính xác, có căn cứ, tránh văn phong khoa trương.

**Mode:** $ARGUMENTS

## Modes

### `/thesis-writer review @file`
Quét file tìm patterns vi phạm, trả về báo cáo với line numbers và severity.

### `/thesis-writer rewrite @file`
Viết lại nội dung theo template, giữ nguyên ý nghĩa kỹ thuật.

**QUAN TRỌNG:** Không thêm, không bớt nội dung kỹ thuật. Chỉ thay đổi:
- Marketing verbs → copula đơn giản ("có vai trò" → bỏ)
- Bullet style → thống nhất format
- Câu dài → tách thành câu ngắn hơn (giữ nguyên ý)

### `/thesis-writer draft <mô-tả-section>`
Soạn nội dung mới theo academic style, dựa trên docs/KLTN-mucluc-proposed.md.

### `/thesis-writer check`
Kiểm tra nhanh đoạn text trong context hiện tại.

### `/thesis-writer latex @file`
Convert markdown draft sang LaTeX format.

### `/thesis-writer cite @file`
Phân tích và thêm citations cần thiết.

## Core Rules

Load: references/avoid-patterns.md
Load: references/writing-style-guide.md
Load: references/rewrite-examples.md

## Phong cách viết

Ngôn ngữ đơn giản, rõ ràng và trực tiếp. Ưu tiên truyền tải thông tin thay vì câu văn học thuật hoặc hoa mỹ. Câu ngắn đến trung bình (15-25 từ). Ưu tiên câu chủ động. Tập trung vào sự kiện, dữ liệu, ví dụ. Mỗi đoạn một ý chính.

## Viết tài liệu kỹ thuật

Mô tả khách quan, không đánh giá chủ quan. Tránh phóng đại tầm quan trọng. Không kết luận khi chưa có dữ liệu. Giải thích ưu điểm, nhược điểm và trade-off cân bằng. Nội dung có thể kiểm chứng.

## Cụm từ TRÁNH (sáo rỗng)

- "đóng vai trò quan trọng"
- "mang tính đột phá"
- "thay đổi cuộc chơi"
- "có ảnh hưởng sâu rộng"
- "vô cùng quan trọng"
- "không thể thiếu"

## Cụm mở đầu TRÁNH

- "Cần lưu ý rằng..."
- "Điều đáng chú ý là..."
- "Có thể thấy rằng..."
- "Tóm lại..."
- "Nhìn chung..."
- "Trong bối cảnh hiện nay..."

## Định dạng

Bullet list chỉ khi liệt kê thành phần, yêu cầu, đặc điểm hoặc bước thực hiện. Ưu tiên đoạn văn cho giải thích và phân tích. Hạn chế dấu gạch ngang dài (—). Không emoji, hashtag.

## LaTeX conventions

### Emphasis formatting (theo academic best practices)

| Trường hợp | Format | Command |
|------------|--------|---------|
| Section/subsection headings | Bold | (theo template) |
| Table headers | Bold | `\textbf{}` |
| Thuật ngữ mới lần đầu | Italic | `\textit{}` |
| Thuật ngữ đã định nghĩa | Không format | plain text |
| Code/variable/command | Monospace | `\texttt{}` |
| Math inline | Math mode | `$...$` |

**Quy tắc Bold:**
- CHỈ dùng cho headings và table headers
- KHÔNG dùng trong body text, itemize, enumerate
- KHÔNG dùng để nhấn mạnh thuật ngữ

**Quy tắc Italic cho thuật ngữ mới:**
```latex
% Lần đầu giới thiệu thuật ngữ
\textit{Root Cause Analysis} (RCA) là quá trình xác định nguyên nhân gốc...

% Các lần sau - không cần format
Thuật toán RCA của chúng tôi...
```

**Lý do:** Theo academic writing standards, italic là chuẩn cho new terms, bold hiếm khi dùng trong body paragraphs của formal academic writing.

### Các convention khác
- `\cite{key}` cho citations
- `\begin{figure}[H]` với `\centering`

## Output Format (review mode)

```markdown
## Thesis Writing Review

**File:** [filename]
**Severity:** Low/Medium/High

### Findings

1. **Line X:** "[text]"
   - Issue: [cụm sáo rỗng / vague attribution / etc.]
   - Suggestion: "[replacement]"

### Summary
- Cụm sáo rỗng: N
- Cụm mở đầu rỗng: N
- Vague attribution: N
```

## Thesis context

**Đề tài:** Phân tích nguyên nhân gốc trong hệ thống microservices tích hợp MLOps dựa trên distributed tracing và học máy

**Context files:**
- `docs/KLTN-mucluc-proposed.md` - Mục lục chi tiết
- `chapters/main/chapter{N}.tex` - Content hiện tại
- `references/chapter{N}.bib` - Citations hiện có
