---
artifact: 2 - Lớp chỉ dẫn AI
bai-tap: 2 - Thiết kế giải pháp
demo: ./demo.md
---

# card.md - Lớp chỉ dẫn AI

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Thêm bộ chỉ dẫn hệ thống cho chatbot tuyển sinh để AI không được bịa deadline, học phí, học bổng hoặc điều kiện xét tuyển khi thiếu nguồn chính thức. Khi người dùng hỏi thông tin rủi ro cao, AI phải kiểm tra nguồn, hỏi lại nếu thiếu bối cảnh, nói rõ khi chưa xác minh được, và chuyển sang tư vấn viên nếu người dùng cần quyết định gấp.

Lớp prompt này không thay thế kiến trúc dữ liệu/RAG, nhưng giúp giảm lỗi AI đoán bừa hoặc chiều theo người dùng trong lúc hệ thống chưa có đủ nguồn.

---

## 2. Vì sao sửa ở lớp chỉ dẫn AI?

- AI có thể trả lời quá tự tin khi thiếu nguồn, đặc biệt với câu hỏi về ngày, số tiền, điều kiện học bổng hoặc chính sách tuyển sinh.
- AI có thể chiều theo giả định sai của người dùng, ví dụ "em nghe hạn là 30/8, đúng không?".
- AI cần luật rõ: khi nào trả lời, khi nào hỏi lại, khi nào từ chối, khi nào chuyển sang người thật.
- Đây là lớp sửa nhanh, có thể kiểm thử ngay bằng bộ tình huống T-01 đến T-15.

**Hành động phòng vệ chính**:

- [x] Ngăn câu trả lời sai ngay từ đầu
- [x] Bắt buộc nêu nguồn khi nói về thông tin quan trọng
- [x] Từ chối trả lời khi thiếu căn cứ
- [x] Chuyển người thật khi vượt phạm vi hoặc cần quyết định gấp

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo có:

- Luật chính cho AI.
- Mẫu câu khi thiếu nguồn.
- Mẫu câu khi cần chuyển sang người thật.
- Ví dụ hỏi đáp kiểm tra rule.
- Kết quả thử lại với các tình huống từ Bài 1.

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

- AI có thể từ chối quá nhiều nếu hiểu mọi câu hỏi tuyển sinh đều là rủi ro cao.
- Câu trả lời có thể cứng và ít thân thiện.
- Người dùng có thể thấy chatbot kém hữu ích nếu không nhận được ngày / số tiền cụ thể.
- Nếu chỉ sửa bằng prompt mà dữ liệu vẫn thiếu, AI vẫn không thể trả lời thông tin chính xác.

**Nhóm giảm vấn đề đó bằng cách nào?**

- Chỉ bắt buộc nguồn với thông tin có hậu quả cao: deadline, học phí, học bổng, điều kiện xét tuyển, ngoại lệ chính sách.
- Tách từ chối mềm và từ chối cứng:
  - Từ chối mềm: "Mình chưa có nguồn chính thức nên chưa thể xác nhận."
  - Từ chối cứng: câu hỏi y tế, vay tiền nóng, gian dối hồ sơ.
- Luôn đưa hành động tiếp theo: xem trang chính thức, gọi hotline, gửi yêu cầu tư vấn.
- Phối hợp với lớp kiến trúc dữ liệu để AI có nguồn đúng thay vì chỉ từ chối.

---

## 5. Checklist trước khi nộp

- [x] Luật viết đủ cụ thể để AI làm theo.
- [x] Có mẫu câu khi AI không có đủ thông tin.
- [x] Có ví dụ cho tình huống dễ sai.
- [x] Có thử lại bằng tình huống trong Bài 1.
- [x] Không dùng prompt như cách duy nhất nếu lỗi nằm ở dữ liệu hoặc quy trình.

**Người phụ trách**: Bùi Trọng Anh - 2A202600010
