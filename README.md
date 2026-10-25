# THÔNG TIN ĐỒ ÁN

- **Họ tên:** Võ Duy Lộc
- **MSSV:** 24127441

## MÔ TẢ TẬP DỮ LIỆU

Đồ án sử dụng hai tập dữ liệu để nghiên cứu các kỹ thuật khám phá, làm sạch và tiền xử lý dữ liệu:

1. **Dữ liệu dạng bảng:** Adult Census Income.
2. **Dữ liệu văn bản:** IMDB 50K Movie Reviews.

---

## 1. TẬP DỮ LIỆU DẠNG BẢNG — ADULT CENSUS INCOME

### 1.1. Bối cảnh

Bộ dữ liệu **Adult Census Income**, còn được gọi là *Adult* hoặc *Census Income*, được xây dựng từ dữ liệu điều tra dân số Hoa Kỳ. Mục tiêu của bài toán là dự đoán thu nhập hằng năm của một người có vượt quá 50.000 USD hay không, dựa trên các thông tin nhân khẩu học và nghề nghiệp.

Tập dữ liệu phù hợp để thực hành tiền xử lý dữ liệu dạng bảng vì có cả thuộc tính số và thuộc tính phân loại, đồng thời chứa các giá trị khuyết tự nhiên. Đồ án sẽ tập trung vào phân tích dữ liệu, xử lý giá trị khuyết, phát hiện ngoại lai, chuẩn hóa dữ liệu, mã hóa biến phân loại, lựa chọn đặc trưng và đánh giá tác động của các phương pháp tiền xử lý.

### 1.2. Thông tin tổng quan

| Thông tin | Mô tả |
|---|---|
| Tên tập dữ liệu | Adult Census Income |
| Nguồn dữ liệu | UCI Machine Learning Repository |
| Số lượng bản ghi | Khoảng 48.842 dòng trong phiên bản kết hợp dữ liệu huấn luyện và kiểm tra |
| Số lượng thuộc tính đầu vào | 14 thuộc tính |
| Biến mục tiêu | `income` — mức thu nhập |
| Các lớp mục tiêu | `<=50K` và `>50K` |
| Kiểu dữ liệu | Kết hợp thuộc tính số và thuộc tính phân loại |
| Giá trị khuyết | Có các giá trị khuyết tự nhiên, thường được biểu diễn bằng dấu `?` trong dữ liệu gốc |

**Lưu ý:** Số lượng bản ghi, tên cột và số lượng giá trị khuyết cần được xác nhận lại bằng mã kiểm tra dữ liệu sau khi tải tập dữ liệu. Các phiên bản lưu trữ khác nhau có thể khác về định dạng hoặc cách biểu diễn nhãn.

### 1.3. Mô tả các thuộc tính

Bộ dữ liệu Adult tiêu chuẩn có 14 thuộc tính đầu vào và một biến mục tiêu. Các thuộc tính đầu vào bao gồm:

| STT | Tên thuộc tính | Mô tả | Kiểu dữ liệu |
|:---:|---|---|---|
| 1 | `age` | Tuổi của người được khảo sát | Số nguyên |
| 2 | `workclass` | Nhóm hoặc loại hình công việc | Phân loại |
| 3 | `fnlwgt` | Trọng số mẫu điều tra dân số | Số nguyên |
| 4 | `education` | Trình độ học vấn | Phân loại |
| 5 | `education-num` | Mã số biểu thị trình độ học vấn | Số nguyên |
| 6 | `marital-status` | Tình trạng hôn nhân | Phân loại |
| 7 | `occupation` | Nghề nghiệp | Phân loại |
| 8 | `relationship` | Vai trò quan hệ trong gia đình | Phân loại |
| 9 | `race` | Nhóm chủng tộc theo dữ liệu khảo sát | Phân loại |
| 10 | `sex` | Giới tính theo dữ liệu khảo sát | Phân loại |
| 11 | `capital-gain` | Thu nhập từ lãi vốn | Số nguyên |
| 12 | `capital-loss` | Khoản lỗ vốn | Số nguyên |
| 13 | `hours-per-week` | Số giờ làm việc trung bình mỗi tuần | Số nguyên |
| 14 | `native-country` | Quốc gia xuất thân | Phân loại |
| 15 | `income` | Mức thu nhập: `<=50K` hoặc `>50K` | Phân loại nhị phân — biến mục tiêu |

### 1.4. Giá trị khuyết và kế hoạch tiền xử lý

