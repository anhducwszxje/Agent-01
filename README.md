# AGENT_01

**BÁO CÁO BÀI TẬP(AGENT_01)**  
**DISCOVERING AI AGENTS**  
**TÌM HIỂU VỀ HỆ TÁC TỬ THÔNG MINH AI AGENT VÀ TÁC TỬ HỌC TĂNG CƯỜNG (REINFORCEMENT LEARNING)**  
Bùi Anh Đức — B23DCCN165 — D23CTPM01

Phần lý thuyết đối chiếu Google Cloud, IBM và McKinsey. Phần thực hành cài đặt Q-learning cho mê cung 10×10 theo bài toán ở GeeksforGeeks, liên hệ learning agent của IBM. Mã được viết lại với seed, giới hạn bước, log, đánh giá và demo.

## Các tệp chính

- `report/AGENT_01_Bao_Cao.pdf`: báo cáo, gồm phần lý thuyết khoảng 6 trang và phần thực hành giải thích từng bước, ảnh code/output, đồ thị và demo.
- `AGENT_01_Q_Learning_Maze.ipynb`: notebook đã chạy đủ 12 code cell, giữ nguyên output.
- `AGENT_01_Q_Learning_Maze.html`: bản xem notebook bằng trình duyệt, không cần mở Jupyter.
- `artifacts/agent_demo.gif`: tác tử tự chạy từ bảng Q đã lưu.
- `artifacts/results.json`: cấu hình và kết quả thực nghiệm.
- `artifacts/training_history.csv`: log 5.000 episode của seed 42.
- `artifacts/demo_trace.csv`: log đủ 24 hành động của demo.
- `artifacts/q_table.npy`: bảng Q sau train.
- `report/main.tex`, `theory.tex`, `practice.tex`, `images/`: nguồn báo cáo.

## Chạy notebook

Dùng Python 3.12. Tạo môi trường trong thư mục dự án rồi cài thư viện:

```bash
python -m venv .venv
# Windows PowerShell
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m jupyterlab
```

Mở `AGENT_01_Q_Learning_Maze.ipynb`, chọn kernel của môi trường vừa cài và chạy **Restart Kernel → Run All**. Thư mục làm việc là thư mục chứa notebook. Các cell tạo lại nội dung trong `artifacts/`. Không cần GPU, API key hoặc tải bộ dữ liệu ngoài.

## Kết quả của lượt chạy đã lưu

| Chính sách từ (0,0) | Số lượt đánh giá | Tỷ lệ tới đích | Reward trung bình | Hành động trung bình |
|---|---:|---:|---:|---:|
| Greedy chưa train | 1000 | 0% | -10.000 | 1.000 |
| Ngẫu nhiên | 1000 | 0% | -10.530 | 1.530 |
| Greedy sau train | 1000 | 100% | 27.000 | 24.000 |

BFS xác nhận đường ngắn nhất có 24 hành động. Năm seed 0, 7, 21, 42, 99 đều tìm được đường cùng độ dài. Khi đổi điểm xuất phát tới tất cả 42 ô trống không phải đích, chính sách seed 42 chỉ tới đích từ 27 ô (64.3%). Các thất bại được giữ trong `results.json`.

1000 lượt greedy cùng điểm đầu trên bản đồ tất định lặp lại cùng một đường đi. Đây là đánh giá môi trường đã học, chưa phải thử trên các bản đồ mới. Tỷ lệ thành công ở 500 episode train cuối là 87.6% vì lúc train còn khám phá, còn demo tắt khám phá.

## Liên hệ learning agent

- Chọn hành động: `choose_action` trong train và `argmax Q` trong demo.
- Học: cập nhật từng phần tử Q theo reward và giá trị trạng thái tiếp theo.
- Phản hồi: hàm `step` trả reward và trạng thái kết thúc.
- Khám phá: nhánh chọn ngẫu nhiên trong epsilon-greedy.

BFS chỉ dùng đối chiếu sau train. Demo nạp lại `q_table.npy` và không gọi BFS, không lọc hành động đâm tường hoặc loại ô đã thăm.

## Biên dịch báo cáo

Biên dịch `report/main.tex` bằng XeLaTeX hai lần trong thư mục `report`. Font ưu tiên Times New Roman; mẫu cũng hỗ trợ pdfLaTeX với cấu hình tiếng Việt. Ảnh trong báo cáo đã có đầy đủ.

```bash
cd report
xelatex -interaction=nonstopmode -halt-on-error main.tex
xelatex -interaction=nonstopmode -halt-on-error main.tex
```

## Đưa lên GitHub

Giữ notebook cùng `artifacts/`, `requirements.txt`, `README.md` và `report/`. Tệp `.gitignore` loại môi trường Python, checkpoint và tệp tạm LaTeX. Chưa có thao tác commit, push hoặc tạo repository từ bộ bàn giao này.

## Nguồn

1. [Google Cloud — What are AI agents?](https://cloud.google.com/discover/what-are-ai-agents)
2. [IBM — What are AI agents?](https://www.ibm.com/think/topics/ai-agents)
3. [McKinsey — What is an AI agent?](https://www.mckinsey.com/featured-insights/mckinsey-explainers/what-is-an-ai-agent)
4. [GeeksforGeeks — Reinforcement Learning](https://www.geeksforgeeks.org/machine-learning/what-is-reinforcement-learning/) — nguồn bài toán, bản đồ và cấu hình cơ bản; mã notebook được viết lại.
5. [Yao et al. — ReAct](https://arxiv.org/abs/2210.03629)

Ngày truy cập: 23/10/2026.
