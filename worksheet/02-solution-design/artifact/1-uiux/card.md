---
artifact: 1 - Lớp giao diện
bai-tap: 2 - Thiết kế giải pháp
demo: ./demo.md và ./demo.html
---

# card.md - Lớp giao diện

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Thiết kế lại giao diện chatbot tuyển sinh để câu trả lời về deadline / học bổng luôn có trạng thái xác minh rõ ràng. Với thông tin có nguồn, giao diện hiển thị nhãn "Đã xác minh từ nguồn chính thức" kèm link nguồn. Với thông tin chưa có nguồn, giao diện không cho AI đưa ngày cụ thể, mà hiển thị cảnh báo "Chưa có nguồn chính thức" và nút chuyển sang tư vấn viên.

Mục tiêu là ngăn người dùng hiểu nhầm câu trả lời của AI là thông báo chính thức của trường khi dữ liệu chưa được xác minh.

---

## 2. Vì sao sửa ở lớp giao diện?

- Người dùng dễ tin câu trả lời của AI quá mức vì chatbot nằm trên website tuyển sinh chính thức của trường.
- Rủi ro xảy ra ngay tại khoảnh khắc người dùng đọc câu trả lời và quyết định nộp hồ sơ / nộp tiền / chờ deadline.
- Giao diện cần làm rõ thông tin nào đã kiểm tra, thông tin nào chưa chắc, và khi nào phải hỏi người thật.
- Nếu prompt hoặc dữ liệu vẫn sót lỗi, giao diện là lớp giảm hại cuối cùng trước khi người dùng hành động.

**Hành động phòng vệ chính**:

- [x] Thông báo rõ giới hạn
- [x] Phát hiện dấu hiệu thiếu nguồn
- [x] Chuyển người thật khi cần
- [x] Giúp người dùng kiểm tra lại nguồn

---

## 3. Demo nằm ở đâu?

**File demo**:

- [`demo.md`](./demo.md): mô tả màn hình, trạng thái và thành phần UI.
- [`demo.html`](./demo.html): bản giao diện tĩnh có thể mở trực tiếp trong trình duyệt.

**Định dạng demo**:

- [x] Phác thảo màn hình
- [x] Luồng màn hình
- [x] Bản HTML đơn giản
- [ ] Ảnh hoặc link prototype

**Thành phần cần có trong demo**:

- Trạng thái có nguồn xác minh.
- Trạng thái chưa có nguồn xác minh.
- Cách người dùng chuyển sang người thật.
- Câu chữ cảnh báo ngắn, dễ hiểu.
- Link nguồn chính thức hoặc trang cần kiểm tra.

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

- Màn hình có thêm nhãn, cảnh báo và nút hành động nên có thể nhìn rối hơn.
- Người dùng có thể thấy chatbot "ít hữu ích" hơn khi AI không đưa ngay deadline cụ thể.
- Việc kiểm tra nguồn có thể làm phản hồi chậm hơn.
- Nếu cảnh báo xuất hiện quá nhiều, người dùng có thể bỏ qua cảnh báo.

**Nhóm giảm vấn đề đó bằng cách nào?**

- Chỉ hiển thị cảnh báo mạnh với thông tin rủi ro cao như deadline, học phí, học bổng, điều kiện xét tuyển.
- Dùng nhãn ngắn: "Đã xác minh", "Chưa có nguồn", "Cần tư vấn viên".
- Đưa chi tiết nguồn vào vùng mở rộng, không nhồi quá nhiều chữ trong bubble chat.
- Luôn có hành động tiếp theo rõ ràng: xem nguồn chính thức, gọi hotline, hoặc chuyển tư vấn viên.
- Cache nguồn chính thức phổ biến để giảm thời gian phản hồi.

---

## 5. Checklist trước khi nộp

- [x] Giải pháp gắn đúng với rủi ro chính T-01.
- [x] Demo nhìn vào là hiểu vấn đề được chặn ở đâu.
- [x] Có đủ trạng thái bình thường và trạng thái lỗi.
- [x] Có cách chuyển sang người thật khi AI không nên tự xử lý.
- [x] Câu chữ trong giao diện ngắn, không đổ hết trách nhiệm cho người dùng.

**Người phụ trách**: Nguyễn Thành Đại Khánh - 2A202600404
