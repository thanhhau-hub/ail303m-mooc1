Chắc chắn rồi, đây là nội dung của tài liệu "ml-data-notes.md" được viết lại dưới dạng Markdown bằng tiếng Việt, giữ nguyên cấu trúc và các đoạn mã.

---

# Nguyên tắc cơ bản về Dữ liệu trong Học máy - Module 2

## Phần 1: Truy xuất Dữ liệu từ Nhiều Nguồn

### 1.1 Tệp CSV (Comma Separated Values - Giá trị được phân tách bằng dấu phẩy)

#### Định nghĩa
Tệp CSV bao gồm các hàng dữ liệu, trong đó các giá trị được phân tách bằng dấu phẩy. Đây là một trong những định dạng phổ biến nhất để lưu trữ dữ liệu dạng bảng.

#### Triển khai cơ bản trong Pandas

**Ví dụ đọc tệp CSV tiêu chuẩn:**
```python
# Bước 1: Import thư viện pandas (thường được viết tắt là 'pd')
import pandas as pd

# Bước 2: Xác định đường dẫn đến tệp
file_path = 'data/iris_data.csv'

# Bước 3: Đọc CSV vào DataFrame
data = pd.read_csv(file_path)

# Bước 4: Xem 5 hàng đầu tiên
print(data.iloc[:5])
```

**Cấu trúc đầu ra:** Một DataFrame với các cột như `sepal_length`, `sepal_width`, `petal_length`, `petal_width`, `species`.

### Các tham số quan trọng của `read_csv()`

#### 1. **Chỉ định Ký tự phân tách (Separator)**
```python
# Đối với tệp được phân tách bằng tab (TSV)
data = pd.read_csv(file_path, sep='\t')

# Đối với tệp được phân tách bằng khoảng trắng với độ dài khác nhau
data = pd.read_csv(file_path, delim_whitespace=True)
```
**Lưu ý:** Các ký tự phân tách khác nhau đòi hỏi các tham số khác nhau. Sử dụng `\t` cho ký tự tab trong Python.

#### 2. **Quản lý Dòng tiêu đề (Header)**
```python
# Bỏ qua các hàng hoặc chỉ định hàng nào chứa tiêu đề
data = pd.read_csv(file_path, header=2)  # Sử dụng hàng thứ 2 làm tiêu đề

# Cung cấp tên cột tùy chỉnh
column_names = ['col1', 'col2', 'col3']
data = pd.read_csv(file_path, names=column_names)
```
**Lưu ý:** Danh sách tên cột phải khớp chính xác với số lượng cột trong DataFrame.

#### 3. **Xử lý Giá trị Null**
```python
# Định nghĩa những giá trị nào nên được coi là null
data = pd.read_csv(file_path, na_values=['NA', '99', 'missing'])
```
**Lưu ý:** Các giá trị lỗi phổ biến hoặc giá trị giữ chỗ (như 99 cho dữ liệu bị thiếu) có thể được tự động chuyển đổi thành null trong quá trình nhập.

---

### 1.2 Tệp JSON (JavaScript Object Notation)

#### Định nghĩa
Định dạng tiêu chuẩn để lưu trữ dữ liệu trên nhiều nền tảng, đặc biệt phổ biến trong:
- Cơ sở dữ liệu NoSQL
- Phản hồi từ API
- Trao đổi dữ liệu đa nền tảng

#### Đặc điểm cấu trúc
- Tương tự như dictionary trong Python
- Các cặp khóa-giá trị (key-value)
- Định dạng có tổ chức và dễ truy cập

**Ví dụ về cấu trúc JSON:**
```json
// Biểu diễn JSON của một hàng dữ liệu
{
    "column_name1": "value1",
    "column_name2": "value2",
    "column_name3": "value3"
}
```

#### Đọc tệp JSON
```python
import pandas as pd

# Đọc JSON cơ bản
data = pd.read_json('data/file.json')

# Nếu gặp sự cố, hãy kiểm tra tham số 'orient'
# Các tùy chọn: 'split', 'records', 'index', 'columns', 'values'
data = pd.read_json('data/file.json', orient='records')
```

