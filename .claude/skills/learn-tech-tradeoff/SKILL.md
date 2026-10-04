---
name: learn-tech-tradeoff
description: Dùng skill này bất cứ khi nào người dùng muốn HỌC SÂU / tìm hiểu / ôn một công nghệ, component, tool, giao thức hay khái niệm hệ thống (Kubernetes, etcd, Kafka, Istio, Terraform, Nomad, Consul, VPC/TGW, Raft, Redis...) theo hướng hiểu bản chất thay vì học thuộc. Trigger khi người dùng nói "học X theo trade-off", "đặt câu hỏi giúp tôi học X", "X giải quyết vấn đề gì", "tại sao cần X", "X hỏng thì sao", "câu hỏi phỏng vấn về X", "ôn X", "tôi muốn hiểu X chứ không học thuộc", hoặc chỉ đưa tên một công nghệ kèm ý định học/chuẩn bị phỏng vấn. Skill sinh bộ câu hỏi Why / Trade-off / Failure + lab kiểm chứng + câu hỏi phỏng vấn thường gặp + lịch ôn. Ưu tiên dùng skill này thay vì giải thích tổng quan thông thường khi mục tiêu là hiểu sâu để vận hành hoặc phỏng vấn.
---

# Học công nghệ từ vấn đề và trade-off

Mục tiêu: giúp người học tự xây mental model về *vì sao công nghệ này tồn tại, nó đánh đổi gì, và nó hỏng như thế nào*, thay vì nhớ danh sách tính năng.

## Vì sao thiết kế như vậy (để áp dụng đúng tinh thần)

Nghiên cứu về học tập (Dunlosky et al. 2013; Roediger & Pyc) cho thấy:
- **Practice testing / retrieval practice** hiệu quả cao nhất: tự nhớ lại và trả lời câu hỏi tốt hơn đọc lại. Vì vậy **đưa câu hỏi trước, để người học tự thử trả lời rồi mới xem đáp án**. Đừng đổ sẵn đáp án đầy đủ ngay.
- **Elaborative interrogation** (hỏi "tại sao/như thế nào") và **self-explanation** có hiệu quả vừa, nhưng cần *kiến thức nền tối thiểu* để tự giải thích. Vì vậy mở đầu bằng một mental model ngắn trước khi hỏi.
- **Spaced practice** và **interleaving** (trộn các chủ đề liên quan) giúp nhớ lâu. Vì vậy kết thúc bằng lịch ôn và câu hỏi so sánh chéo.
- Đọc lại và highlight kém hiệu quả, nên không dùng làm phương pháp chính.

## Quy trình

1. **Xác định phạm vi và mục tiêu học.** Nếu người dùng chỉ đưa tên tech, mặc định học *một component/khái niệm* mỗi lần (ví dụ "etcd trong Kubernetes", không phải "toàn bộ Kubernetes"). Xác định người dùng muốn hiểu để sử dụng, debug production, thiết kế hệ thống, chuẩn bị phỏng vấn hay so sánh lựa chọn. Phạm vi quá rộng thì đề xuất chia nhỏ. Nếu biết nền tảng của người học (qua ngữ cảnh hoặc bộ nhớ), dùng nó để so sánh với công nghệ họ đã quen. Chỉ hỏi lại tối đa 1 câu khi thật sự thiếu thông tin.
2. **Nêu các giả định ban đầu.** Ghi rõ workload, quy mô dữ liệu, tốc độ tăng trưởng, yêu cầu latency/throughput, availability/durability, mức chấp nhận mất dữ liệu hoặc eventual consistency, năng lực team và yêu cầu môi trường. Nếu chưa biết, đánh dấu là giả định cần kiểm chứng thay vì coi là sự thật.
3. **Kiểm tra độ mới.** Với tool có phiên bản (k8s, Istio, Terraform...), hành vi mặc định và giới hạn đổi theo version. Dùng web search/tài liệu chính thức để xác minh các con số và hành vi cụ thể. Không bịa số liệu; nếu không chắc, nói rõ và chỉ tới đúng trang docs.
4. **Viết mental model ngắn** (3-5 dòng): component này là gì, nằm ở đâu, tương tác với ai.
5. **Sinh bộ câu hỏi** theo 6 nhóm bên dưới.
6. **Đề xuất lab kiểm chứng** và **câu hỏi phỏng vấn**.
7. **Chốt bằng lịch ôn** và 2-3 câu so sánh chéo.

## 6 nhóm câu hỏi

Mỗi nhóm 2-4 câu, chọn câu *đặc thù cho tech đó*, không nhồi câu chung chung. Mỗi câu nên đủ cụ thể để trả lời được bằng 2-5 câu.

1. **Why (vấn đề gốc):** Nếu không có nó thì chuyện gì xảy ra? Vấn đề nào ở thế hệ giải pháp trước khiến nó ra đời? Nó giả định điều gì về môi trường?
2. **Mechanism (cơ chế tối thiểu):** Dữ liệu/luồng điều khiển đi qua nó như thế nào? Trạng thái nào được lưu ở đâu? Mô tả luồng một request/một thay đổi từ đầu đến cuối.
3. **Trade-off — 80/20 cho production và phỏng vấn:** Mỗi tech chỉ cần tập trung vào 2-3 trade-off quan trọng nhất và trả lời 4 câu:
   1. Nó tối ưu điều gì, và phải đánh đổi điều gì để đạt được điều đó?
   2. Trong điều kiện nào nó hiệu quả? Khi nào không nên dùng?
   3. Cái giá thực tế khi vận hành production là gì? Tập trung vào failure handling, monitoring, backup/restore, upgrade, debugging, resource usage và on-call.
   4. Nếu workload hoặc giả định chính thay đổi, quyết định này còn đúng không? Cần theo dõi metric hoặc dấu hiệu nào để phát hiện nó không còn phù hợp?
