# Phân Tích Dữ Liệu & Dự Đoán Lợi Nhuận Bán Lẻ (Superstore Analysis)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Libraries](https://img.shields.io/badge/Library-Sklearn%20%7C%20Pandas%20%7C%20NumPy%20%7C%20Seaborn%20%7C%20Matplotlib-orange)

## 1. Tổng quan dự án & Thông tin nhóm (Project Overview & Team Info)

Dự án này tập trung phân tích bộ dữ liệu bán lẻ **Superstore** để tìm ra các yếu tố ảnh hưởng đến doanh số và lợi nhuận. Mục tiêu chính là xây dựng các mô hình Học máy (Machine Learning) để dự đoán lợi nhuận đơn hàng và phân loại rủi ro (Lãi/Lỗ), từ đó đề xuất chiến lược tối ưu hóa mức chiết khấu (Discount).

### Thành viên nhóm:
1. **Cao Tiến Thành** - 23120088
2. **Lê Minh Hải** - 23120041
3. **Phạm Ngọc Duy** - 23120035

---

## 2. Nguồn dữ liệu & Mô tả (Dataset Source & Description)

* **Nguồn dữ liệu:** [Kaggle - Superstore Dataset](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)
* **Tên file:** `Superstore.csv`
* **Kích thước:** 9994 dòng, 21 cột.

**Các đặc trưng chính (Features):**
* `Order Date`, `Ship Date`: Thông tin thời gian.
* `Ship Mode`, `Segment`, `Region`: Thông tin vận chuyển và khách hàng.
* `Category`, `Sub-Category`: Loại sản phẩm.
* `Sales`, `Quantity`, `Discount`: Các chỉ số bán hàng.
* `Profit`: Lợi nhuận.

---

## 3. Câu hỏi nghiên cứu (Research Questions)

Dự án tập trung giải quyết các câu hỏi cốt lõi sau:

1. Các đặc trưng nào có khả năng làm ảnh hưởng lợi nhuận (`Profit`) và dự đoán lợi nhuận của sản phẩm trước khi nó được mua?
2. Có thể phân cụm khách hàng dựa trên hành vi mua sắm như thế nào, từ đó đề ra các chiến lược cụ thể cho từng nhóm?
3.  Dựa trên các đặc trưng giao dịch, liệu chúng ta có thể xây dựng hệ thống cảnh báo sớm để tự động phát hiện các đơn hàng **'Rủi ro'** trước khi duyệt không? Các yếu tố nào là tín hiệu cảnh báo mạnh nhất?
4. Đâu là những **"Hố đen tài chính"** tại các thị trường trọng điểm? Cụ thể, nhóm sản phẩm (**Sub-Category**) nào tại các Tiểu bang đang có Doanh số cao nhưng Lợi nhuận âm?
5. Theo thời gian (năm, quý, tháng) doanh số và lợi nhuận có xu hướng thế nào? Có thời điểm **“đỉnh điểm”** hoặc “thấp điểm” không?"
6. Sản phẩm nào thuộc nhóm **"Hot items"** chỉ bán chạy trong các tháng cụ thể?

---

## 4. Tóm tắt kết quả chính (Key Findings Summary)

Sau quá trình phân tích và huấn luyện mô hình, có thể rút ra các kết luận sau:

### Về kinh doanh (Business Insights):

* **Phân cụm khách hàng** (Customer Clustering): Mô hình K-Means xác định 4 nhóm khách hàng chiến lược dựa trên hành vi tiêu dùng (RFM):

    * **VIP**: Nhóm giá trị nhất chi tiêu lớn, tần suất cao. Cần tập trung duy trì lòng trung thành qua dịch vụ ưu tiên.

    * **Tiềm năng**: Nhóm hoạt động tích cực nhất giao dịch gần nhất, chi tiêu vừa. Cơ hội vàng để Upsell/Cross-sell thúc đẩy lên hạng VIP.

    * **Ngủ đông**: Khách hàng cũ có giá trị khá chi tiêu khá ổn nhưng lâu rồi chưa quay lại, cần chiến dịch Win-back (lôi kéo lại).

    * **Rời bỏ**: Nhóm chi tiêu thấp và ngừng mua gần khá lâu, chiến lược là tối ưu chi phí bằng cách hạn chế tiếp thị.