**Lưu ý:** Tham số `orient` rất quan trọng khi cấu trúc JSON không khớp với định dạng mong đợi. `orient` xác định **hướng** của dữ liệu JSON khi chuyển đổi thành DataFrame.
*   **`records`** (phổ biến nhất): JSON là một danh sách các dictionary. Mỗi dictionary là một hàng.
*   **`index`**: JSON là một dictionary lồng nhau, trong đó các khóa là chỉ mục (index).
*   **`columns`**: JSON là một dictionary, trong đó các khóa là tên cột.
*   **`split`**: JSON lưu trữ index, columns, và data một cách riêng biệt.
*   **`values`**: JSON chỉ chứa danh sách các giá trị.

#### Ghi tệp JSON```python
# Chuyển đổi DataFrame thành JSON
data.to_json('output_file.json')
```

---

### 1.3 Cơ sở dữ liệu SQL (Structured Query Language)

#### Định nghĩa
Cơ sở dữ liệu quan hệ có cấu trúc cao với schema cố định. Dữ liệu được tổ chức trong các bảng với các mối quan hệ được xác định.

#### Các loại CSDL SQL phổ biến
- Microsoft SQL Server
- PostgreSQL
- MySQL
- AWS Redshift
- Oracle DB

#### Thư viện Python để kết nối SQL
- **sqlite3**: Dành cho cơ sở dữ liệu SQLite
- **SQLAlchemy**: Hoạt động với nhiều loại CSDL SQL
- **psycopg2**: Dành riêng cho PostgreSQL

#### Ví dụ kết nối SQL hoàn chỉnh (SQLite)
```python
# Bước 1: Import các thư viện cần thiết
import sqlite3 as sq3
import pandas as pd

# Bước 2: Xác định đường dẫn đến cơ sở dữ liệu
path = 'data/classic_rock.db'

# Bước 3: Thiết lập kết nối
con = sq3.connect(path)

# Bước 4: Viết câu truy vấn SQL dưới dạng chuỗi
query = "SELECT * FROM rock_songs"

# Bước 5: Thực thi truy vấn và tạo DataFrame
data = pd.read_sql(query, con)

# Bước 6: Đừng quên đóng kết nối khi hoàn tất
con.close()
```
**Lưu ý:**
1.  Đối tượng kết nối (`con`) duy trì liên kết đến cơ sở dữ liệu.
2.  Câu truy vấn SQL được viết dưới dạng chuỗi trong Python.
3.  `pd.read_sql()` tự động chuyển đổi kết quả truy vấn thành DataFrame.
4.  Luôn đóng kết nối để tránh rò rỉ tài nguyên.

---

### 1.4 Cơ sở dữ liệu NoSQL

#### Định nghĩa
Cơ sở dữ liệu phi quan hệ với cấu trúc linh hoạt. Có lợi thế về hiệu suất và chi phí so với SQL trong một số ứng dụng nhất định.

#### Các loại CSDL NoSQL
1.  **Cơ sở dữ liệu Tài liệu (Document Databases):** Mỗi tài liệu là một quan sát, được lưu trữ dưới dạng giống JSON.
2.  **Kho lưu trữ Khóa-Giá trị (Key-Value Stores):** Một khóa chính (như ID) ánh xạ tới các giá trị.
3.  **Cơ sở dữ liệu Đồ thị (Graph Databases):** Tối ưu hóa cho việc quản lý các mối quan hệ (ví dụ: kết nối bạn bè trên mạng xã hội).
4.  **Họ Cột Rộng (Wide Column Families):** Các cột được nhóm lại thành các "họ" (families).

#### Ví dụ về MongoDB (CSDL NoSQL phổ biến)
```python
# Bước 1: Import và thiết lập kết nối
from pymongo import MongoClient

# Tạo kết nối (có thể cần username/password)
con = MongoClient()

# Bước 2: Liệt kê các cơ sở dữ liệu có sẵn
print(con.list_database_names())

# Bước 3: Chọn một cơ sở dữ liệu cụ thể
db = con.database_name

# Bước 4: Truy vấn dữ liệu từ một collection (tương tự bảng SQL)
cursor = db.collection_name.find({})  # {} chọn tất cả tài liệu

