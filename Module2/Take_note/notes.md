# Xử lý Dữ liệu cho Học máy

Mọi mô hình học máy đều bắt đầu từ dữ liệu. Chất lượng của mô hình không thể vượt qua chất lượng của "nguyên liệu" đầu vào. Dưới đây là quy trình hai bước cốt lõi để chuẩn bị dữ liệu.

## Giai đoạn 1: Thu thập Dữ liệu - Dữ liệu của bạn ở đâu?

Dữ liệu có thể nằm ở khắp mọi nơi. Việc đầu tiên là đưa chúng về một định dạng chung mà chúng ta có thể làm việc được, đó là **Pandas DataFrame**.

### Kịch bản 1: Dữ liệu nằm trong các tệp tin (CSV, JSON)

Đây là trường hợp phổ biến nhất. Bạn có các tệp tin đơn giản trên máy.

*   **Với tệp CSV:** Đây là "bánh mì và bơ" của khoa học dữ liệu. Lệnh chính là `pd.read_csv()`.
    *   **Mẹo quan trọng:** Hãy để ý đến các tham số như `sep` (nếu tệp không dùng dấu phẩy), `header` (nếu dòng tiêu đề không phải dòng đầu tiên), và `na_values` (để tự động nhận diện các giá trị rỗng như "N/A" hay "-99").

*   **Với tệp JSON:** Phổ biến với dữ liệu từ web và API. Lệnh chính là `pd.read_json()`.
    *   **Mẹo quan trọng:** JSON có nhiều cấu trúc. Tham số `orient` (ví dụ: `orient='records'`) là chìa khóa để `pandas` hiểu đúng cách sắp xếp dữ liệu của bạn.

### Kịch bản 2: Dữ liệu nằm trong cơ sở dữ liệu (SQL, NoSQL)

Khi dữ liệu lớn và có cấu trúc, nó thường được lưu trong CSDL. Quy trình làm việc chung là: **Kết nối -> Truy vấn -> Đóng kết nối**.

*   **Với SQL (dữ liệu quan hệ):** Bạn sẽ viết một câu lệnh `SELECT` để lấy chính xác những gì bạn cần.
    ```python
    # Quy trình 3 bước với SQL
    import sqlite3
    import pandas as pd

    con = sqlite3.connect("database.db") # 1. Kết nối
    data = pd.read_sql("SELECT * FROM users WHERE age > 30", con) # 2. Truy vấn
    con.close() # 3. Đóng kết nối
    ```

*   **Với NoSQL (ví dụ: MongoDB):** Thay vì chuỗi SQL, bạn sẽ dùng các đối tượng (như dictionary) để định nghĩa truy vấn.
    ```python
    # Quy trình tương tự với NoSQL
    from pymongo import MongoClient
    
    client = MongoClient() # 1. Kết nối
    collection = client.database.collection
    cursor = collection.find({'age': {'$gt': 30}}) # 2. Truy vấn
    data = pd.DataFrame(list(cursor)) # Chuyển kết quả sang DataFrame
    client.close() # 3. Đóng kết nối
    ```

---

## Giai đoạn 2: Làm sạch Dữ liệu - "Sửa chữa" Nguyên liệu thô

Dữ liệu thô hiếm khi hoàn hảo. Giai đoạn này quyết định 80% thành công của dự án. Hãy tập trung vào ba vấn đề kinh điển.

### Vấn đề 1: Dữ liệu bị thiếu (Missing Values)

Đây là vấn đề bạn sẽ gặp nhiều nhất. Các mô hình không thể xử lý các ô trống. Bạn có 3 lựa chọn chiến lược:

1.  **Xóa bỏ (Nhanh nhưng mạo hiểm):** Xóa các hàng hoặc cột có chứa giá trị thiếu. Chỉ nên làm điều này nếu lượng dữ liệu thiếu rất nhỏ, nếu không bạn sẽ vứt bỏ đi thông tin quý giá.
2.  **Điền giá trị thay thế (Imputation - Phổ biến nhất):** Dùng một giá trị ước tính để lấp vào chỗ trống.
    *   **Đối với cột số:** Thường dùng giá trị trung bình (`.mean()`) hoặc trung vị (`.median()`). Trung vị thường tốt hơn vì nó ít bị ảnh hưởng bởi các giá trị ngoại lai.
    *   **Đối với cột danh mục:** Dùng giá trị xuất hiện nhiều nhất (`.mode()`).
    ```python
    # Điền giá trị thiếu bằng trung vị (an toàn hơn trung bình)
    df['age'].fillna(df['age'].median(), inplace=True)
    ```
3.  **Xem "Thiếu" là một thông tin:** Đôi khi, việc một giá trị bị thiếu lại là một tín hiệu quan trọng. Trong trường hợp này, bạn có thể tạo một cột mới để đánh dấu các hàng bị thiếu dữ liệu.

### Vấn đề 2: Giá trị ngoại lai (Outliers)

Đây là những giá trị quá khác biệt so với phần còn lại, ví dụ như một giao dịch 10.000.000$ trong khi hầu hết các giao dịch khác dưới 1.000$.

*   **Tác động:** Chúng có thể "kéo" các giá trị thống kê như trung bình và làm sai lệch mô hình, đặc biệt là các mô hình tuyến tính.
*   **Cách phát hiện:** Cách nhanh nhất là dùng **trực quan hóa**. Một biểu đồ hộp (`boxplot`) sẽ ngay lập tức chỉ ra các điểm nằm ngoài "vùng an toàn".
*   **Cách xử lý:**
    *   **Nếu là lỗi nhập liệu:** Hãy sửa hoặc xóa nó.
    *   **Nếu là sự kiện có thật:** Đừng vội xóa! Nó có thể chứa thông tin quan trọng. Cân nhắc các phương pháp:
        *   **Biến đổi dữ liệu:** Áp dụng phép biến đổi logarit (`np.log()`) có thể làm giảm tác động của giá trị ngoại lai.
        *   **Sử dụng các mô hình mạnh mẽ hơn:** Các mô hình dựa trên cây (như Random Forest) ít bị ảnh hưởng bởi giá trị ngoại lai.

### Vấn đề 3: Dữ liệu không nhất quán và Trùng lặp
*   **Không nhất quán:** "USA", "United States", "usa" nên được chuẩn hóa thành một giá trị duy nhất. Các hàm xử lý chuỗi (`.str.lower()`, `.str.strip()`) là bạn đồng hành của bạn.
*   **Trùng lặp:** Dùng `df.drop_duplicates()` để xóa các hàng giống hệt nhau. Nhưng hãy cẩn thận, luôn kiểm tra xem liệu việc trùng lặp đó có hợp lệ trong bối cảnh thực tế hay không trước khi xóa.

### Kết luận
Làm sạch dữ liệu là một quá trình lặp đi lặp lại và đòi hỏi tư duy phản biện. Một bộ dữ liệu được chuẩn bị tốt là nền tảng vững chắc nhất cho một mô hình học máy thành công.