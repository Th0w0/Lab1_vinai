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
> Khi temperature tăng từ 0.0 đến 1.5, phản hồi trở nên ngẫu nhiên và sáng tạo hơn nhưng cũng kém ổn định và có thể trở nên vô nghĩa ở mức cao (1.5). Ở 0.0, phản hồi là xác định (deterministic) và có tính lặp lại cao nhất, trong khi ở 1.5, mô hình có thể tạo ra các từ ngữ lạ hoặc cấu trúc câu không chuẩn.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature thấp (0.0 đến 0.2). Trong hỗ trợ khách hàng, tính chính xác và nhất quán là quan trọng nhất; chúng ta muốn chatbot đưa ra cùng một câu trả lời chính xác cho cùng một câu hỏi và tránh hiện tượng "ảo tưởng" (hallucination).

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> GPT-4o ($0.010/1K tokens) đắt hơn GPT-4o-mini ($0.0006/1K tokens) khoảng 16.67 lần. Với workload 10,000 users * 3 calls * 350 tokens = 10,500,000 tokens mỗi ngày, sự chênh lệch chi phí là rất đáng kể.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng khi cần khả năng suy luận phức tạp, phân tích dữ liệu chuyên sâu hoặc viết lách sáng tạo chất lượng cao. GPT-4o-mini tốt hơn cho các tác vụ đơn giản như phân loại văn bản, tóm tắt ý chính, hoặc các ứng dụng yêu cầu độ trễ cực thấp và chi phí tối ưu.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các ứng dụng đối thoại trực tiếp (Chatbot UI) vì nó giúp giảm "độ trễ cảm nhận" (perceived latency), cho phép người dùng bắt đầu đọc ngay khi tokens đầu tiên được sinh ra. Non-streaming phù hợp hơn khi hệ thống cần xử lý kết quả trước khi hiển thị (như kiểm tra kiểm duyệt, phân tích JSON) hoặc trong các quy trình backend tự động không có giao diện người dùng trực tiếp.


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
