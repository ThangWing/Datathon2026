# Datathon 2026 — The Gridbreaker

> Repository nộp bài Vòng 1 cuộc thi **DATATHON 2026 — The Gridbreaker**, được tổ chức bởi VinTelligence — VinUniversity Data Science & AI Club.

## 1. Giới thiệu dự án

Dự án giải quyết bài toán phân tích dữ liệu cho một doanh nghiệp thương mại điện tử thời trang tại Việt Nam. Bộ dữ liệu mô phỏng hoạt động bán hàng, khách hàng, sản phẩm, khuyến mãi, tồn kho, vận chuyển, hoàn trả, đánh giá và lưu lượng truy cập website trong giai đoạn lịch sử.

Repo này bao gồm toàn bộ mã nguồn, notebook, dashboard, hình ảnh phân tích, báo cáo và file dự báo dùng để nộp lên Kaggle cho Vòng 1.

Mục tiêu chính của bài làm:

- **Phần 1 — MCQ:** tính toán trực tiếp từ dữ liệu để trả lời 10 câu hỏi trắc nghiệm.
- **Phần 2 — EDA & Data Storytelling:** trực quan hóa và phân tích dữ liệu theo bốn cấp độ: Descriptive, Diagnostic, Predictive và Prescriptive.
- **Phần 3 — Sales Forecasting:** xây dựng mô hình dự báo `Revenue` và `COGS` cho giai đoạn test, đồng thời đảm bảo tính tái lập và kiểm soát leakage.

## 2. Cấu trúc thư mục

```text
Datathon2026/
│
├── Code/
│   ├── datathon_part1_pipeline.ipynb      # Notebook xử lý Phần 1: tính toán đáp án MCQ
│   ├── datathon_part2_eda.pbix            # Dashboard Power BI cho Phần 2
│   └── datathon_part3_pipeline.ipynb      # Notebook pipeline dự báo Phần 3
│
├── Dataset/
│   ├── customers.csv                      # Thông tin khách hàng
│   ├── geography.csv                      # Thông tin địa lý theo zip code
│   ├── inventory.csv                      # Tồn kho theo sản phẩm và tháng
│   ├── orders.csv                         # Thông tin đơn hàng
│   ├── order_items.csv                    # Chi tiết sản phẩm trong từng đơn hàng
│   ├── payments.csv                       # Thông tin thanh toán
│   ├── products.csv                       # Danh mục sản phẩm
│   ├── promotions.csv                     # Thông tin chương trình khuyến mãi
│   ├── returns.csv                        # Thông tin trả hàng
│   ├── reviews.csv                        # Đánh giá sản phẩm
│   ├── sales.csv                          # Dữ liệu doanh thu huấn luyện
│   ├── sample_submission.csv              # File mẫu định dạng nộp Kaggle
│   ├── shipments.csv                      # Thông tin vận chuyển
│   └── web_traffic.csv                    # Lưu lượng truy cập website
│
├── Images/
│   ├── descriptive.jpg                    # Hình minh họa/phân tích cấp độ descriptive
│   ├── diagnostic.jpg                     # Hình minh họa/phân tích cấp độ diagnostic
│   ├── predictive.jpg                     # Hình minh họa/phân tích cấp độ predictive
│   └── SHAP.png                           # Hình giải thích mô hình bằng SHAP/feature importance
│
├── Reports/
│   └── Datathon_Report.pdf                # Báo cáo cuối cùng theo template hội nghị
│
├── Results/
│   └── datathon_part3_submission.csv      # File dự báo cuối cùng dùng để nộp Kaggle
│
└── README.md                              # Tài liệu mô tả repo và hướng dẫn chạy lại
```

## 3. Dữ liệu sử dụng

Bộ dữ liệu trong thư mục `Dataset/` được chia thành bốn nhóm chính:

| Nhóm dữ liệu | File liên quan | Vai trò |
|---|---|---|
| Master | `products.csv`, `customers.csv`, `promotions.csv`, `geography.csv` | Thông tin tham chiếu về sản phẩm, khách hàng, khuyến mãi và địa lý |
| Transaction | `orders.csv`, `order_items.csv`, `payments.csv`, `shipments.csv`, `returns.csv`, `reviews.csv` | Dữ liệu giao dịch, thanh toán, vận chuyển, hoàn trả và đánh giá |
| Analytical | `sales.csv`, `sample_submission.csv` | Dữ liệu huấn luyện và định dạng file nộp |
| Operational | `inventory.csv`, `web_traffic.csv` | Dữ liệu vận hành về tồn kho và lưu lượng truy cập |