Trong dữ liệu Adult tiêu chuẩn, các thuộc tính như `workclass`, `occupation` và `native-country` có thể chứa giá trị `?`, biểu thị thông tin chưa được ghi nhận.

Trong quá trình tải dữ liệu, các giá trị này sẽ được kiểm tra và chuyển thành giá trị khuyết (`NaN`) trước khi phân tích. Tỷ lệ khuyết thiếu thực tế sẽ được tính bằng số lượng và tỷ lệ phần trăm giá trị khuyết trên từng thuộc tính.

Đồ án sẽ thực hiện các nội dung sau:

- Phân tích phân phối dữ liệu và mối quan hệ giữa các thuộc tính.
- Trực quan hóa mẫu hình khuyết thiếu và thảo luận về MCAR, MAR và MNAR.
- So sánh các phương pháp điền khuyết như mean, median, mode, KNN imputation và MICE.
- Phát hiện và đánh giá ngoại lai bằng nhiều phương pháp.
- So sánh các kỹ thuật chuẩn hóa dữ liệu số.
- Thử nghiệm các phương pháp mã hóa biến phân loại.
- Đánh giá tương quan, đa cộng tuyến và lựa chọn đặc trưng.
- Khảo sát các kỹ thuật giảm chiều dữ liệu khi phù hợp.

Đối với thí nghiệm tạo thêm giá trị khuyết MCAR, dữ liệu gốc sẽ được giữ nguyên. Tập dữ liệu dùng cho thí nghiệm sẽ được tạo riêng để có thể so sánh các phương pháp điền khuyết trên những giá trị đã biết trước khi bị che đi.

### 1.5. Phân chia dữ liệu

Dữ liệu sẽ được chia thành:

- **Training set:** 80%.
- **Test set:** 20%.

Sử dụng **Stratified Sampling** theo biến mục tiêu `income` để duy trì tỷ lệ các lớp giữa hai tập dữ liệu.

Các phép biến đổi có tham số học được từ dữ liệu, chẳng hạn như điền khuyết, chuẩn hóa, mã hóa dựa trên mục tiêu và lựa chọn đặc trưng, sẽ được khớp trên tập huấn luyện rồi áp dụng cho tập kiểm tra nhằm tránh rò rỉ dữ liệu (*data leakage*).

---

## 2. TẬP DỮ LIỆU VĂN BẢN — IMDB 50K MOVIE REVIEWS

### 2.1. Bối cảnh

Bộ dữ liệu **IMDB 50K Movie Reviews** được sử dụng cho bài toán phân tích cảm xúc văn bản (*Sentiment Analysis*). Mục tiêu là tiền xử lý các bài đánh giá phim, giảm nhiễu, chuyển đổi văn bản thành đặc trưng số và phân loại cảm xúc thành tích cực hoặc tiêu cực.

Tập dữ liệu phù hợp để khảo sát các kỹ thuật xử lý ngôn ngữ tự nhiên như chuẩn hóa văn bản, tách từ, loại bỏ từ dừng, stemming, lemmatization và vector hóa văn bản.

### 2.2. Thông tin tổng quan

| Thông tin | Mô tả |
|---|---|
| Tên tập dữ liệu | IMDB 50K Movie Reviews |
| Số lượng bản ghi | 50.000 đánh giá phim |
| Phân bố nhãn | 25.000 mẫu tích cực và 25.000 mẫu tiêu cực |
| Số lượng thuộc tính | 2 cột: `review` và `sentiment` |
| Tập huấn luyện | 25.000 mẫu, gồm 12.500 tích cực và 12.500 tiêu cực |
| Tập kiểm tra | 25.000 mẫu, gồm 12.500 tích cực và 12.500 tiêu cực |
| Kiểu dữ liệu | Văn bản và nhãn phân loại nhị phân |

### 2.3. Mô tả các thuộc tính

| STT | Tên thuộc tính | Mô tả | Kiểu dữ liệu | Vai trò |
|:---:|---|---|---|---|
| 1 | `review` | Nội dung đánh giá phim do người dùng viết. Có độ dài thay đổi, có thể chứa thẻ HTML như `<br />`, dấu câu và ký tự đặc biệt. | Chuỗi ký tự | Đặc trưng đầu vào |
| 2 | `sentiment` | Nhãn cảm xúc gồm `positive` (tích cực) và `negative` (tiêu cực) | Phân loại nhị phân | Biến mục tiêu |

### 2.4. Kế hoạch tiền xử lý văn bản

