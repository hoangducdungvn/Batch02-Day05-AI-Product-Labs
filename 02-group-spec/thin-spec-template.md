# Thin SPEC Cuối Day 05 — Máy Dịch Khái Niệm

---

## 1. Track, product/app và user

**Track:** Learning OS  
**Product/app thật:** Máy Dịch Khái Niệm  
**User cụ thể:** Học viên đang học khóa AI thực chiến, có ít nhất một sở thích cá nhân cụ thể (thể thao, âm nhạc, nấu ăn...), cảm thấy định nghĩa kỹ thuật khó hình dung dù đã đọc nhiều lần.  
**Nhóm có phải user thật không?** Có  — thành viên trong nhóm cũng là học viên AI beginner.

---

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Học viên đọc định nghĩa AI xong vẫn cảm thấy khó hiểu vì ngôn ngữ hàn lâm, thiếu liên kết thực tế | Quan sát lớp học + self-use | Định nghĩa đơn giản chưa đủ — cần analogy gắn với thứ user đã biết | Pain statement tập trung vào "thiếu kết nối cá nhân hóa", không chỉ "thiếu đơn giản" |
| Não học qua analogy nhanh hơn định nghĩa (pattern học được từ tài liệu tham khảo) | Ghi chú lớp + analogy trong sách AI | Đây là cơ chế học tự nhiên của não, không phải preference — nên thiết kế theo | Build slice phải tạo ra analogy có narrative rõ, không chỉ viết lại định nghĩa |
| Nhập sở thích "thể thao" → analogy mơ hồ; nhập "bóng đá" → analogy rõ và relate được | Self-use | Chất lượng output phụ thuộc hoàn toàn vào độ cụ thể của input | Cần bước kiểm tra và hỏi lại trước khi generate |
| AI có thể sinh analogy nghe hay nhưng bỏ sót thành phần kỹ thuật quan trọng | Self-use (test Embedding) | Hallucination dạng "thiếu" nguy hiểm hơn hallucination dạng "sai rõ" | Cần bảng mapping để user tự kiểm tra — không chỉ đọc narrative |

---

## 3. Pain statement

```text
Học viên lần đầu học AI đang gặp khó ở bước hiểu và nhớ khái niệm kỹ thuật,
vì định nghĩa hàn lâm thiếu kết nối với thứ quen thuộc trong cuộc sống của họ,
dẫn tới phải đọc đi đọc lại nhiều lần mà vẫn không "dùng được" khái niệm đó.

Bằng chứng chính là: học viên đọc xong định nghĩa Embedding vẫn không hình dung
được ứng dụng thực tế; khi dùng analogy cá nhân hóa (gắn bóng đá, nấu ăn...)
thì hiểu và nhớ ngay trong lần đọc đầu tiên.
```

---

## 4. Build slice

```text
Cho học viên khóa AI thực chiến đang cần hiểu một khái niệm kỹ thuật mới,
prototype sẽ dùng AI để augment bước tạo analogy cá nhân hóa:
tiếp nhận tên khái niệm + sở thích cụ thể → map từng thành phần kỹ thuật
sang ngữ cảnh quen thuộc → sinh narrative có mở đầu/diễn biến rõ + bảng mapping cuối.

Tạo ra output gồm: (1) analogy narrative, (2) bảng mapping [Thành phần kỹ thuật] = [Thứ trong analogy].

Xử lý failure mode "sở thích quá chung chung" bằng bước hỏi lại trước khi generate.
Xử lý failure mode "confidence thấp" bằng fallback card: lý do + 3 gợi ý sửa prompt,
không để AI tự chạy ra output tệ.
```

---

## 5. Auto/Aug decision

- [x] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.
- [ ] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
- [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:** Analogy về khái niệm kỹ thuật có thể bỏ sót thành phần quan trọng mà user không nhận ra ngay. Cần user tự kiểm tra bảng mapping trước khi "tin" vào analogy. AI là công cụ tạo cầu nối, user là người chịu trách nhiệm học và kiểm chứng.

**Human role:** reviewer — đọc analogy, kiểm tra bảng mapping, tự đánh giá có hiểu hơn không, quyết định dùng lại hay sửa input.

---

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| Happy | User nhập khái niệm rõ (VD: "Embedding") + sở thích cụ thể (VD: "bóng đá") → AI sinh analogy narrative đầy đủ + bảng mapping rõ ràng → User đọc, hiểu, hài lòng. |
| Low-confidence | User nhập sở thích quá chung chung ("thể thao") → AI detect và hỏi lại "Bạn thích môn nào cụ thể?" → User bổ sung → AI sinh analogy tốt hơn. |
| Failure | AI không nhận ra khái niệm user nhập (sai tên hoặc khái niệm không tồn tại) → AI báo không nhận ra + gợi ý khái niệm gần nhất. Hoặc: confidence < 60% → hiện fallback card với lý do cụ thể + 3 gợi ý sửa prompt. |
| Correction | User đọc analogy, thấy bảng mapping bỏ sót thành phần quan trọng → User sửa lại input hoặc thêm yêu cầu → AI regenerate analogy có mapping đủ hơn. |

---

## 7. Failure mode nguy hiểm nhất

```text
Nếu user đọc analogy narrative nghe hay và không kiểm tra bảng mapping,
AI có thể đã bỏ sót thành phần kỹ thuật quan trọng (VD: chiều vector space
trong Embedding) mà không ai nhận ra,
hậu quả là user hiểu sai khái niệm mà nghĩ mình đã hiểu đúng —
đây là dạng hallucination nguy hiểm nhất vì "nghe hợp lý".

Prototype sẽ xử lý bằng: luôn hiển thị bảng mapping rõ ràng kèm analogy,
kèm ghi chú "Kiểm tra xem AI đã map đủ thành phần chưa trước khi dùng".
Fallback card khi confidence < 60%.

Owner kiểm thử path này là: [tên thành viên phụ trách test/failure path].
```

---

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| *Hoàng Đức Dũng* | Research / evidence — phỏng vấn nhanh 2–3 học viên, bổ sung user quotes | File interview notes hoặc screenshot |
| *Nguyễn Trần Kiên* | SPEC — hoàn thiện thin SPEC, cập nhật nếu có evidence mới từ interview | File thin-spec.md đã finalize |
| *Đoàn Công Phú* | Prototype — build flow chính: input → kiểm tra → sinh analogy → hiển thị narrative + bảng mapping | Link demo hoặc file code chạy được |
| *Đinh Văn Anh Khôi* | Test / failure path — test fallback card (confidence < 60%), test hỏi lại sở thích, test khái niệm không tồn tại | Ghi chép kết quả test + screenshot từng path |
| *Vũ Quang Vinh* | Demo script / repo — viết script 3–5 phút, chuẩn bị repo đủ README | File demo-script.md + repo link |