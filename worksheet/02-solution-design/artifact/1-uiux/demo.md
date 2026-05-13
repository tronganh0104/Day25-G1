---
artifact: 1 - Demo giao diện
format: phác thảo Markdown + HTML tĩnh
---

# demo.md - Demo giao diện

Demo này minh họa lớp giao diện cho rủi ro T-01: AI bịa deadline học bổng 2026 khi chưa có nguồn chính thức.

Bản giao diện tĩnh có thể mở ở: [`demo.html`](./demo.html)

---

## 1. Màn hình chính

```text
┌────────────────────────────────────────────────────────────────────────────┐
│ Tuyển sinh 2026                                      Hotline: 1900 0000    │
├────────────────────────────────────────────────────────────────────────────┤
│ Chatbot tư vấn tuyển sinh                                                  │
│                                                                            │
│ User                                                                       │
│ "Hạn chót nộp hồ sơ xét học bổng toàn phần ngành Kinh tế năm 2026          │
│  là ngày mấy?"                                                             │
│                                                                            │
│ AI                                                                         │
│ ┌──────────────────────────────────────────────────────────────────────┐   │
│ │ Trạng thái: CHƯA CÓ NGUỒN CHÍNH THỨC                                  │   │
│ │                                                                      │   │
│ │ Mình chưa tìm thấy thông báo chính thức về hạn nộp hồ sơ học bổng     │   │
│ │ toàn phần ngành Kinh tế cho năm 2026. Vì đây là thông tin có thể       │   │
│ │ ảnh hưởng đến việc nộp hồ sơ, mình không nên đoán ngày.                │   │
│ │                                                                      │   │
│ │ Bạn có thể kiểm tra trang học bổng hoặc chuyển cho tư vấn viên.        │   │
│ │                                                                      │   │
│ │ [Xem trang học bổng] [Chuyển tư vấn viên] [Báo câu trả lời thiếu nguồn]│   │
│ └──────────────────────────────────────────────────────────────────────┘   │
│                                                                            │
│ Nguồn hiện có:                                                             │
│ - Trang học bổng: chưa có thông báo 2026                                   │
│ - Trang tuyển sinh: chưa có deadline học bổng 2026                         │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Trạng thái cần minh họa

| Trạng thái | Người dùng thấy gì? | Người dùng làm gì tiếp? |
|---|---|---|
| Có nguồn xác minh | Nhãn xanh "Đã xác minh từ nguồn chính thức", ngày deadline, link nguồn và thời điểm cập nhật | Mở nguồn chính thức hoặc lưu lại thông tin |
| Chưa có nguồn xác minh | Nhãn vàng "Chưa có nguồn chính thức", AI không đưa ngày cụ thể, giải thích ngắn vì sao không đoán | Xem trang học bổng, theo dõi cập nhật, hoặc chuyển tư vấn viên |
| AI không nên tự trả lời | Nhãn đỏ "Cần tư vấn viên kiểm tra", không có kết luận thay trường | Bấm "Chuyển tư vấn viên" hoặc gọi hotline |
| Cần chuyển sang người thật | Form nhỏ hỏi tên, email/số điện thoại, ngành quan tâm và nội dung cần tư vấn | Gửi yêu cầu cho tư vấn viên |

---

## 3. Luồng tương tác

```text
Người dùng hỏi deadline / học bổng
        ↓
Giao diện hiển thị trạng thái kiểm tra nguồn
        ↓
Nếu có nguồn chính thức
        → Hiển thị câu trả lời + link nguồn + ngày cập nhật
        ↓
Nếu chưa có nguồn chính thức
        → Không hiển thị ngày đoán
        → Hiển thị cảnh báo "Chưa có nguồn chính thức"
        → Gợi ý xem trang học bổng / chuyển tư vấn viên
        ↓
Nếu người dùng cần quyết định gấp
        → Ưu tiên nút "Chuyển tư vấn viên" và hotline
```

---

## 4. Ghi chú cho từng thành phần

- **Nhãn trạng thái nguồn**: nằm trên đầu câu trả lời AI. Có 3 trạng thái: `Đã xác minh`, `Chưa có nguồn`, `Cần tư vấn viên`.
- **Vùng câu trả lời AI**: không được đưa deadline cụ thể nếu trạng thái là `Chưa có nguồn`.
- **Nguồn tham khảo**: hiển thị link trang học bổng / tuyển sinh chính thức; nếu chưa có nguồn 2026 thì ghi rõ "chưa có thông báo 2026".
- **Nút chuyển tư vấn viên**: xuất hiện nổi bật khi câu hỏi liên quan đến deadline, học bổng, học phí hoặc quyết định gấp.
- **Nút báo thiếu nguồn**: cho phép người dùng báo lại nếu câu trả lời không có nguồn hoặc nguồn đã cũ.

---

## 5. Microcopy dùng trong giao diện

| Tình huống | Câu chữ hiển thị |
|---|---|
| Có nguồn | "Đã xác minh từ nguồn chính thức. Cập nhật lần cuối: [ngày]." |
| Thiếu nguồn | "Chưa có nguồn chính thức cho thông tin này. Chatbot sẽ không đoán ngày hoặc mức học bổng." |
| Cần người thật | "Thông tin này có thể ảnh hưởng đến hồ sơ của bạn. Hãy chuyển cho tư vấn viên kiểm tra." |
| Người dùng đang vội | "Nếu bạn cần quyết định hôm nay, vui lòng gọi hotline hoặc gửi yêu cầu tư vấn ngay." |

---

## 6. Kiểm tra nhanh

- [x] Nhìn vào demo là hiểu rủi ro đang được chặn ở đâu.
- [x] Có trạng thái khi AI không có đủ thông tin.
- [x] Có cách chuyển sang người thật.
- [x] Câu chữ đủ ngắn để đặt trên màn hình thật.
- [x] Không trình bày thông tin chưa xác minh như thông báo chính thức.
