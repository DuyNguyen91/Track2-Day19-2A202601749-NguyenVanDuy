# Reflection — Lab 19

**Tên:** Nguyễn Văn Duy

**Cohort:** A20-K3

**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

- **Kết quả theo query type:**
  - `exact`: BM25 và Hybrid có độ chính xác cao nhất (~97%) vì từ khóa kỹ thuật xuất hiện nguyên văn trong tài liệu.
  - `paraphrase`: Vector search chiếm ưu thế so với BM25 nhờ khả năng bắt khớp ngữ nghĩa thay vì dựa vào từ khóa chính xác.
  - `mixed`: Hybrid (RRF=60) vượt trội hoàn toàn (~100%) nhờ kết hợp tín hiệu từ cả keyword matching và semantic similarity.
- **Khi nào không dùng Hybrid:**
  - Không dùng khi hệ thống yêu cầu độ trễ cực thấp (< 5-10ms) với tài nguyên giới hạn (pure BM25 nhẹ hơn rất nhiều vì không cần inference embedding model).
  - Không dùng khi bài toán tìm kiếm mã định danh, ID, mã đơn hàng, cú pháp code chính xác (pure BM25 tối ưu hơn). Ngược lại, khi tìm kiếm đa ngôn ngữ / cross-lingual hoặc văn bản mô tả trừu tượng thì pure vector là đủ tốt.

---

## Điều ngạc nhiên nhất khi làm lab này

- Thuật toán RRF tuy đơn giản (không cần chuẩn hóa điểm số) nhưng lại mang lại độ chính xác tổng thể và tính ổn định vượt trội trên mọi dạng câu hỏi.
- **Hạn chế thực tế về độ trễ:** Khi chạy `fastembed` bằng CPU (qua ONNX Runtime) trên môi trường máy cá nhân / WSL, thời gian inference sinh embedding cho mỗi query mất khoảng ~120–150ms, khiến P99 server-side của Semantic và Hybrid dao động quanh mức 150–240ms, khó đạt ngưỡng < 50ms nếu không có GPU hoặc dedicated embedding service.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