4. **Alternatives — quyết định lựa chọn:** Có giải pháp đơn giản hơn nào đủ đáp ứng yêu cầu hiện tại không? Vì sao chọn công nghệ này thay vì giải pháp thay thế phổ biến nhất? Điều kiện nào khiến lựa chọn thay thế trở nên hợp lý hơn?
5. **Failure (hỏng thì sao):** Với mỗi failure mode quan trọng, yêu cầu người học dự đoán theo mẫu: *triệu chứng quan sát được -> giả thuyết nguyên nhân -> cách kiểm chứng (lệnh, log, metric) -> cách khắc phục/phòng ngừa*. Bao gồm: mất một phần, mất quorum/toàn bộ, chậm (degraded), cấu hình sai, dữ liệu hỏng, hết tài nguyên. Hỏi thêm: failure nào có thể tự phục hồi, failure nào cần can thiệp thủ công?
6. **Limits & Ops (giới hạn và vận hành):** Giới hạn scale/kích thước, thứ gì sẽ nghẽn trước, cần monitor metric nào, backup/restore/upgrade ra sao, thêm/bớt node tốn gì.

## Lab kiểm chứng

Đề xuất 3-4 thí nghiệm nhỏ chạy được trên môi trường local/dev (kind, K3s, docker compose, LocalStack, free tier...). Mỗi lab theo mẫu: **Giả thuyết -> Cách làm -> Quan sát cần ghi lại -> Kết quả có khớp giả thuyết không? -> Mental model cần sửa gì? -> Đối chiếu với docs**. Ưu tiên lab *phá hoại có kiểm soát* (dừng node, làm chậm disk, xóa config, cắt mạng) vì đây là nơi học được phần Failure. Không đề xuất thử nghiệm phá hoại trên môi trường production.

## Câu hỏi phỏng vấn

Sinh 8-12 câu, chia theo cấp độ và loại, mỗi câu kèm **"Câu trả lời tốt cần có"** (2-4 ý chính, gấp lại/để cuối để người học tự trả lời trước):

- **Nền tảng (junior):** X là gì, giải quyết vấn đề gì.
- **Trade-off (mid):** "Vì sao chọn X thay vì Y?", "Cái giá của X là gì?"
- **Troubleshooting theo tình huống (mid/senior):** "Sáng nay Z bị lỗi triệu chứng T, bạn điều tra thế nào?" Câu trả lời tốt đi theo thứ tự giả thuyết và kiểm chứng, không nhảy vào kết luận.
- **Thiết kế/Scale (senior):** "Thiết kế X cho 10x tải/multi-region/multi-account thì thay đổi gì?"
- **Gotcha:** các hiểu lầm phổ biến (ví dụ "thêm node có tăng write throughput không?").

Chỉ đưa các câu thực sự hay gặp hoặc thực sự phân biệt được người hiểu và người học thuộc. Nếu không chắc một câu có "hay gặp" hay không, đừng gán nhãn đó cho nó.
Không để phần phỏng vấn lấn át mục tiêu chính là hiểu và vận hành công nghệ.

## Định dạng đầu ra

Giữ ngắn gọn, ưu tiên tiếng Việt kèm thuật ngữ tiếng Anh. Dùng đúng khung sau:

```
# [Tech]: học từ vấn đề và trade-off
**Mục tiêu học:** ...
**Phạm vi:** ...
**Giả định cần kiểm tra:** ...
**Mental model (3-5 dòng):** ...

## 1. Why  ## 2. Mechanism  ## 3. Trade-off  ## 4. Alternatives  ## 5. Failure  ## 6. Limits & Ops
(mỗi mục: danh sách câu hỏi đánh số)

## Lab kiểm chứng
## Câu hỏi phỏng vấn
## Lịch ôn
- Sau 1 ngày: tự trả lời lại nhóm Why + Failure không nhìn tài liệu
- Sau 3 ngày: Trade-off + Alternatives
- Sau 7 ngày: làm lại 1 lab + 3 câu phỏng vấn
- Sau 21 ngày: câu so sánh chéo
## So sánh chéo (interleaving)
2-3 câu đặt tech này cạnh một tech liên quan
```

Sau khi đưa bộ câu hỏi, đề nghị **chế độ hỏi-đáp từng câu**: Claude hỏi một câu,
người học trả lời, Claude chấm theo một trong bốn mức sau rồi chỉ ra lỗ hổng và hỏi
câu tiếp theo, ưu tiên các câu người học trả lời yếu:

- **Đúng:** mental model đúng và nêu được điều kiện áp dụng.
- **Thiếu:** kết luận đúng nhưng thiếu cơ chế, giới hạn hoặc chi phí vận hành.
- **Sai:** nhầm nguyên lý, phạm vi hoặc giả định.
- **Chưa kiểm chứng:** suy luận hợp lý nhưng chưa có evidence từ lab, metric hoặc tài liệu.

Đây là cách áp dụng retrieval practice hiệu quả nhất.

## Lưu ý

- Chỉ đưa đáp án đầy đủ khi người dùng yêu cầu, hoặc sau khi họ đã thử trả lời. Nếu người dùng muốn "giải đáp nhanh", cứ trả lời trực tiếp.
- Không cực đoan: cú pháp, tên flag, giá trị quy ước thì tra docs, không cần suy ra từ nguyên lý.
- Giả thuyết của người học là suy luận cho tới khi được kiểm chứng bằng lab hoặc tài liệu chính thức. Nhắc điều này khi chấm.
- Nếu câu trả lời của người học sai nhưng hợp lý, giải thích *vì sao trực giác đó sai* (thường là chi tiết của hệ thống phân tán), đừng chỉ đưa đáp án đúng.