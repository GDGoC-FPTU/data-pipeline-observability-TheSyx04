# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600308
**Name:** Trần Sỹ Minh Quân
**Date:** 15/4/2026

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 9/10 | Hợp lý vì trong nhóm Electronics, Laptop có giá cao nhất (1200$). |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 2/10 | Kết quả có giá cực lớn, không thức tế. |

---

## 2. Phân tích & nhận xét (Phan tich & nhan xet)

### Tại sao Agent trả lời sai khi dùng Garbage Data? (Tai sao Agent tra loi sai khi dung Garbage Data?)

Agent trong `agent_simulation.py` chọn sản phẩm Electronics có giá cao nhất, nên rất nhạy cảm với chất lượng dữ liệu đầu vào. Trong `garbage_data.csv` có nhiều lỗi: duplicate ID (id=1 lặp lại), sai kiểu dữ liệu (`ten dollars`), outlier cực lớn (`Nuclear Reactor` giá 999999), và null/zero (`Ghost Item`). Vì agent không validate khi stress test, outlier giá trị lớn nhất sẽ thắng trong phép `idxmax`, dẫn đến trả lời lệch hoàn toàn. Ngoài ra, wrong data type và null values có thể gây lỗi hoặc làm giảm độ tin cậy của truy vấn, cho thấy nếu không có data observability thì prompt tốt vẫn cho ra kết quả tệ.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** (Đồng ý hay không? Giải thích ngắn gọn.)

Đồng ý. Prompt chỉ điều khiển cách hỏi, còn kết quả cuối cùng phụ thuộc trực tiếp vào dữ liệu mà agent thấy. Khi data sạch (`processed_data.csv`), agent trả lời hợp lý và ổn định, còn khi data bẩn (`garbage_data.csv`), agent bị nhiễu và đưa ra lựa chọn sai.