Trong bài toán forecasting, `sales.csv` là dữ liệu huấn luyện chính, bao gồm:

- `Date`: ngày ghi nhận doanh thu.
- `Revenue`: doanh thu thuần theo ngày.
- `COGS`: giá vốn hàng bán theo ngày.

File `sample_submission.csv` được dùng làm khung thời gian dự báo và định dạng đầu ra cuối cùng.

## 4. Nội dung từng phần

### 4.1. Phần 1 — Câu hỏi trắc nghiệm

Notebook:

```text
Code/datathon_part1_pipeline.ipynb
```

Notebook này thực hiện các phép tính trực tiếp từ dữ liệu để trả lời 10 câu hỏi MCQ, bao gồm:

- inter-order gap giữa các lần mua liên tiếp;
- biên lợi nhuận gộp theo phân khúc sản phẩm;
- lý do trả hàng phổ biến;
- bounce rate theo nguồn traffic;
- tỷ lệ áp dụng khuyến mãi;
- số đơn hàng trung bình theo nhóm tuổi;
- doanh thu theo vùng;
- phương thức thanh toán của đơn bị hủy;
- tỷ lệ trả hàng theo kích thước sản phẩm;
- giá trị thanh toán trung bình theo số kỳ trả góp.

### 4.2. Phần 2 — EDA & Data Storytelling

Dashboard:

```text
Code/datathon_part2_eda.pbix
```

Các hình ảnh chính:

```text
Images/descriptive.jpg
Images/diagnostic.jpg
Images/predictive.jpg
```

Phần này tập trung xây dựng câu chuyện dữ liệu theo bốn cấp độ:

| Cấp độ | Câu hỏi chính | Hướng phân tích |
|---|---|---|
| Descriptive | What happened? | Tổng quan doanh thu, đơn hàng, sản phẩm, khu vực, traffic |
| Diagnostic | Why did it happen? | Phân tích nguyên nhân qua khuyến mãi, tồn kho, hoàn trả, kênh bán |
| Predictive | What is likely to happen? | Nhận diện mùa vụ, xu hướng, tín hiệu dẫn dắt doanh thu |
| Prescriptive | What should we do? | Đề xuất hành động về tồn kho, khuyến mãi, marketing và logistics |

Các biểu đồ trong dashboard được thiết kế để hỗ trợ lập luận kinh doanh, không chỉ mô tả số liệu bề mặt.

### 4.3. Phần 3 — Sales Forecasting

Notebook:

```text
Code/datathon_part3_pipeline.ipynb
```

File kết quả:

```text
Results/datathon_part3_submission.csv
```

Mục tiêu là dự báo hai cột:

- `Revenue`
- `COGS`

cho toàn bộ giai đoạn trong `sample_submission.csv`, đồng thời giữ đúng thứ tự dòng theo file mẫu.

Pipeline tổng quát:

1. Đọc dữ liệu từ thư mục `Dataset/`.
2. Chuẩn hóa kiểu dữ liệu thời gian.
3. Tạo đặc trưng lịch:
   - day of week;
   - month;
   - quarter;
   - day of year;
   - week of year;
   - weekend flag;
   - Fourier/sin-cos seasonal features.
4. Tạo đặc trưng chuỗi thời gian:
   - lag features;
   - rolling mean;
   - rolling standard deviation;
   - expanding statistics;
   - seasonal lag theo năm.
5. Bổ sung đặc trưng từ các bảng phụ theo nguyên tắc không dùng dữ liệu ngoài và hạn chế leakage.
6. Huấn luyện mô hình dự báo.
7. Đánh giá bằng validation theo thời gian.
8. Giải thích mô hình bằng feature importance/SHAP.
9. Sinh file submission theo đúng định dạng Kaggle.

## 5. Môi trường chạy

Khuyến nghị chạy notebook bằng **Google Colab** hoặc local Jupyter Notebook.

### 5.1. Cài đặt thư viện

Nếu chạy trên Colab, cài đặt các thư viện cần thiết trước khi chạy notebook:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn lightgbm xgboost shap
```

Nếu chạy local, có thể tạo môi trường Python mới:

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate

pip install pandas numpy matplotlib seaborn scikit-learn lightgbm xgboost shap jupyter
```

### 5.2. Phiên bản Python khuyến nghị

```text
Python >= 3.10
```

## 6. Hướng dẫn chạy lại kết quả

### Bước 1 — Clone repository

```bash
git clone <your-github-repository-url>
cd Datathon2026
```

### Bước 2 — Kiểm tra cấu trúc dữ liệu

