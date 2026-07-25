# Văn phong viết thesis tiếng Việt

## Nguyên tắc chung

Viết như kỹ sư hoặc nhà nghiên cứu giải thích vấn đề cho đồng nghiệp. Rõ ràng, chính xác, có căn cứ. Tránh văn phong khoa trương.

## Quy tắc rewrite (QUAN TRỌNG)

Khi rewrite, KHÔNG thêm/bớt nội dung kỹ thuật. Chỉ thay đổi:
- Marketing verbs → copula đơn giản ("có vai trò xử lý" → "xử lý")
- Bullet style → thống nhất format
- Câu dài → tách thành câu ngắn hơn (giữ nguyên ý)

## Phong cách câu

Câu ngắn đến trung bình (15-25 từ). Ưu tiên câu chủ động. Subject và verb gần nhau. Mỗi câu một ý.

**Ví dụ:**

❌ "Hệ thống, sau khi được triển khai trên Kubernetes với cấu hình autoscaling và monitoring, đã hoạt động ổn định trong suốt quá trình thử nghiệm kéo dài 30 ngày."

✓ "Hệ thống hoạt động ổn định trong 30 ngày thử nghiệm. Triển khai sử dụng Kubernetes với autoscaling và monitoring."

## Phong cách đoạn

Mỗi đoạn một ý chính. Câu đầu nêu topic. Các câu sau hỗ trợ bằng dữ liệu, ví dụ, dẫn chứng. Không kết đoạn bằng cụm rỗng như "Tóm lại" hay "Nhìn chung".

## Citation

**Inline:** "Theo Fowler (2014), microservices là..."
**LaTeX:** "...trong hệ thống phân tán \cite{opentelemetry2024}."

Luôn cite cụ thể. Không dùng "các chuyên gia", "nhiều nghiên cứu".

## Thuật ngữ

Lần đầu định nghĩa đầy đủ: "Root Cause Analysis (RCA) là quá trình xác định nguyên nhân gốc của sự cố."

Sau đó dùng viết tắt: "Thuật toán RCA của chúng tôi..."

Giữ nguyên thuật ngữ tiếng Anh phổ biến: trace, span, API, microservices, container, pod.

## Định dạng

**Bullet list:** Dùng khi liệt kê ≥3 items ngang hàng (đặc điểm, bước, yêu cầu).

**Văn xuôi:** Dùng cho giải thích, phân tích, lập luận.

**Không:** Bullet liên tục >10 items, em dash (—) nhiều, emoji, hashtag.

## Emphasis Formatting (Academic Best Practices)

Theo chuẩn academic writing, italic dùng cho thuật ngữ mới, bold hiếm khi dùng trong body text.

### Bold (`\textbf{}`)

**CHỈ dùng cho:**
- Section/subsection headings (theo template)
- Table headers

**KHÔNG dùng trong:**
- Body text
- Itemize/enumerate items
- Định nghĩa thuật ngữ

### Italic (`\textit{}`)

**Dùng cho thuật ngữ mới lần đầu xuất hiện:**

```latex
% Lần đầu giới thiệu
\textit{Root Cause Analysis} (RCA) là quá trình xác định nguyên nhân gốc...

% Lần đầu giới thiệu trong itemize
\item \textit{Latency Sensitivity Index} (LSI): Chỉ số đo mức độ nhạy cảm...

% Các lần sau - plain text
Thuật toán RCA của chúng tôi...
```

### Monospace (`\texttt{}`)

**Dùng cho:** code, variable names, commands, file paths

```latex
Hàm \texttt{calculate\_score()} trả về giá trị float.
```

### Ví dụ so sánh

❌ `\item \textbf{ClickHouse}: Cơ sở dữ liệu...` (bold trong itemize)

❌ `\item \textbf{LSI}: Chỉ số đo...` (bold cho thuật ngữ)

✓ `\item ClickHouse lưu trữ span...` (đã giới thiệu trước đó)

✓ `\item \textit{Latency Sensitivity Index} (LSI): Chỉ số đo...` (thuật ngữ mới, dùng italic)

## Nội dung kỹ thuật

Mô tả khách quan. Không phóng đại. Nêu trade-off cân bằng. Số liệu cụ thể khi có. Kết luận phải có dữ liệu hỗ trợ.

**Ví dụ:**

❌ "Thuật toán MyRCA mang tính đột phá, giải quyết triệt để vấn đề RCA trong microservices."

✓ "Thuật toán MyRCA đạt A@5 = 0.89 trên dataset Chat-Web, cao hơn 12% so với TraceRCA."

## Cấu trúc section

**Mở đầu section:** Nêu mục đích section trong 1-2 câu. Không dùng cụm mở đầu rỗng.

**Thân section:** Trình bày theo logic. Mỗi subsection một khía cạnh. Dữ liệu và ví dụ hỗ trợ.

**Kết section:** Link sang section tiếp hoặc nêu kết luận có căn cứ. Không dùng "Tóm lại, có thể thấy rằng..."
