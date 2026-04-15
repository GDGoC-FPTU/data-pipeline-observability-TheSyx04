[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574100&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** minhquantsy@gmail.com
**Name:** Trần Sỹ Minh Quân

---

## Mô tả

Trong bài lab này, tôi đã xây dựng một ETL pipeline quan sát dữ liệu cơ bản:
- Extract dữ liệu từ `raw_data.json`
- Validate để loại bỏ records không hợp lệ (`price <= 0`, `category` rỗng)
- Transform dữ liệu (giảm giá 10%, chuẩn hóa category về Title Case, thêm `processed_at`)
- Load kết quả ra `processed_data.csv`

Ngoài ra, tôi còn thực hiện stress test bằng `agent_simulation.py` để so sánh phản hồi của agent giữa clean data và garbage data.

---

## Cách chạy (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chạy ETL Pipeline
```bash
python solution.py
```

### Chạy Agent Simulation (Stress Test)
```bash
python generate_garbage.py
python agent_simulation.py
```

`agent_simulation.py` sẽ tự động test 2 kịch bản:
- CLEAN data: đọc từ `processed_data.csv`
- GARBAGE data: đọc từ `garbage_data.csv`

---

## Cấu trúc thư mục

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output của pipeline
├── experiment_report.md     # Báo cáo thí nghiệm
└── README.md                # File này
```

---

## Kết quả

- Tổng số records đầu vào: 5
- Records hợp lệ sau validate: 3
- Records bị loại: 2
	- 1 record có `price <= 0`
	- 1 record có `category` rỗng
- Output tạo được: `processed_data.csv` gồm các cột:
	- `id`, `product`, `price`, `category`, `discounted_price`, `processed_at`

Tóm tắt stress test:
- Clean Data: Agent trả lời hợp lý (Laptop, $1200)
- Garbage Data: Agent bị lệch bởi outlier và trả lời không hợp lý (Nuclear Reactor, $999999)
