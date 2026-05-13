---
artifact: 3 - Lớp kiến trúc dữ liệu
bai-tap: 2 - Thiết kế giải pháp
demo: ./demo.md
---

# card.md - Lớp kiến trúc dữ liệu

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Thiết kế pipeline tra cứu nguồn chính thức trước khi AI trả lời các câu hỏi rủi ro cao về deadline, học bổng, học phí và điều kiện xét tuyển. Với câu hỏi học bổng 2026, hệ thống phải tìm trong nguồn chính thức, kiểm tra đúng năm tuyển sinh và độ mới của nguồn; nếu không có dữ liệu verified, AI không được đoán mà phải trả lời theo mẫu thiếu nguồn và chuyển sang tư vấn viên.

Hệ thống cũng ghi log các câu hỏi thiếu nguồn, nguồn lỗi hoặc người dùng báo sai để đội tuyển sinh cập nhật dữ liệu.

---

## 2. Vì sao sửa ở lớp kiến trúc dữ liệu?

- Nguyên nhân chính là thiếu nguồn đúng hoặc nguồn cũ.
- AI đang phải tự nhớ hoặc suy luận thông tin thay vì đọc từ nguồn đáng tin cậy.
- Cần kiểm tra dữ liệu trước khi câu trả lời được tạo ra, đặc biệt với deadline/học bổng.
- Cần ghi lại lỗi để nhóm biết câu hỏi nào bị thiếu nguồn lặp lại nhiều lần.

**Hành động phòng vệ chính**:

- [x] Ngăn lỗi bằng nguồn dữ liệu đúng
- [x] Phát hiện khi nguồn thiếu, lỗi hoặc quá cũ
- [x] Khắc phục bằng cách chuyển sang người thật
- [x] Ghi lại lỗi để cải thiện sau

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo có:

- Sơ đồ cách dữ liệu đi qua hệ thống.
- Nguồn dữ liệu chính thức.
- Bước kiểm tra trước khi AI trả lời.
- Cách xử lý khi nguồn thiếu, lỗi hoặc quá cũ.
- Cách ghi lại hoặc theo dõi lỗi.

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

- Trả lời chậm hơn vì cần tra cứu và kiểm tra nguồn.
- Phụ thuộc vào chất lượng và độ cập nhật của nguồn tuyển sinh.
- Tốn công duy trì danh sách nguồn chính thức và metadata như năm tuyển sinh, ngày cập nhật, trạng thái verified.
- Hệ thống phức tạp hơn so với chatbot chỉ gọi LLM trực tiếp.

**Nhóm giảm vấn đề đó bằng cách nào?**

- Lưu tạm các nguồn phổ biến như học phí, học bổng, đề án tuyển sinh và FAQ.
- Chỉ bật kiểm tra nguồn nghiêm ngặt với câu hỏi rủi ro cao.
- Đặt người phụ trách cập nhật nguồn trước mùa tuyển sinh.
- Hiển thị thông báo rõ khi nguồn lỗi hoặc chưa có dữ liệu, thay vì để AI đoán.
- Dùng log thiếu nguồn để ưu tiên cập nhật các trang được hỏi nhiều nhất.

---

## 5. Checklist trước khi nộp

- [x] Sơ đồ cho thấy dữ liệu đi từ đâu đến đâu.
- [x] Có bước kiểm tra nguồn trước khi AI trả lời.
- [x] Có cách xử lý khi không có dữ liệu.
- [x] Có cách chuyển sang người thật với tình huống rủi ro cao.
- [x] Có cách biết lỗi này có đang lặp lại không.

**Người phụ trách**: Nguyễn Tiến Thành - 2A202600487
