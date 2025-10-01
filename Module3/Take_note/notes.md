# Module 3: Quy Trình Làm Việc Tinh Gọn với Dữ Liệu

Mục tiêu của module này là cung cấp một quy trình 3 bước nhanh gọn để xử lý dữ liệu, từ khám phá ban đầu đến chuẩn bị cho mô hình.

## Bước 1: Khám Phá Tổng Quan (Cái nhìn toàn cảnh)

**Mục tiêu:** Nhanh chóng hiểu được cấu trúc, phân phối và các mối quan hệ chính trong dữ liệu của bạn.

**Công cụ chính:** `seaborn.pairplot`. Đây là công cụ hiệu quả nhất để xem mọi thứ cùng một lúc. Chỉ với một dòng lệnh, nó sẽ cho bạn thấy:
*   Mối quan hệ giữa từng cặp biến (biểu đồ phân tán).
*   Sự phân phối của từng biến riêng lẻ (biểu đồ tần suất).

```python
import seaborn as sns

# Nhanh chóng vẽ biểu đồ cho mọi cặp biến, tô màu theo 'species'
sns.pairplot(data, hue='species', height=3)
```**Kết quả**: ![Demo Image](./output_sns_pair.png)

➡️ **Hành động:** Nhìn vào biểu đồ này để tìm ra những mối tương quan rõ rệt hoặc những phân phối bất thường cần được điều tra thêm.

## Bước 2: Trực Quan Hóa Chi Tiết (Khi cần làm rõ một điểm)

**Mục tiêu:** Sau khi phát hiện một điểm thú vị từ Bước 1, hãy tạo một biểu đồ rõ ràng, có chú thích đầy đủ để phân tích sâu hơn hoặc để trình bày cho người khác.

**Công cụ chính:** `matplotlib` với cú pháp `fig, ax`. Cách này cho phép bạn kiểm soát tuyệt đối mọi chi tiết của biểu đồ.

```python
# Cú pháp fig, ax cho phép tùy chỉnh sâu
fig, ax = plt.subplots()

# Vẽ và tùy chỉnh một biểu đồ cụ thể
ax.barh(np.arange(10), data['sepal_width'].iloc[:10])
ax.set(xlabel='Nhãn X', ylabel='Nhãn Y', title='Tiêu đề Biểu đồ')
```
**Kết quả**: ![Demo Image](./output_custom.png)

➡️ **Hành động:** Sử dụng kỹ thuật này để tạo ra các biểu đồ "chất lượng cao" nhằm chứng minh một luận điểm hoặc phân tích một khía cạnh cụ thể của dữ liệu.

## Bước 3: Chế Tác & Chuẩn Hóa (Sẵn sàng cho mô hình)

**Mục tiêu:** Biến đổi tất cả các cột dữ liệu thành định dạng số mà mô hình máy học có thể "hiểu" được.

### **Quy tắc vàng:**

*   **Dữ liệu dạng chữ (Categorical):**
    *   Nếu không có thứ tự (VD: Tên thành phố) → Dùng `pd.get_dummies()` (One-Hot Encode).
    *   Nếu có thứ tự (VD: Tốt, Trung bình, Kém) → Chuyển thành số (VD: 2, 1, 0).

*   **Dữ liệu dạng số (Numerical):**
    *   Nếu các cột có thang đo khác nhau (VD: tuổi và lương) → **BẮT BUỘC** phải co giãn (scale). `StandardScaler` là lựa chọn an toàn nhất.
    *   Nếu dữ liệu bị lệch nhiều → Cân nhắc dùng phép biến đổi logarit `np.log1p()`.

### **Kiểm tra cuối cùng:**

Sau khi biến đổi, hãy kiểm tra xem phân phối của dữ liệu trông như thế nào giữa các nhóm khác nhau. `FacetGrid` của Seaborn rất hữu ích cho việc này.

```python
# Tạo lưới biểu đồ để so sánh phân phối của 'sepal_width' trên mỗi 'species'
g = sns.FacetGrid(data, col='species')
g.map(plt.hist, 'sepal_width')
```![Demo Image](./output_sns_facet1.png)