Đồ án sẽ thực hiện các nội dung sau:

- Phân tích độ dài văn bản theo số từ và số ký tự.
- Khảo sát các từ xuất hiện phổ biến theo từng lớp cảm xúc.
- Phân tích độ đa dạng từ vựng và quy luật Zipf.
- Chuẩn hóa chữ thường, thẻ HTML, URL, ký tự đặc biệt và khoảng trắng.
- So sánh các phương pháp tách từ và ảnh hưởng của việc loại bỏ từ dừng.
- So sánh stemming và lemmatization.
- Thử nghiệm Bag of Words, TF-IDF với các n-gram và Word2Vec.
- Phân tích độ thưa, độ tương đồng giữa các văn bản và biểu diễn giảm chiều.
- Khi phù hợp, đánh giá đặc trưng văn bản bằng mô hình phân loại.

Tập kiểm tra sẽ được giữ riêng để đánh giá cuối cùng. Các bước học từ dữ liệu, chẳng hạn như xây dựng từ vựng hoặc khớp vectorizer, sẽ chỉ được thực hiện trên tập huấn luyện.

---

## HƯỚNG DẪN CÀI ĐẶT MÔI TRƯỜNG

### 1. Yêu cầu hệ thống

- Python phiên bản **3.9 trở lên**.
- Công cụ quản lý môi trường và gói phụ thuộc `uv`.
- VS Code cùng các phần mở rộng Python và Jupyter nếu làm việc với notebook.

### 2. Cài đặt môi trường

Mở terminal tại thư mục gốc của dự án. Nếu dự án đã có `pyproject.toml` và `uv.lock`, đồng bộ các gói phụ thuộc bằng lệnh:

```bash
uv sync
```

Kiểm tra phiên bản Python trong môi trường dự án:

```bash
uv run python --version
```

Để chạy các lệnh Python hoặc notebook bằng đúng môi trường dự án, sử dụng `uv run`. Trong VS Code, chọn kernel thuộc môi trường ảo của dự án, thường là `.venv/bin/python` trên Linux.

### 3. Tải tài nguyên NLTK

Một số bước xử lý ngôn ngữ tự nhiên cần các tài nguyên bổ sung của NLTK. Có thể tải các tài nguyên thường dùng bằng lệnh:

```bash
uv run python -c "import nltk; nltk.download('punkt'); nltk.download('stopwords'); nltk.download('wordnet')"
```

Nếu tokenizer đang sử dụng yêu cầu tài nguyên `punkt_tab`, tải bổ sung bằng:

```bash
uv run python -c "import nltk; nltk.download('punkt_tab')"
```

### 4. Tải dữ liệu

Dữ liệu gốc không nên được đưa trực tiếp vào Git nếu dung lượng lớn hoặc điều kiện cấp phép không cho phép. Hãy tải dữ liệu từ các nguồn được liệt kê bên dưới và làm theo hướng dẫn trong notebook để nạp dữ liệu.

Sau khi tải, cần kiểm tra số dòng, tên cột, kiểu dữ liệu, nhãn và giá trị khuyết trước khi bắt đầu phân tích.

---

## BUILD BOOK

Quy trình biên dịch Jupyter Book và kiểm tra nội dung trước khi xuất bản:

1. **Chạy và kiểm tra notebook:** Đảm bảo các notebook trong thư mục `book/` chạy từ đầu đến cuối mà không gặp lỗi runtime.
2. **Build thành website tĩnh (HTML):**

   ```bash
   uv run jupyter-book build book/
   ```

3. **Xem trước trên máy cá nhân:** Mở file `book/_build/html/index.html` bằng trình duyệt để kiểm tra mục lục, bảng, hình vẽ và công thức.
4. **Xuất bản lên GitHub Pages:** Sau khi build thành công và cấu hình nhánh xuất bản phù hợp, chạy:

   ```bash
   uv run ghp-import -n -p -f book/_build/html
   ```

---

## LIÊN KẾT TÀI NGUYÊN NGOÀI

- **Bộ dữ liệu dạng bảng — Adult Census Income:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/2/adult)
- **Bản sao Adult Census Income trên Hugging Face:** [Hugging Face Datasets](https://huggingface.co/datasets/cestwc/census-income)
- **Bộ dữ liệu văn bản — IMDB 50K Movie Reviews:** [Kaggle](https://www.kaggle.com/datasets/atulanandjha/imdb-50k-movie-reviews-test-your-bert)