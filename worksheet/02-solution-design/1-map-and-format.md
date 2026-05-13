---
artifact: 1 - FINAL kế hoạch giải pháp
bai-tap: 2 - Thiết kế giải pháp
phase: Chọn rủi ro + chọn tầng + chọn demo + chốt 3 lớp giải pháp
time: 11:00-11:55
input: 00-context.md + 01-test-set-review/3-FINAL-test-set-eval-plan.md
nop-cuoi: Có - file cuối Bài 2
---

# 1 - FINAL: Kế hoạch giải pháp

File này ghi lại quyết định chính của Bài 2:

- Rủi ro nào được chọn.
- Vì sao rủi ro đó quan trọng.
- Nguyên nhân gốc là gì.
- Nhóm sẽ xây 3 lớp giải pháp nào.
- Mỗi lớp dùng demo gì.

Lý do cần 3 lớp: một giải pháp đơn lẻ dễ lọt lỗi. Với rủi ro nặng, nhóm cần nhiều lớp cùng đỡ: lớp này ngăn, lớp kia phát hiện, lớp khác khắc phục hoặc thông báo cho người dùng.

Ba lớp giải pháp nằm trong thư mục `artifact/`:

| Lớp | Thư mục | Vai trò |
|---|---|---|
| Giao diện | `artifact/1-uiux/` | Cảnh báo, dẫn nguồn, nút chuyển sang người thật |
| Chỉ dẫn AI | `artifact/2-prompt/` | Hỏi lại, từ chối, bắt buộc dẫn nguồn |
| Kiến trúc dữ liệu | `artifact/3-architecture/` | Tra cứu nguồn đúng, kiểm tra nguồn, xử lý khi thiếu nguồn, giám sát lỗi |

Ba lớp này bổ sung cho nhau. Nếu một lớp lọt lỗi, lớp khác vẫn có thể chặn hoặc giảm hại.

## Thông tin nhóm

- **Chủ đề**: Track 01 - Chatbot tư vấn tuyển sinh đại học
- **Thành viên**:
  - Nguyễn Thành Đại Khánh - 2A202600404
  - Bùi Trọng Anh - 2A202600010
  - Nguyễn Tiến Thành - 2A202600487
- **Ngày**: 2026-05-13

---

## Phần A - Chọn rủi ro và tầng giải pháp

### Rủi ro chính được chọn

- **ID tình huống**: T-01
- **Mô tả ngắn**: Khi học sinh hoặc phụ huynh hỏi deadline học bổng 2026 cụ thể, AI có xu hướng bịa hoặc suy đoán ngày nếu chưa có nguồn chính thức, gây nguy cơ lỡ hạn nộp hồ sơ, mất cơ hội học bổng và làm người dùng ra quyết định tài chính sai.
- **Mức độ**: Nặng
- **Điểm rủi ro**: 25
- **Vì sao chọn tình huống này**: Đây là rủi ro chính đã được xác định từ Day 24, có điểm rủi ro cao nhất, có hậu quả thực tế với học sinh và phụ huynh, đồng thời phù hợp để thiết kế đủ 3 lớp giải pháp: giao diện, chỉ dẫn AI và kiến trúc dữ liệu.

### Tìm nguyên nhân gốc

Đừng chỉ mô tả lỗi. Hãy trả lời: vì sao lỗi xảy ra?

- [x] Thiếu nguồn dữ liệu đúng.
- [x] AI đoán khi không biết.
- [x] Giao diện khiến người dùng tin quá mức.
- [x] Quy trình thiếu người duyệt hoặc thiếu bước chuyển sang người thật.
- [x] Không có theo dõi sau khi ra mắt.
- [ ] Khác: Không áp dụng.

### Bảng nối nguyên nhân với tầng sửa

