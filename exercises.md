# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Ở temperature=0.0, model cho ra phản hồi gần như giống nhau mỗi lần chạy — câu chữ súc tích, chính xác, rất ít biến đổi. Khi temperature tăng lên 0.5 và 1.0, câu trả lời bắt đầu đa dạng hơn về cách diễn đạt, thêm chi tiết màu sắc và ví dụ khác nhau qua mỗi lần. Ở temperature=1.5, phản hồi trở nên sáng tạo và bất ngờ nhất nhưng đôi khi lan man hoặc lặp từ bất thường — xác suất chọn token ít phổ biến tăng cao đến mức có thể ảnh hưởng tính mạch lạc.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Nên đặt temperature=0.2. Chatbot hỗ trợ khách hàng cần trả lời nhất quán, chính xác và chuyên nghiệp — tránh sự sáng tạo không cần thiết có thể dẫn đến thông tin sai hoặc lời hứa không phù hợp với chính sách công ty.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Giả sử mỗi lần gọi gồm ~175 input tokens + 175 output tokens (tổng 350 tokens):
> - GPT-4o: (175 × $5.00 + 175 × $20.00) / 1,000,000 ≈ **$0.004375/call** → $131.25/ngày
> - GPT-4o-mini: (175 × $0.15 + 175 × $0.60) / 1,000,000 ≈ **$0.000131/call** → $3.94/ngày
>
> **GPT-4o đắt hơn khoảng 33 lần** so với GPT-4o-mini cho workload này.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> **GPT-4o xứng đáng:** Phân tích hợp đồng pháp lý hoặc chẩn đoán lỗi code phức tạp — nơi lập luận nhiều bước và độ chính xác cao ảnh hưởng trực tiếp đến kết quả kinh doanh, sai một câu có thể gây thiệt hại lớn hơn nhiều so với chênh lệch chi phí.
> **GPT-4o-mini phù hợp hơn:** Phân loại email, gắn nhãn nội dung, hoặc trả lời FAQ đơn giản — những tác vụ có cấu trúc rõ ràng, ít cần suy luận sâu, nơi tiết kiệm 97% chi phí mà chất lượng không chênh lệch đáng kể.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các giao diện chat trực tiếp hoặc khi model cần sinh văn bản dài (giải thích, viết code, soạn thảo) — người dùng thấy token xuất hiện ngay lập tức thay vì chờ vài giây nhìn màn hình trắng, giúp trải nghiệm cảm giác nhanh hơn và tự nhiên hơn dù tổng thời gian không đổi. Ngược lại, non-streaming phù hợp hơn khi cần toàn bộ phản hồi trước khi xử lý tiếp — ví dụ như pipeline tự động phân tích sentiment, dịch thuật batch, hoặc khi kết quả cần được kiểm tra/format trước khi hiển thị — vì việc ghép stream lại thêm độ phức tạp không cần thiết trong những trường hợp này.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
