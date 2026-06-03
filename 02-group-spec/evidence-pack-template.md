# Evidence Pack — Máy Dịch Khái Niệm

Nộp kèm thin SPEC cuối Day 05.

## 1. Nhóm và track

**Tên nhóm:** *5 ae siuuuuu nhơn*  
**Track:** Learning OS 

**Product/app đã chọn:** Máy Dịch Khái Niệm  
**Build slice đang nghĩ:** User nhập 1 khái niệm AI + 1 sở thích cá nhân → AI trả về analogy dạng narrative + bảng mapping. Có fallback card khi confidence < 60%.

---

## 2. Self-use evidence

Nhóm tự dùng app/workflow và ghi lại điểm gãy.

| Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
| Đọc định nghĩa "Embedding" trong tài liệu gốc — hiểu từng chữ nhưng không hình dung được ứng dụng thực tế | *(chưa có)* | Failure | Định nghĩa hàn lâm không đủ — cần cầu nối analogy gắn với thứ quen thuộc |
| Thử nhập sở thích "thể thao" quá chung → analogy sinh ra mơ hồ, không cá nhân hóa được | *(chưa có)* | Low-confidence | AI cần hỏi lại môn thể thao cụ thể trước khi generate |
| Nhập khái niệm đúng, sở thích cụ thể (ví dụ: bóng đá) → analogy ra rõ ràng, có narrative mở đầu/diễn biến | *(chưa có)* | Happy | Khi input đủ rõ, AI sinh kết quả tốt và dễ kiểm tra |
| AI sinh analogy nghe hay nhưng bỏ sót chiều vector space quan trọng của Embedding | *(chưa có)* | Correction | Cần hiển thị lại danh sách thành phần AI đã map để user tự kiểm tra bỏ sót |

---

## 3. User / review / social evidence

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| "Đọc xong vẫn không hiểu Embedding là gì, cứ thấy toàn chữ vector" | *(giả định — sẽ kiểm qua phỏng vấn)* | Học viên mới học AI | Ngôn ngữ kỹ thuật thiếu kết nối thực tế |
| "Phải đọc cùng một định nghĩa 3–4 lần mới nhớ, mà nhớ xong vẫn không dùng được" | *(giả định — sẽ kiểm qua phỏng vấn)* | Học viên khoá AI cơ bản | Thiếu cơ chế giúp não "neo" khái niệm |
| "Muốn hiểu nhanh hơn qua ví dụ thực tế, không phải định nghĩa dài" | *(giả định — sẽ kiểm qua phỏng vấn)* | Người tự học online | Não học qua analogy nhanh hơn định nghĩa |


---

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| ChatGPT (prompt "giải thích như tôi 5 tuổi") | User tự viết prompt yêu cầu giải thích đơn giản, AI trả free-form | Analogy hoạt động tốt nhưng cần user biết cách prompt | Có — nhưng cần cấu trúc hóa thêm phần sở thích cá nhân |
| Explainlikeimfive.io | Giải thích cố định theo style đơn giản, không cá nhân hóa | Cá nhân hóa theo sở thích là điểm khác biệt rõ | Có — đây là gap cần lấp |
| Analogies trong sách "AI Superpowers" | Dùng analogy văn hóa đại chúng Trung Quốc để giải thích AI | Analogy gắn bối cảnh quen thuộc giúp người đọc hiểu và nhớ lâu hơn | Có — áp dụng trực tiếp cho narrative structure |

---

## 5. Evidence → Insight

```text
Evidence nổi bật nhất:
Học viên đọc định nghĩa kỹ thuật xong vẫn cảm thấy khó hiểu vì ngôn ngữ
hàn lâm thiếu liên kết thực tế. Khi thử dùng analogy tự nghĩ, não tiếp thu
nhanh hơn rõ rệt — nhưng không phải ai cũng tự nghĩ được analogy phù hợp.

Insight:
User không chỉ gặp vấn đề "định nghĩa khó đọc".
Thật ra họ cần một cầu nối giữa khái niệm kỹ thuật và thứ họ đã biết,
được cá nhân hóa theo đúng sở thích của họ — không phải ví dụ generic.

Opportunity:
AI có thể giúp bằng cách augment bước "tạo analogy cá nhân hóa":
nhận khái niệm + sở thích → sinh narrative + bảng mapping rõ ràng,
trong khi vẫn để user tự kiểm tra độ chính xác kỹ thuật.
```

---

## 6. Evidence đổi SPEC như thế nào?

- [x] Đổi pain statement.
- [x] Đổi build slice.
- [x] Đổi failure mode.
- [ ] Đổi user chính.
- [ ] Đổi Auto/Aug decision.
- [ ] Đổi 4 paths.
- [ ] Đổi owner/test plan.

```text
Trước evidence, nhóm định build một tool giải thích AI concept theo style
"dễ hiểu" cố định (giống Explain Like I'm 5).

Sau evidence, nhóm đổi thành build slice tập trung vào cá nhân hóa theo sở thích:
user nhập sở thích → AI map từng thành phần kỹ thuật sang thứ quen thuộc của user.

Lý do: Evidence cho thấy analogy generic không hiệu quả bằng analogy gắn
với thứ user thực sự biết và yêu thích. Cá nhân hóa là điểm tạo ra
giá trị khác biệt thực sự.
```