* Nhóm đơn hàng bị lỗ có mức giảm giá cao gấp **5.9 lần** so với nhóm an toàn. Điều này khẳng định mức chiết khấu **> 20%** là nguyên nhân chính dẫn đến thua lỗ. Điểm tối ưu ("Sweet Spot") cho lợi nhuận là mức giảm giá **10%**.

* Dữ liệu cho thấy cả Doanh số và Lợi nhuận đều có xu hướng tăng rõ rệt qua từng năm (2014-2017). Quý 4 (Tháng 10, 11, 12) là quý có Doanh số và Lợi nhuận cao nhất trong tất cả các năm.  

* Các sản phẩm **"Hot Items"** này chủ yếu nằm trong danh mục Office Supplies (Văn phòng phẩm) - nhóm hàng thường có giá trị cao, và việc mua sắm của chúng thường gắn liền với ngân sách và chu kỳ kinh doanh của doanh nghiệp (Phân khúc Corporate/Home Office).


### Về mô hình (Model Performance):

* **Dự đoán Lợi nhuận (Regression):**
    * Mô hình **Random Forest Regressor** hoạt động tốt nhất với **R² ~ 0.72**.

    * Mô hình **Linear Regression** kém hiệu quả hơn do các đặc trưng không có tương quan mạnh và chủ yếu là các mối quan hệ phi tuyến tính.

* **Phân cụm khách hàng (Customer Clustering):**
    * Mô hình **K-means Clustering**: Cho thấy khả năng phân cụm tương đối ổn. Với số cụm **K = 4** được tính bằng **Elbow Method (Phương pháp khuỷu tay)**.

    * Mô hình đối sánh - **Hierarchical Clustering (Phân cụm phân cấp)**. Dùng làm tham chiếu (benchmark) để kiểm tra độ ổn định của các cụm tìm được bởi K-Means. Kết quả cho thấy **Silhouette Score** của hai mô hình là tương đương.

* **Phân loại Rủi ro Lãi/Lỗ (Classification):**
    * Mô hình **Random Forest Classifier** đạt độ chính xác tổng thể **~97%**.

    * Đạt chỉ số **Recall cho lớp Rủi ro (1) rất cao: 0.96**. Điều này có nghĩa là mô hình bắt được **96%** tổng số đơn hàng bị lỗ, bỏ sót rất ít các đơn hàng rủi ro.

---

## 5. Cấu trúc thư mục (File Structure)

```bash
Superstore_Sales_Analysis
├── Data/
│   └── Superstore.csv            # Dữ liệu gốc
├── Notebooks/
│   ├── Data_Analysis.ipynb       # Đặt câu hỏi phân tích dữ liệu (Model)
│   ├── Data_Collection.ipynb     # Thu thập dữ liệu
│   └── Data_Exploration.ipynb    # Khám phá dữ liệu
├── README.md                     # Tài liệu hướng dẫn dự án
└── requirements.txt              # Danh sách thư viện cần thiết
```

## 6. Hướng dẫn chạy dự án (How to Run)
Để tái lập kết quả phân tích, vui lòng thực hiện theo các bước sau:

Bước 1: Clone dự án về máy và truy cập vào thư mục chính

```bash
git clone https://github.com/TThanhc/Superstore_Sales_Analysis.git
```

Bước 2: Cài đặt thư viện.

```bash
pip install -r requirements.txt
```

Bước 3: Mở Jupyter Notebook

```bash
jupyter notebook
```

Bước 4: Chạy các file trong thư mục notebooks/.

```bash
Run All
```

**Lưu ý**: Đảm bảo đang ở thư mục chính của dự án.

## 7. Thư viện sử dụng (Dependencies List)
Dự án được xây dựng trên ngôn ngữ Python 3.x và các thư viện sau:

* Xử lý dữ liệu: pandas, numpy

* Trực quan hóa: matplotlib, seaborn

* Học máy (Machine Learning): scikit-learn

* Models: LinearRegression, LogisticRegression, KMeans, RandomForestRegressor, RandomForestClassifier.

* Preprocessing: StandardScaler, OneHotEncoder.

* Metrics: r2_score, mean_squared_error, classification_report, roc_auc_score, silhouette_score. 