➡️ **Hành động:** Áp dụng các quy tắc trên để làm sạch và chuẩn hóa dữ liệu. Sử dụng `FacetGrid` để đảm bảo các phép biến đổi của bạn hợp lý trên toàn bộ tập dữ liệu.Chắc chắn rồi! Dưới đây là phiên bản tóm lược tinh gọn của Module 3, tập trung vào quy trình làm việc cốt lõi và chỉ giải thích sơ qua các khái niệm.

***

# Module 3: Quy Trình Làm Việc Tinh Gọn với Dữ Liệu

Mục tiêu của module này là cung cấp một quy trình 3 bước nhanh gọn để xử lý dữ liệu, từ khám phá ban đầu đến chuẩn bị cho mô hình.

## Bước 1: Khám Phá Tổng Quan (Cái nhìn toàn cảnh)

**Mục tiêu:** Nhanh chóng hiểu được cấu trúc, phân phối và các mối quan hệ chính trong dữ liệu của bạn.

**Công cụ chính:** `seaborn.pairplot`. Đây là công cụ hiệu quả nhất để xem mọi thứ cùng một lúc. Chỉ với một dòng lệnh, nó sẽ cho bạn thấy:
*   Mối quan hệ giữa từng cặp biến (biểu đồ phân tán).
*   Sự phân phối của từng biến riêng lẻ (biểu đồ tần suất).

```python
import seaborn as sns

# Nhanh chóng vẽ biểu đồ cho mọi cặp biến, tô màu theo 'species'
sns.pairplot(data, hue='species', height=3)
```**Kết quả**: ![Demo Image](./output_sns_pair.png)


## Bước 2: Trực Quan Hóa Chi Tiết (Khi cần làm rõ một điểm)

**Mục tiêu:** Sau khi phát hiện một điểm thú vị từ Bước 1, hãy tạo một biểu đồ rõ ràng, có chú thích đầy đủ để phân tích sâu hơn hoặc để trình bày cho người khác.

**Công cụ chính:** `matplotlib` với cú pháp `fig, ax`. Cách này cho phép bạn kiểm soát tuyệt đối mọi chi tiết của biểu đồ.

```python
# Cú pháp fig, ax cho phép tùy chỉnh sâu
fig, ax = plt.subplots()

# Vẽ và tùy chỉnh một biểu đồ cụ thể
ax.barh(np.arange(10), data['sepal_width'].iloc[:10])
ax.set(xlabel='Nhãn X', ylabel='Nhãn Y', title='Tiêu đề Biểu đồ')
```
**Kết quả**: ![Demo Image](./output_custom.png)

➡️ **Hành động:** Sử dụng kỹ thuật này để tạo ra các biểu đồ "chất lượng cao" nhằm chứng minh một luận điểm hoặc phân tích một khía cạnh cụ thể của dữ liệu.

## Bước 3: Chế Tác & Chuẩn Hóa (Sẵn sàng cho mô hình)

**Mục tiêu:** Biến đổi tất cả các cột dữ liệu thành định dạng số mà mô hình máy học có thể "hiểu" được.

### **Quy tắc vàng:**

*   **Dữ liệu dạng chữ (Categorical):**
    *   Nếu không có thứ tự (VD: Tên thành phố) → Dùng `pd.get_dummies()` (One-Hot Encode).
    *   Nếu có thứ tự (VD: Tốt, Trung bình, Kém) → Chuyển thành số (VD: 2, 1, 0).

*   **Dữ liệu dạng số (Numerical):**
    *   Nếu các cột có thang đo khác nhau (VD: tuổi và lương) → **BẮT BUỘC** phải co giãn (scale). `StandardScaler` là lựa chọn an toàn nhất.
    *   Nếu dữ liệu bị lệch nhiều → Cân nhắc dùng phép biến đổi logarit `np.log1p()`.

### **Kiểm tra cuối cùng:**

Sau khi biến đổi, hãy kiểm tra xem phân phối của dữ liệu trông như thế nào giữa các nhóm khác nhau. `FacetGrid` của Seaborn rất hữu ích cho việc này.

```python
# Tạo lưới biểu đồ để so sánh phân phối của 'sepal_width' trên mỗi 'species'
g = sns.FacetGrid(data, col='species')
g.map(plt.hist, 'sepal_width')
```![Demo Image](./output_sns_facet1.png)