| Nguyên nhân gốc | Tầng ưu tiên sửa | Lớp giải pháp liên quan |
|---|---|---|
| Nguồn tuyển sinh / học bổng 2026 chưa có hoặc chưa được cập nhật vào hệ thống | Dữ liệu / tra cứu nguồn chính thức / kiểm tra freshness | `3-architecture` là chính |
| AI cố trả lời bằng pattern từ năm cũ hoặc dữ liệu huấn luyện | Chỉ dẫn hệ thống / quy tắc không đoán / bắt buộc dẫn nguồn | `2-prompt` là chính |
| Chatbot nằm trên website chính thức nên người dùng tin câu trả lời như thông báo của trường | Giao diện cảnh báo mức xác minh, nhãn nguồn, nút chuyển tư vấn viên | `1-uiux` là chính |
| Người dùng hỏi trong trạng thái gấp, cần quyết định nộp tiền hoặc nộp hồ sơ ngay | Luồng chuyển người thật và hotline khi rủi ro cao | `1-uiux` + `2-prompt` + `3-architecture` |
| Lỗi có thể lặp lại nhưng đội tuyển sinh không biết | Log lỗi, nút báo sai, dashboard theo dõi câu hỏi thiếu nguồn | `3-architecture` là chính |

Nguyên tắc: lỗi nằm ở nhiều tầng nên không sửa bằng một cảnh báo giao diện đơn lẻ. Cần nguồn đúng để ngăn lỗi, prompt để buộc AI không đoán, UI để người dùng thấy mức tin cậy, và kiến trúc để chuyển sang người thật khi thiếu nguồn.

### 10 tầng giải pháp tham khảo

Không bắt buộc dùng đủ 10 tầng. Bảng này giúp nhóm chọn đúng hướng sửa.

| Tầng | Khi nào dùng |
|---|---|
| Giao diện | Người dùng tin AI quá mức, thiếu cảnh báo, thiếu nguồn, thiếu nút chuyển sang người thật |
| Chỉ dẫn AI | AI đoán khi không biết, không hỏi lại, không từ chối |
| Quy trình xử lý | Cần phân loại ý định, chuyển đúng nơi xử lý, có cách xử lý khi AI không nên trả lời |
| Dữ liệu / tra cứu nguồn (RAG) | Thiếu nguồn đúng, nguồn cũ, AI không dựa vào nguồn đáng tin cậy |
| Theo dõi | Lỗi lặp lại sau khi ra mắt nhưng không ai thấy |
| Chính sách / thông báo giới hạn | Người dùng không biết giới hạn của AI |
| Người duyệt / phê duyệt | Tình huống pháp lý, y tế, tài chính, tuyển dụng, hoặc tác động lớn |
| Vai trò trách nhiệm | Có cảnh báo nhưng không ai chịu trách nhiệm xử lý |
| Vòng phản hồi | Cần người dùng / người rà báo lỗi để cập nhật hệ thống |
| Kiến trúc lai | LLM một mình không đủ, cần rule, classifier, hoặc nhiều bước kiểm tra |

### 4 hành động phòng vệ

Mỗi lớp nên làm ít nhất một việc:

- **Ngăn**: giảm khả năng lỗi xảy ra từ đầu.
- **Phát hiện**: nhận ra lỗi hoặc tín hiệu nguy hiểm.
- **Khắc phục**: chuyển sang người thật, dùng câu trả lời dự phòng, hoặc dừng trả lời.
- **Thông báo**: giúp người dùng hiểu mức tin cậy và rủi ro.

Gợi ý theo mức rủi ro:

| Mức rủi ro | Nên có |
|---|---|
| Nhẹ | Ít nhất 1 hành động |
| Vừa | Ít nhất 2 hành động |
| Nặng | Ít nhất 3 hành động |
| Rất nặng / không đảo ngược được | Cố gắng đủ 4 hành động + có người chịu trách nhiệm |

### Kết luận Phần A

**Nguyên nhân gốc**: Chatbot có thể trả lời deadline học bổng bằng suy đoán vì thiếu nguồn tuyển sinh chính thức mới nhất, thiếu quy tắc bắt buộc không đoán, thiếu giao diện thể hiện trạng thái xác minh, và thiếu luồng chuyển người thật khi thông tin chưa có nguồn.

**Tầng chính cần sửa**: Dữ liệu / tra cứu nguồn chính thức là tầng chính; chỉ dẫn AI và giao diện là hai tầng hỗ trợ bắt buộc.

**Vì sao cần 3 lớp giải pháp**:

- Lớp giao diện: giúp người dùng thấy câu trả lời đã xác minh hay chưa, thấy nguồn, và có nút chuyển tư vấn viên khi thiếu nguồn.
- Lớp chỉ dẫn AI: buộc AI không bịa deadline, không suy từ năm cũ, phải hỏi lại hoặc từ chối đoán khi thiếu nguồn.
- Lớp kiến trúc dữ liệu: đảm bảo AI chỉ trả lời từ nguồn tuyển sinh/học bổng chính thức, kiểm tra nguồn còn mới không, và log lỗi để đội tuyển sinh sửa.

---

## Phần B - Chọn định dạng demo

Mỗi lớp cần một bản demo. Demo giúp biến ý tưởng thành thứ trực quan để nhóm khác xem, kiểm tra và phản biện.

| Lớp | Thư mục | Định dạng demo chọn | Thời gian dự kiến |
|---|---|---|---|
| Giao diện | `1-uiux` | HTML đơn giản mô phỏng chatbot + trạng thái nguồn + nút chuyển tư vấn viên | 20 phút |
| Chỉ dẫn AI | `2-prompt` | Bản prompt trong Markdown + quy tắc + ví dụ hỏi đáp | 15 phút |
| Kiến trúc dữ liệu | `3-architecture` | Mermaid diagram trong Markdown | 15 phút |

**Lý do chọn demo**

- Giao diện: HTML giúp người phản biện nhìn rõ người dùng sẽ thấy nhãn nguồn, cảnh báo và nút chuyển tư vấn viên ở đâu.
- Chỉ dẫn AI: Markdown phù hợp để mô tả rule, mẫu từ chối, mẫu hỏi lại và test bằng ví dụ.
- Kiến trúc dữ liệu: Mermaid diagram giúp thấy luồng dữ liệu từ câu hỏi người dùng đến RAG, kiểm tra nguồn, AI trả lời, fallback và logging.

Gợi ý: có thể dùng AI để dựng nhanh bản nháp demo, nhưng nhóm phải đọc lại, sửa thuật ngữ, và kiểm tra tính khả thi.

### Chọn demo theo điều cần chứng minh

| Nếu cần chứng minh... | Demo phù hợp |
|---|---|
| Người dùng nhìn thấy gì | Sketch, Figma, HTML, ASCII UI |
| AI được chỉ dẫn thế nào | Bản prompt trong Markdown, ví dụ trả lời |
| Dữ liệu đi qua đâu | Sơ đồ hộp-mũi tên, ASCII, Mermaid |
| Quy trình chuyển sang người thật | Sơ đồ quy trình |

---

## Phần C - Ba lớp giải pháp

Ghi tóm tắt ở đây. Chi tiết nằm trong `card.md` và `demo.*` của từng thư mục.

### Lớp 1 - Giao diện (`artifact/1-uiux/`)

- **Cách tiếp cận**: Thiết kế giao diện chatbot có trạng thái xác minh rõ ràng cho câu trả lời về deadline / học bổng: "Đã xác minh từ nguồn chính thức", "Chưa có nguồn chính thức", hoặc "Cần tư vấn viên kiểm tra". Khi thiếu nguồn, giao diện không trình bày câu trả lời như fact mà hiển thị cảnh báo ngắn, link trang tuyển sinh và nút chuyển tư vấn viên.
- **Hành động phòng vệ bao phủ**: Thông báo / Phát hiện / Khắc phục.
- **Demo**: `artifact/1-uiux/demo.html` hoặc `artifact/1-uiux/demo.md` mô phỏng 3 trạng thái: có nguồn, thiếu nguồn, chuyển tư vấn viên.
- **Trạng thái**: Đang làm.

Link chi tiết:

- `artifact/1-uiux/card.md`
- `artifact/1-uiux/demo.*`

### Lớp 2 - Chỉ dẫn AI (`artifact/2-prompt/`)

- **Cách tiếp cận**: Viết bộ quy tắc hệ thống cho chatbot tuyển sinh: không được đoán deadline, học phí, học bổng; phải kiểm tra nguồn chính thức; phải nói rõ khi chưa có thông tin; phải hỏi lại khi thiếu năm/ngành/loại học bổng; phải chuyển tư vấn viên khi người dùng cần quyết định gấp.
- **Hành động phòng vệ bao phủ**: Ngăn / Từ chối / Hỏi lại / Dẫn nguồn / Khắc phục.
- **Demo**: `artifact/2-prompt/demo.md` gồm prompt chính, mẫu câu khi thiếu nguồn, mẫu câu chuyển tư vấn viên và 3 ví dụ hỏi đáp.
- **Trạng thái**: Đang làm.

