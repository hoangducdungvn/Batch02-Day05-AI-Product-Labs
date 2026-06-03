# 1. CHỌN SẢN PHẨM: AI CHATBOT VIETNAM AIRLINES - NEO

## 2. Dùng thử: Promise vs Reality

* **Product hứa gì?** Hỗ trợ hành khách tra cứu, giải đáp thông tin và thao tác các dịch vụ hàng không nhanh chóng, tiện lợi thông qua giao diện trò chuyện.
* **User nào được hứa sẽ được giúp?** Hành khách của Vietnam Airlines (bao gồm cả khách hàng đang tìm kiếm vé và khách hàng đã có mã đặt chỗ).
* **Bạn kỳ vọng AI làm được task nào?** Có thể tìm kiếm chuyến bay, giữ chỗ theo ngữ cảnh hội thoại và hỗ trợ chuyển tiếp trực tiếp sang bước thanh toán mà không làm mất thông tin đã trao đổi.
* **Khi dùng thật, điểm gãy xuất hiện ở đâu?** Gãy ở bước chuyển giao (handoff) từ việc "chốt chuyến bay" trên chat sang hành động "đặt vé". Hệ thống ghi nhận lựa chọn nhưng không lưu trữ ngữ cảnh để đẩy vào flow booking, bắt user làm lại từ số không.

### Bằng chứng (Evidence)
* **Screenshot:** `File neo.png` — Bot yêu cầu *"Truy cập website... Nhập thông tin điểm đi, điểm đến và ngày bay mong muốn"*.
* **Prompt/input đã thử:** `"chốt option 2"`
* **Hành vi quan sát được:** AI phản hồi đã ghi nhận thông tin chuyến bay VN267 rất chi tiết (giá vé, ngày giờ, số khách), nhưng ngay sau đó lại đưa ra hướng dẫn tĩnh dạng text yêu cầu khách hàng tự lên website làm lại bước tìm kiếm ban đầu.

---

## 3. Vẽ 4 paths

| Path | Câu hỏi cần trả lời | Trả lời thực tế trên App |
| :--- | :--- | :--- |
| **Happy** | Khi AI đúng và tự tin, user thấy gì? | User nhận được câu trả lời trực tiếp hoặc được điều hướng đúng link (chủ yếu hoạt động tốt ở các luồng hỏi đáp FAQ tĩnh hoặc tra cứu mã PNR đã có sẵn). |
| **Low-confidence** | Khi AI không chắc, hệ thống có hỏi lại, show options hoặc chuyển người không? | **Thiếu vắng.** Thay vì hỏi lại để làm rõ intent, hệ thống thường fallback về câu lệnh mặc định yêu cầu nhập Mã đặt chỗ, tạo cảm giác như một chatbot rule-based cũ. |
| **Failure** | Khi AI sai, user biết bằng cách nào và sửa thế nào? | User nhận ra lỗi khi AI đưa ra action vô lý (bắt nhập lại thông tin điểm đi/đến dù vừa chốt vé). User không có cách nào sửa trực tiếp trong chat ngoài việc... thoát chat và tự lên web làm tay. |
| **Correction** | Khi user sửa, correction có được lưu/log/học lại không hay biến mất? | Không có cơ chế UI/UX để user báo lỗi (như nút Thumbs down hoặc "Thông tin không đúng"). Việc user bỏ dở session (drop-off) có thể được log lại ở backend, nhưng không có feedback loop trực tiếp cho user. |

---

## 4. Viết finding thành quyết định

> **Ngữ cảnh (When):** Khi user đã chọn được chuyến bay cụ thể qua chat (VD: chốt option 2),  
> **Vấn đề hiện tại (But):** AI/product phản hồi bằng văn bản hướng dẫn tĩnh, yêu cầu user tự truy cập web và nhập lại từ đầu điểm đi/điểm đến/ngày bay,  
> **Hậu quả (Impact):** Hậu quả là đứt gãy hoàn toàn trải nghiệm hội thoại, lãng phí công sức tra cứu của user và tỷ lệ thoát (drop-off) ở bước này gần như tuyệt đối.  
> **Phân loại lỗi:** Lỗi thuộc layer **UX Recovery & Data-tool** (thiếu API handoff / đánh rơi Context).

### **Quyết định sửa đổi (Requirement):**
Hệ thống sinh ra **Deep Link/Payload** chứa sẵn các tham số *(Mã chuyến bay, ngày bay, số lượng khách)* đính kèm vào một nút Call-to-action, đẩy thẳng user sang trang điền thông tin hành khách của VNA.

---

## 5. Sketch As-is / To-be

| As-is (Flow hiện tại) | To-be (Flow đề xuất) |
| :--- | :--- |
| **[User]** Tra cứu chuyến bay đi SG ngày mai cho 5 người.<br>**[AI]** Trả về list chuyến bay hợp lệ.<br>**[User]** Gõ: *"Chốt option 2"*.<br>**[AI]** Báo đã ghi nhận chuyến VN267, giá 11.060.000đ.<br>🚨 **(ĐIỂM GÃY) [AI] In ra text:** *"Vui lòng vào web nhập lại điểm đi, điểm đến, ngày bay..."*<br>**[User]** Phải tự mở web, gõ lại từ đầu ➔ Ức chế, thoát luồng. | **[User]** Tra cứu chuyến bay đi SG ngày mai cho 5 người.<br>**[AI]** Trả về list chuyến bay hợp lệ.<br>**[User]** Gõ: *"Chốt option 2"*.<br>**[AI]** *"NEO đã ghi nhận chuyến VN267. Để giữ mức giá 11.060k cho 5 khách, vui lòng điền thông tin người bay tại đây."*<br>✅ **(PATH ĐÃ SỬA) [Product]:** Hiển thị UI Button: **`[Điền thông tin & Thanh toán]`** *(Nút chứa Deep Link truyền sẵn thông số vé)*.<br>**[User]** Click nút ➔ Mở trang Checkout của VNA với giỏ hàng đã có sẵn vé VN267 ➔ Nhập tên ➔ Thanh toán. |

---

## 6. Tự kiểm trước khi nộp

- [x] Có ít nhất 1 screenshot hoặc observation cụ thể.
- [x] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product.
- [x] Finding được viết thành product decision, không chỉ là nhận xét.
- [x] Sketch có as-is và to-be.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.

### **Câu nói rõ thay đổi trong SPEC:**
> *"Cập nhật SPEC module Integration: AI Agent phải gọi hàm sinh URL động (mang payload thông tin vé đã chốt) thay vì trả về text hướng dẫn, đồng thời Front-end chat UI cần bổ sung component hiển thị nút bấm Action (Call-to-action button) để chuyển giao luồng đặt vé."*