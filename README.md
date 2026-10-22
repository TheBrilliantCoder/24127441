# THÔNG TIN ĐỒ ÁN

*Họ tên: Võ Duy Lộc*  
*MSSV: 24127441*

## MÔ TẢ TẬP DỮ LIỆU

### TẬP DỮ LIỆU DẠNG BẢNG

* **Context:**
  Phát hiện gian lận thẻ tín dụng (Credit Card Fraud Detection). Bộ dữ liệu ghi nhận các giao dịch qua thẻ tín dụng của các chủ thẻ người châu Âu vào tháng 09/2013. Bài toán tập trung vào việc xử lý dữ liệu mất cân bằng cực cao (Highly Imbalanced Data) giữa giao dịch hợp lệ và giao dịch gian lận, phát hiện ngoại lai, chuẩn hóa các đặc trưng số và xây dựng mô hình phân loại giảm thiểu rủi ro tài chính.

* **Dataset metadata:**
  * **Số lượng bản ghi (Rows):** 284.807 giao dịch (trong đó có 492 giao dịch gian lận, chiếm tỉ lệ khoảng 0.172%).
  * **Số lượng thuộc tính (Columns):** 31 cột (gồm 30 biến số đầu vào và 1 nhãn mục tiêu).
  * **Phân chia dữ liệu:** Dữ liệu được chia theo tỉ lệ 80% Training set (khoảng 227.845 dòng) và 20% Test set (khoảng 56.962 dòng), bắt buộc áp dụng **Stratified Sampling** theo nhãn `Class` để bảo toàn tỉ lệ giao dịch gian lận giữa các tập.

* **Bảng mô tả chi tiết các thuộc tính:**

  | STT | Tên thuộc tính | Mô tả & Miền giá trị | Kiểu dữ liệu | Vai trò / Ghi chú |
  | :---: | :--- | :--- | :--- | :--- |
  | **1** | `Time` | Số giây trôi qua giữa giao dịch hiện tại và giao dịch đầu tiên trong tập dữ liệu ($0 \to 172.792$) | Số thực liên tục (Continuous Float) | Đặc trưng thời gian giao dịch |
  | **2 - 29** | `V1` đến `V28` | Các thành phần chính thu được sau biến đổi PCA nhằm bảo mật dữ liệu nhạy cảm của khách hàng | Số thực liên tục (Continuous Float) | Đặc trưng ẩn sau phép giảm chiều |
  | **30** | `Amount` | Giá trị tiền của giao dịch tính theo ngoại tệ ($0 \to 25.691,16$) | Số thực liên tục (Continuous Float) | Chi phí giao dịch; có độ lệch phân phối cao |
  | **31** | `Class` | Nhãn phản ánh tính hợp lệ của giao dịch (`0`: Giao dịch bình thường, `1`: Gian lận) | Số nguyên nhị phân (Binary Integer) | **Biến mục tiêu (Target)**; mất cân bằng cực đoan |

*(Ghi chú: Theo yêu cầu đề bài về tỉ lệ khuyết thiếu tối thiểu 5% trên ít nhất một thuộc tính, một cơ chế khuyết ngẫu nhiên hoàn toàn MCAR sẽ được thiết lập nhân tạo trên thuộc tính `Amount` để thực hiện đánh giá các phương pháp điền khuyết).*

---

### TẬP DỮ LIỆU TEXT

* **Context:**
  Phân tích cảm xúc văn bản (Sentiment Analysis) trên tập đánh giá phim IMDB (Large Movie Review Dataset). Bài toán hướng tới việc tiền xử lý văn bản tự nhiên, loại bỏ nhiễu và vector hóa để phân loại sắc thái cảm xúc tích cực hoặc tiêu cực của người xem.

* **Dataset metadata:**
  * **Số lượng bản ghi (Rows):** 50.000 đánh giá phim phân cực mạnh (25.000 mẫu positive và 25.000 mẫu negative).
  * **Số lượng thuộc tính (Columns):** 2 cột (`review` và `sentiment`).
  * **Phân chia dữ liệu:** Phân tách sẵn thành tập Training set (25.000 dòng gồm 12.500 pos, 12.500 neg) và Test set (25.000 dòng gồm 12.500 pos, 12.500 neg).

* **Bảng mô tả chi tiết các thuộc tính:**

| STT | Tên thuộc tính | Mô tả & Miền giá trị | Kiểu dữ liệu | Vai trò / Ghi chú |
| --- | --- | --- | --- | --- |
| **1** | `review` | Nội dung đánh giá phim do người dùng viết; độ dài biến thiên, chứa văn bản tự nhiên kèm các thẻ HTML (`<br />`), ký tự đặc biệt và dấu câu cảm thán. | Chuỗi ký tự (Text / String) | Đặc trưng đầu vào (Input Text Features) |
| **2** | `sentiment` | Nhãn cảm xúc của bài đánh giá, gồm 2 giá trị phân cực đối xứng: `positive` (tích cực) và `negative` (tiêu cực). | Phân loại nhị phân (Binary Categorical / Label) | **Biến mục tiêu (Target Label)** |

---

## HƯỚNG DẪN CÀI ĐẶT MÔI TRƯỜNG

1. **Yêu cầu hệ thống:** Python phiên bản `3.9` trở lên.

2. **Khởi tạo và kích hoạt môi trường ảo:**
   ```bash
   # Tạo môi trường ảo
   python -m venv venv

   # Kích hoạt môi trường (trên Linux/macOS)
   source venv/bin/activate

   # Kích hoạt môi trường (trên Windows PowerShell)
   .\venv\Scripts\Activate.ps1
   ```

3. **Cài đặt các gói thư viện cần thiết:**
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. **Tải tài nguyên bổ sung cho xử lý ngôn ngữ tự nhiên (NLTK):**
   ```bash
   python -c "import nltk; nltk.download('punkt'); nltk.download('stopwords'); nltk.download('wordnet')"
   ```

---

## BUILD BOOK

Quy trình biên dịch cuốn Jupyter Book và kiểm tra trước khi xuất bản:

1. **Chạy và kiểm tra nội dung:**  
   Đảm bảo toàn bộ các file notebook trong thư mục `book/` đã được chạy sạch từ đầu đến cuối và lưu lại outputs mà không gặp lỗi runtime.

2. **Build sách sang dạng website tĩnh (HTML):**
   ```bash
   jupyter-book build book/
   ```

3. **Xem trước trên máy cá nhân:**  
   Mở file HTML vừa tạo tại đường dẫn `book/_build/html/index.html` bằng trình duyệt để kiểm tra mục lục, định dạng bảng biểu, hình vẽ và công thức toán.

4. **Xuất bản lên GitHub Pages:**
   ```bash
   ghp-import -n -p -f book/_build/html
   ```

---

## LINK TÀI NGUYÊN NGOÀI

* [Bộ dữ liệu bảng: Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
* [Bộ dữ liệu text: IMDB 50K Movie Reviews](https://www.kaggle.com/datasets/atulanandjha/imdb-50k-movie-reviews-test-your-bert)