Link chi tiết:

- `artifact/2-prompt/card.md`
- `artifact/2-prompt/demo.md`

### Lớp 3 - Kiến trúc dữ liệu (`artifact/3-architecture/`)

- **Cách tiếp cận**: Thiết kế pipeline RAG chỉ dùng nguồn chính thức: website tuyển sinh, trang học bổng, đề án tuyển sinh, FAQ, hotline/email tuyển sinh. Trước khi AI trả lời thông tin deadline / học bổng, hệ thống phải kiểm tra có nguồn phù hợp, còn hiệu lực và đúng năm tuyển sinh hay không. Nếu thiếu nguồn hoặc nguồn quá cũ, hệ thống trả trạng thái "no verified source" và chuyển sang câu trả lời an toàn.
- **Hành động phòng vệ bao phủ**: Ngăn / Phát hiện / Khắc phục / Theo dõi.
- **Demo**: `artifact/3-architecture/demo.md` bằng Mermaid diagram: user question -> risk classifier -> source retriever -> freshness check -> answer generator hoặc human handoff -> logging.
- **Trạng thái**: Đang làm.

Link chi tiết:

- `artifact/3-architecture/card.md`
- `artifact/3-architecture/demo.md`

---

## Tổng kiểm tra

| Câu hỏi | Trả lời |
|---|---|
| Rủi ro chính đã chọn là gì? | T-01 - AI bịa deadline học bổng 2026 khi chưa có nguồn chính thức |
| Nguyên nhân gốc là gì? | Thiếu nguồn chính thức/cập nhật, AI đoán khi thiếu nguồn, UI làm người dùng tin quá mức, thiếu luồng chuyển tư vấn viên và thiếu logging |
| 3 lớp giải pháp đã đủ chưa? | Giao diện: có / Chỉ dẫn AI: có / Kiến trúc: có |
| 4 hành động đã bao phủ chưa? | Ngăn: có / Phát hiện: có / Khắc phục: có / Thông báo: có |
| Nhóm khác đã góp ý chưa? | Chưa - sẽ ghi sau phần phản biện chéo |
| Nhóm đã sửa gì sau phản biện? | Chưa - sẽ cập nhật sau khi nhận góp ý |

## Phản biện chéo: 4 câu phải trả lời

Khi nhóm khác góp ý, hoặc khi nhóm tự rà lại, dùng 4 câu này:

| Góc phản biện | Câu hỏi | Trả lời hiện tại của nhóm |
|---|---|---|
| Đúng tầng | Giải pháp có sửa đúng nguyên nhân gốc không? | Có. Tầng dữ liệu/RAG xử lý thiếu nguồn; prompt xử lý AI đoán; UI xử lý người dùng tin quá mức. |
| Cụ thể | Demo có đủ rõ để hiểu cách vận hành không? | Cần thể hiện rõ 3 trạng thái: có nguồn, thiếu nguồn, chuyển tư vấn viên. |
| Đủ lớp | 3 lớp có bổ sung cho nhau không, hay đang lặp cùng một ý? | Có bổ sung: kiến trúc quyết định dữ liệu, prompt quyết định hành vi AI, UI quyết định cách người dùng nhìn và hành động. |
| Tác dụng phụ | Giải pháp có làm chậm, tốn kém, rối giao diện, hoặc gây hiểu nhầm mới không? | Có thể làm phản hồi chậm hơn và giao diện nhiều cảnh báo hơn; giảm bằng cache nguồn chính thức, cảnh báo ngắn, chỉ bật kiểm tra nguồn nghiêm ngặt với câu hỏi rủi ro cao. |

Ghi góp ý cụ thể vào `card.md` hoặc phần tổng kiểm tra. Không ghi chung chung "ổn" hoặc "chưa ổn".

## Gợi ý chia việc

Nhóm 3 người:

- Nguyễn Thành Đại Khánh: `artifact/1-uiux/`
- Bùi Trọng Anh: `artifact/2-prompt/`
- Nguyễn Tiến Thành: `artifact/3-architecture/`

5 phút cuối: cả nhóm đọc chéo 3 lớp, sửa lại bảng tổng kiểm tra, rồi chuẩn bị phần phản biện chéo.