Đảm bảo thư mục `Dataset/` có đầy đủ các file CSV sau:

```text
customers.csv
geography.csv
inventory.csv
orders.csv
order_items.csv
payments.csv
products.csv
promotions.csv
returns.csv
reviews.csv
sales.csv
sample_submission.csv
shipments.csv
web_traffic.csv
```

### Bước 3 — Chạy notebook Phần 1

Mở và chạy toàn bộ notebook:

```text
Code/datathon_part1_pipeline.ipynb
```

Kết quả notebook dùng để đối chiếu và chọn đáp án cho phần câu hỏi trắc nghiệm.

### Bước 4 — Xem dashboard Phần 2

Mở file Power BI:

```text
Code/datathon_part2_eda.pbix
```

File này chứa dashboard trực quan hóa và các phân tích hỗ trợ cho phần báo cáo EDA.

Nếu không có Power BI Desktop, có thể xem nhanh các hình xuất sẵn trong thư mục:

```text
Images/
```

### Bước 5 — Chạy notebook Phần 3

Mở và chạy toàn bộ notebook:

```text
Code/datathon_part3_pipeline.ipynb
```

Notebook sẽ thực hiện feature engineering, huấn luyện mô hình, giải thích mô hình và tạo file dự báo cuối cùng.

### Bước 6 — Kiểm tra file submission

File submission cuối cùng nằm tại:

```text
Results/datathon_part3_submission.csv
```

Định dạng cần có:

```text
Date,Revenue,COGS
```

Lưu ý:

- Không đổi tên cột.
- Không sắp xếp lại dòng.
- Không thay đổi số lượng dòng so với `sample_submission.csv`.
- Không dùng dữ liệu ngoài hoặc dữ liệu tương lai không được cung cấp.

## 7. Reproducibility

Để đảm bảo kết quả có thể tái lập:

- Các bước xử lý dữ liệu được đóng gói trong notebook.
- Dữ liệu đầu vào được lưu trong `Dataset/`.
- File nộp cuối cùng được lưu trong `Results/`.
- Random seed được cố định trong quá trình huấn luyện khi cần.
- Validation được thiết kế theo hướng tôn trọng thứ tự thời gian.
- Các đặc trưng được tạo từ dữ liệu được cung cấp, không sử dụng nguồn dữ liệu ngoài.

## 8. Kiểm soát leakage

Trong phần forecasting, repo tuân thủ các nguyên tắc sau:

- Không sử dụng `Revenue` hoặc `COGS` thực tế của tập test làm đặc trưng.
- Không dùng dữ liệu ngoài bộ dữ liệu được cung cấp.
- Các đặc trưng rolling/lag được tạo theo hướng chỉ sử dụng thông tin quá khứ.
- Các bảng phụ như đơn hàng, tồn kho, traffic, trả hàng và review được xử lý cẩn thận để tránh đưa thông tin tương lai vào mô hình.
- File submission giữ đúng cấu trúc của `sample_submission.csv`.

## 9. Báo cáo cuối cùng

Báo cáo PDF nằm tại:

```text
Reports/Datathon_Report.pdf
```

Báo cáo bao gồm:

- phần trực quan hóa và phân tích dữ liệu;
- câu chuyện dữ liệu và insight kinh doanh;
- phương pháp xây dựng mô hình forecasting;
- pipeline feature engineering;
- kết quả thực nghiệm;
- giải thích mô hình bằng SHAP/feature importance;
- đề xuất hành động cho doanh nghiệp.

## 10. Kết quả nộp

File dự báo chính thức:

```text
Results/datathon_part3_submission.csv
```

File này được dùng để nộp lên Kaggle theo yêu cầu của cuộc thi.

## 11. Ghi chú cho ban giám khảo

Repo được tổ chức nhằm hỗ trợ kiểm tra nhanh ba nội dung chính:

1. **Tính đầy đủ:** có notebook cho MCQ, dashboard EDA, notebook forecasting, báo cáo và file submission.
2. **Tính tái lập:** dữ liệu, mã nguồn và kết quả được đặt trong các thư mục riêng biệt, dễ chạy lại.
3. **Tính giải thích:** mô hình forecasting có phần phân tích feature importance/SHAP để diễn giải các yếu tố dẫn động doanh thu bằng ngôn ngữ kinh doanh.

## 12. License

Repository này được xây dựng cho mục đích tham gia cuộc thi Datathon 2026. Vui lòng không sử dụng lại dữ liệu hoặc mã nguồn ngoài phạm vi được ban tổ chức cho phép.