# Bước 5: Chuyển đổi thành DataFrame của Pandas
# Cursor là một đối tượng generator chứa các tài liệu JSON
df = pd.DataFrame(list(cursor))
```

---

### 1.5 API và Truy cập Dữ liệu Đám mây

#### Trường hợp sử dụng
- Dữ liệu mạng xã hội (tweet trên Twitter)
- Dữ liệu marketing (Amazon)
- Các bộ dữ liệu công khai (Thư viện Machine Learning của UC Irvine)

#### Ví dụ truy cập dữ liệu trực tiếp từ URL
```python
import pandas as pd

# Xác định URL đến nguồn dữ liệu
data_url = "https://archive.ics.uci.edu/ml/datasets/dataset.csv"

# Đọc trực tiếp từ URL (giống như tệp cục bộ)
df = pd.read_csv(data_url)
```
**Lưu ý:** `pd.read_csv()` có thể đọc trực tiếp từ các URL.

---

## Phần 2: Làm sạch Dữ liệu

### Tại sao làm sạch dữ liệu lại quan trọng?

#### Nguyên tắc "Rác đầu vào, Rác đầu ra" (Garbage In, Garbage Out)
Chất lượng của mô hình chỉ có thể tốt bằng chất lượng của dữ liệu được dùng để huấn luyện nó. Dữ liệu kém chất lượng dẫn đến kết quả không đáng tin cậy.

### 2.1 Các vấn đề phổ biến về chất lượng dữ liệu

1.  **Thiếu dữ liệu (Lack of Data):** Không đủ dữ liệu liên quan để huấn luyện.
2.  **Quá nhiều dữ liệu (Too Much Data):** Dữ liệu phân tán ở nhiều nơi, cần được tổ chức và hợp nhất.
3.  **Dữ liệu kém chất lượng (Bad Data Types):**
    *   **Dữ liệu trùng lặp (Duplicate Data):** Tạo ra trọng số không cần thiết cho một số mẫu nhất định.
    *   **Văn bản không nhất quán và lỗi chính tả (Inconsistent Text):** Khoảng trắng thừa, viết hoa/viết thường khác nhau ("New York", "new york").
    *   **Dữ liệu bị thiếu (Missing Data):** Quá nhiều dữ liệu thiếu có thể làm cho một đặc trưng trở nên vô dụng.
    *   **Giá trị ngoại lai (Outliers):** Các giá trị cực đoan làm sai lệch các đặc trưng và khiến các mẫu thật khó bị phát hiện.
    *   **Vấn đề về nguồn dữ liệu (Data Sourcing Issues):** Dữ liệu từ các hệ thống khác nhau có định dạng không khớp.

### 2.2 Xử lý Dữ liệu trùng lặp

1.  **Phân tích:** Xác định xem các bản sao có hợp lệ hay không (ví dụ: hai bông hoa có cùng số đo là hợp lệ, nhưng cùng một hình ảnh xuất hiện hai lần thì không).
2.  **Thực hành tốt nhất:**
    *   Luôn kiểm tra các đặc trưng trước khi lọc.
    *   Giữ lại quyền truy cập vào dữ liệu gốc.
    *   Không lọc quá mức để tránh mất thông tin quan trọng.

### 2.3 Xử lý Dữ liệu bị thiếu

**Vấn đề cốt lõi:** Các mô hình không thể chấp nhận các giá trị trống vì chúng không chứa thông tin.

#### Chiến lược 1: Xóa dữ liệu
- **Ưu điểm:** Nhanh chóng, đơn giản.
- **Nhược điểm:** Có thể mất quá nhiều thông tin, gây thiên vị cho bộ dữ liệu.

#### Chiến lược 2: Gán giá trị thay thế (Impute)
```python
# Thay thế bằng giá trị trung bình (mean)
df['column'].fillna(df['column'].mean(), inplace=True)

