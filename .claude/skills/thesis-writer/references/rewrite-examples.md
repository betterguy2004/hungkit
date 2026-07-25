# Ví dụ viết lại

## Example 1: Cụm sáo rỗng

**Before:**
> Distributed tracing đóng vai trò quan trọng và không thể thiếu trong việc giám sát hệ thống microservices hiện đại.

**After:**
> Distributed tracing cho phép theo dõi request qua nhiều service và xác định điểm gây lỗi.

**Thay đổi:** Bỏ "đóng vai trò quan trọng", "không thể thiếu". Nêu cụ thể chức năng.

---

## Example 2: Cụm mở đầu rỗng

**Before:**
> Cần lưu ý rằng trong bối cảnh hiện nay, với sự phát triển không ngừng của công nghệ cloud, việc áp dụng Kubernetes trở nên phổ biến.

**After:**
> Kubernetes được áp dụng rộng rãi để orchestrate container workloads.

**Thay đổi:** Bỏ toàn bộ opener. Nói thẳng vào vấn đề.

---

## Example 3: Vague Attribution

**Before:**
> Các chuyên gia cho rằng MLOps giúp cải thiện quy trình triển khai mô hình ML.

**After:**
> Theo Sculley et al. (2015), technical debt trong ML systems chủ yếu đến từ quy trình deployment, không phải model code.

**Thay đổi:** Citation cụ thể. Nêu insight cụ thể thay vì claim chung.

---

## Example 4: Phóng đại

**Before:**
> Thuật toán MyRCA mang tính đột phá, thay đổi cuộc chơi trong lĩnh vực RCA.

**After:**
> Thuật toán MyRCA cải thiện A@5 từ 0.77 (TraceRCA) lên 0.89 trên dataset Chat-Web.

**Thay đổi:** Thay claim phóng đại bằng số liệu cụ thể.

---

## Example 5: Marketing Verb

**Before:**
> Hệ thống MLOps mang đến khả năng tự động tái huấn luyện mô hình khi phát hiện data drift.

**After:**
> Hệ thống MLOps tự động tái huấn luyện mô hình khi PSI > 0.2.

**Thay đổi:** "mang đến khả năng" bỏ đi. Nói thẳng chức năng với threshold cụ thể.

---

## Example 6: Câu dài

**Before:**
> Kiến trúc microservices, vốn được phát triển nhằm giải quyết các vấn đề về scalability và maintainability của monolithic architecture, hiện đang được áp dụng rộng rãi trong các hệ thống enterprise với quy mô lớn.

**After:**
> Kiến trúc microservices giải quyết vấn đề scalability và maintainability của monolithic. Các hệ thống enterprise lớn như Netflix, Uber áp dụng kiến trúc này.

**Thay đổi:** Tách thành 2 câu. Thêm ví dụ cụ thể.

---

## Example 7: Bullet không cần thiết

**Before:**
> Các ưu điểm của microservices:
> - Scalability
> - Maintainability  
> - Flexibility

**After:**
> Microservices cho phép scale từng service độc lập. Mỗi team có thể maintain service riêng mà không ảnh hưởng team khác. Các service có thể sử dụng technology stack khác nhau.

**Thay đổi:** Chuyển bullet thành văn xuôi với giải thích cụ thể.

---

## Example 8: Kết luận không căn cứ

**Before:**
> Kết quả cho thấy hệ thống có tiềm năng ứng dụng rộng rãi và sẽ mang lại giá trị lớn cho cộng đồng.

**After:**
> Hệ thống xử lý được 1000 traces/giây với latency p99 < 50ms trên 3-node cluster.

**Thay đổi:** Thay claim mơ hồ bằng số liệu đo được.

---

## Example 9: Negative Parallelism

**Before:**
> Không chỉ là công cụ giám sát, distributed tracing còn là nền tảng cho việc phân tích nguyên nhân gốc.

**After:**
> Distributed tracing vừa giám sát hệ thống vừa cung cấp dữ liệu cho RCA.

**Thay đổi:** Bỏ "Không chỉ...còn là". Nói thẳng.
