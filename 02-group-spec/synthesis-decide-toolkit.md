# Toolkit — Từ Evidence Đến Build Slice: Máy Dịch Khái Niệm

---

## 1. Gom evidence thành cụm

*(Gom theo workflow/pain)*

- **"Đọc định nghĩa xong vẫn không hiểu"** — Ngôn ngữ hàn lâm, thiếu kết nối với thứ quen thuộc. Học viên phải đọc đi đọc lại nhiều lần mà vẫn không "neo" được khái niệm vào não.

- **"Không biết dùng analogy nào cho mình"** — User biết analogy giúp ích nhưng không tự nghĩ được ví dụ phù hợp với sở thích cá nhân.

- **"Analogy có sẵn quá generic, không relate được"** — Các tool hiện có (ChatGPT prompt đơn giản, ELI5) đưa ra ví dụ cố định, không cá nhân hóa.

- **"AI sinh analogy nghe hay nhưng bỏ sót thành phần quan trọng"** — Hallucination dạng thiếu — analogy đúng một phần nhưng map không đủ các thành phần kỹ thuật.

- **"Nhập sở thích quá chung → kết quả mơ hồ"** — Khi user nhập "thể thao" thay vì "bóng đá", AI không đủ ngữ cảnh để cá nhân hóa.

---

## 2. Viết insight

```text
Học viên AI không chỉ cần định nghĩa viết đơn giản hơn.
Họ thật ra cần một cầu nối được cá nhân hóa — map đúng
thành phần kỹ thuật sang thứ họ đã biết và yêu thích —
vì não người học qua analogy quen thuộc nhanh và nhớ lâu hơn
so với định nghĩa trừu tượng, dù định nghĩa có được diễn đạt
đơn giản đến đâu.
```

---

## 3. Viết opportunity

```text
Cơ hội là dùng AI để augment bước "tạo analogy cá nhân hóa":
tiếp nhận khái niệm kỹ thuật + sở thích cụ thể của user,
map từng thành phần sang ngữ cảnh quen thuộc, sinh narrative rõ + bảng mapping,
giúp user hiểu khái niệm nhanh hơn trong lần đọc đầu tiên,
trong khi vẫn để user tự kiểm tra độ chính xác kỹ thuật
(analogy là cầu nối, không thay thế tài liệu gốc).
```

---

## 4. Chọn build slice

| Câu hỏi | Đánh giá |
|---|---|
| User cụ thể chưa? | ✅ Học viên đang học AI concept lần đầu, có sở thích cá nhân cụ thể (bóng đá, nấu ăn, âm nhạc...) |
| Task đủ hẹp chưa? | ✅ Nhập 1 khái niệm + 1 sở thích → xem analogy narrative + bảng mapping. Demo được trong 3–5 phút. |
| AI decision rõ chưa? | ✅ AI map từng thành phần kỹ thuật sang thứ quen thuộc, sinh narrative có cấu trúc, kiểm tra confidence trước khi generate. |
| Failure path rõ chưa? | ✅ Confidence < 60% → hiện fallback card với lý do + 3 gợi ý sửa prompt. Không để output tệ trôi qua. |
| Có evidence không? | ✅ Self-use evidence + pain statement từ quan sát lớp học. Cần bổ sung interview người dùng trước M1. |

**Build slice được chọn:**
> User nhập 1 khái niệm AI + 1 sở thích cá nhân → AI kiểm tra confidence input → nếu đủ rõ: sinh analogy narrative + bảng mapping → user review. Nếu sở thích quá chung: AI hỏi lại. Nếu confidence < 60%: hiện fallback card.

---

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

| Tình huống | Quyết định |
|---|---|
| Ý tưởng ban đầu rộng (dạy toàn bộ khái niệm AI) | ✅ Giữ domain, cắt xuống một flow: analogy 1 khái niệm + 1 sở thích |
| AI sinh analogy sai/thiếu | ✅ Augmentation — user tự kiểm tra bảng mapping, không để AI tự quyết |
| Quiz/lưu lịch sử/personalization dài hạn | ✅ Đưa vào backlog, không build trong Day 06 |
| Rủi ro hallucination | ✅ Hiện bảng mapping để user kiểm tra + fallback card khi confidence thấp |

---

## 6. Câu chốt cuối

```text
Dựa trên self-use evidence (analogy cá nhân hóa giúp hiểu nhanh hơn)
và pain observation (ngôn ngữ hàn lâm thiếu kết nối thực tế),

nhóm sẽ build prototype "Máy Dịch Khái Niệm" — flow nhập khái niệm + sở thích,
AI sinh analogy narrative + bảng mapping,

cho học viên đang học AI concept lần đầu,

để giải quyết pain "đọc định nghĩa xong vẫn không hình dung được",

bằng cách AI augment bước tạo analogy cá nhân hóa
(map thành phần kỹ thuật sang ngữ cảnh quen thuộc của user),

và sẽ test failure path: confidence < 60% → fallback card
(lý do cụ thể + 3 gợi ý sửa prompt, không để output tệ tự chạy).
```

---

## 7. Backlog

Những thứ **không build trong Day 06**:

- Hệ thống quiz kiểm tra user có hiểu đúng không
- Lưu analogy yêu thích / lịch sử các lần dùng
- Gợi ý khái niệm tiếp theo sau khi hiểu xong
- AI gợi ý sở thích phổ biến khi user không biết nhập gì (Bậc 2)
- Personalized learning path nhớ sở thích qua nhiều lần dùng (Bậc 3)
- Tài khoản người dùng