# Thay thế bằng giá trị trung vị (median)
df['column'].fillna(df['column'].median(), inplace=True)```
- **Ưu điểm:** Giữ lại tất cả các hàng và cột, bảo toàn kích thước bộ dữ liệu.
- **Nhược điểm:** Thêm sự không chắc chắn vào mô hình vì các giá trị là ước tính, không phải thực tế.

#### Chiến lược 3: Đánh dấu (Mask)
Tạo ra một danh mục riêng cho các giá trị bị thiếu.
- **Khi nào hữu ích:** Khi bản thân sự thiếu hụt dữ liệu mang thông tin (ví dụ: khách hàng cúp máy ở câu hỏi cuối cùng của khảo sát).
- **Ưu điểm:** Không mất dữ liệu, nắm bắt được mẫu trong sự thiếu hụt.
- **Nhược điểm:** Thêm độ phức tạp cho mô hình.

---

### 2.4 Phát hiện và Xử lý Giá trị ngoại lai (Outlier)

#### Định nghĩa
Các quan sát khác biệt rõ rệt so với hầu hết các điểm dữ liệu khác.

#### Tác động
Một giá trị ngoại lai có thể làm sai lệch nghiêm trọng các thống kê như giá trị trung bình, dẫn đến các dự đoán sai lầm.
**Lưu ý:** Một số giá trị ngoại lai lại chứa thông tin quan trọng (ví dụ: một tuần có doanh số đột biến có thể tiết lộ một chiến lược marketing hiệu quả).

#### Phương pháp phát hiện

1.  **Phương pháp trực quan:**
    *   **Biểu đồ tần suất (Histogram):** `sns.distplot(data)`
    *   **Biểu đồ hộp (Box Plot):** `sns.boxplot(data)`

2.  **Phương pháp toán học (Quy tắc IQR):**
    ```python
    import numpy as np

    # Tính các tứ phân vị
    q25 = np.percentile(data['column'], 25)
    q75 = np.percentile(data['column'], 75)

    # Tính khoảng liên tứ phân vị (IQR)
    iqr = q75 - q25

    # Xác định ngưỡng ngoại lai
    min_val = q25 - (1.5 * iqr)
    max_val = q75 + (1.5 * iqr)

    # Tìm các giá trị ngoại lai
    outliers = [x for x in data['column'] if x > max_val or x < min_val]
    ```

3.  **Phát hiện dựa trên Phần dư (Residual):**
    *   **Phần dư được chuẩn hóa (Standardized Residuals):** Chuẩn hóa phần dư để so sánh trên các thang đo khác nhau.
    *   **Phần dư Studentized (Studentized Residuals):** Phương pháp tinh vi nhất, xem xét ảnh hưởng của từng quan sát lên mô hình.

#### Chiến lược xử lý Giá trị ngoại lai

1.  **Xóa bỏ:** Loại bỏ hoàn toàn ảnh hưởng nhưng làm mất dữ liệu.
2.  **Thay thế bằng giá trị khác:** Giữ lại hàng nhưng mất đi giá trị gốc.
3.  **Biến đổi cột:** Sử dụng các phép biến đổi (ví dụ: logarit) để giảm tác động của giá trị ngoại lai.
    ```python
    df['column_log'] = np.log(df['column'])
    ```
4.  **Dự đoán giá trị:** Sử dụng các quan sát tương tự hoặc một mô hình khác để dự đoán giá trị thay thế.
5.  **Giữ lại giá trị ngoại lai:** Giữ lại tất cả thông tin thực tế nhưng yêu cầu sử dụng các mô hình có khả năng chống lại giá trị ngoại lai.

---

## Những điểm chính cần nhớ

### Truy xuất dữ liệu
1.  Các nguồn dữ liệu khác nhau đòi hỏi các phương pháp và thư viện khác nhau.
2.  Hiểu cấu trúc dữ liệu là chìa khóa để nhập dữ liệu thành công.
3.  Luôn quản lý kết nối đúng cách (đặc biệt là với cơ sở dữ liệu).

### Làm sạch dữ liệu
1.  Dữ liệu sạch là nền tảng của ML thành công - "Rác đầu vào, Rác đầu ra".
2.  Không có giải pháp chung cho mọi vấn đề; quyết định phụ thuộc vào bối cảnh.
3.  Ghi lại các quyết định làm sạch để đảm bảo khả năng tái lập.
4.  Luôn bảo tồn dữ liệu gốc khi có thể.