

# Exploratory Data Analysis and Feature Engineering

Phân tích dữ liệu thăm dò (EDA) và Kỹ thuật đặc trưng (Feature Engineering) là hai giai đoạn cực kỳ quan trọng trong quy trình khoa học dữ liệu. Chúng không chỉ giúp chúng ta hiểu rõ hơn về dữ liệu mà còn chuẩn bị dữ liệu một cách hiệu quả nhất cho các mô hình học máy.

## 1. Exploratory Data Analysis

EDA là quá trình ban đầu trong việc phân tích các tập dữ liệu để tóm tắt các đặc điểm chính của chúng, thường sử dụng các phương pháp trực quan hóa dữ liệu. Mục tiêu chính của EDA là khám phá các mẫu, phát hiện các điểm bất thường, kiểm tra các giả thuyết và kiểm tra các giả định với sự hỗ trợ của các thống kê tóm tắt và biểu diễn đồ họa.

### a. Patterns/Trends/Hypothesis

Trong giai đoạn này, chúng ta tìm kiếm các mối quan hệ tiềm ẩn giữa các biến, các xu hướng theo thời gian (nếu có dữ liệu chuỗi thời gian), hoặc các nhóm dữ liệu có hành vi tương tự.

*   **Mẫu:** Ví dụ, liệu có một tập hợp con khách hàng cụ thể (ví dụ: những người trẻ tuổi, sống ở thành thị) có xu hướng mua một loại sản phẩm nhất định không?
*   **Xu hướng:** Doanh số bán hàng có tăng theo mùa không? Tỷ lệ chấp nhận một dịch vụ có tăng đều qua các năm không?
*   **Giả thuyết:**
    *   Giả thuyết 1: Giá nhà đất có mối tương quan thuận với số phòng ngủ.
    *   Giả thuyết 2: Những khách hàng chi tiêu nhiều hơn có xu hướng ở lại với dịch vụ lâu hơn.
    *   Giả thuyết 3: Các giao dịch gian lận thường có giá trị nhỏ hơn hoặc lớn hơn đáng kể so với các giao dịch hợp lệ.

Để kiểm tra các giả thuyết này, chúng ta sẽ sử dụng các thống kê mô tả và biểu đồ.

### b. Summary Statistics: mean, median, std, min, max

Thống kê tóm tắt cung cấp một cái nhìn tổng quan nhanh chóng về phân phối của từng biến trong tập dữ liệu. Các chỉ số quan trọng bao gồm:

*   **Giá trị Trung bình (Mean - $\mu$):** Tổng của tất cả các giá trị chia cho số lượng các giá trị.
    $\mu = \frac{1}{n} \sum_{i=1}^{n} x_i$
    Đây là một thước đo của xu hướng trung tâm.
*   **Giá trị Trung vị (Median):** Giá trị nằm ở giữa của một tập dữ liệu đã được sắp xếp. Ít bị ảnh hưởng bởi các giá trị ngoại lai hơn giá trị trung bình.
*   **Độ lệch Chuẩn (Standard Deviation - $\sigma$):** Đo lường mức độ phân tán của dữ liệu xung quanh giá trị trung bình.
    $\sigma = \sqrt{\frac{1}{n-1} \sum_{i=1}^{n} (x_i - \mu)^2}$
    Độ lệch chuẩn càng lớn, dữ liệu càng phân tán rộng.
*   **Giá trị Tối thiểu (Min) và Tối đa (Max):** Giá trị nhỏ nhất và lớn nhất trong tập dữ liệu.
*   **Phần tư vị (Quartiles):** Chia dữ liệu thành bốn phần bằng nhau (Q1, Q2 - median, Q3). Khoảng cách giữa Q3 và Q1 được gọi là Khoảng Tứ phân vị (IQR), cung cấp thông tin về sự phân tán của 50% dữ liệu trung tâm.
*   **Chế độ (Mode):** Giá trị xuất hiện thường xuyên nhất trong tập dữ liệu.

Các thư viện như Pandas trong Python cung cấp hàm `.describe()` để dễ dàng tính toán các thống kê này cho tất cả các cột số.

### c. EDA with Visualization

Trực quan hóa dữ liệu là một công cụ mạnh mẽ trong EDA, giúp chúng ta nhìn thấy các mẫu và xu hướng mà các thống kê số có thể bỏ qua.

*   **Visualization libraries: Matplotlib/Pandas/Seaborn**
    *   **Matplotlib:** Thư viện cơ bản và mạnh mẽ để tạo ra các biểu đồ tĩnh, động và tương tác trong Python.
    *   **Pandas:** Tích hợp sẵn các hàm vẽ biểu đồ đơn giản, rất tiện lợi để trực quan hóa Series và DataFrame.
    *   **Seaborn:** Xây dựng trên Matplotlib, cung cấp giao diện cấp cao hơn để tạo các biểu đồ thống kê hấp dẫn và giàu thông tin.

*   **Plot types: scatter/histograms/box plots/pairplot/groupby plots**

    *   **Biểu đồ Phân tán (Scatter Plots):** Dùng để hiển thị mối quan hệ giữa hai biến số. Mỗi điểm trên biểu đồ đại diện cho một quan sát, với vị trí theo trục X và Y tương ứng với giá trị của hai biến. Rất hữu ích để phát hiện các mối tương quan hoặc cụm dữ liệu.
        *   *Ví dụ:* Biểu đồ phân tán giữa "Số giờ học" và "Điểm thi" để xem có mối quan hệ tuyến tính không.
        
    *   **Biểu đồ Tần suất (Histograms):** Trực quan hóa phân phối của một biến số duy nhất. Biểu đồ chia dữ liệu thành các "thùng" (bins) và đếm số lượng quan sát rơi vào mỗi thùng. Giúp xác định hình dạng phân phối (chuẩn, lệch trái, lệch phải), các giá trị phổ biến và các ngoại lai.
        *   *Ví dụ:* Biểu đồ tần suất của "Tuổi" để xem phân bố tuổi của khách hàng.
        
    *   **Biểu đồ Hộp (Box Plots):** Hiển thị tóm tắt năm số (min, Q1, median, Q3, max) và các điểm ngoại lai của một biến số. Rất tốt để so sánh phân phối của một biến số giữa các nhóm khác nhau hoặc để phát hiện ngoại lai.
        *   *Ví dụ:* Biểu đồ hộp của "Thu nhập" theo "Trình độ học vấn" để so sánh phân phối thu nhập giữa các nhóm trình độ khác nhau.
        
    *   **Biểu đồ Cặp (Pair Plots):** (Thường dùng với Seaborn) Tạo ra một ma trận các biểu đồ phân tán cho tất cả các cặp biến số trong tập dữ liệu, cùng với biểu đồ tần suất hoặc biểu đồ mật độ cho từng biến trên đường chéo chính. Cực kỳ hữu ích để có cái nhìn tổng quan nhanh về các mối quan hệ giữa các biến.
        
    *   **Biểu đồ Groupby (Groupby Plots):** Kết hợp các kỹ thuật nhóm dữ liệu (groupby) với các loại biểu đồ khác để trực quan hóa các thống kê tóm tắt của một biến số dựa trên các nhóm của một biến phân loại khác.
        *   *Ví dụ:* Biểu đồ thanh (bar plot) của giá trị trung bình "Doanh số" theo "Khu vực" để so sánh doanh số trung bình giữa các khu vực.

## 2. Feature Engineering

Kỹ thuật đặc trưng là quá trình sử dụng kiến thức về miền dữ liệu để tạo ra các đặc trưng mới hoặc biến đổi các đặc trưng hiện có từ dữ liệu thô, nhằm cải thiện hiệu suất của các mô hình học máy. Đây là một trong những bước quan trọng nhất và thường đòi hỏi sự sáng tạo và hiểu biết sâu sắc về dữ liệu.

### a. Variable transformation: log, polynomial features

Biến đổi biến số nhằm mục đích thay đổi phân phối của dữ liệu để làm cho nó phù hợp hơn với các giả định của mô hình (ví dụ: phân phối chuẩn), giảm thiểu sự ảnh hưởng của các ngoại lai, hoặc làm cho mối quan hệ giữa các biến trở nên tuyến tính hơn.

*   **Log Transformation (Biến đổi Logarit):** Thường được sử dụng cho các biến có phân phối lệch dương (right-skewed) hoặc các biến có phạm vi giá trị rất rộng. Nó giúp nén phạm vi giá trị và làm cho phân phối gần với phân phối chuẩn hơn.
    $x' = \log(x)$ hoặc $x' = \log(x+1)$ (để xử lý các giá trị 0)
    
*   **Polynomial Features (Đặc trưng Đa thức):** Tạo ra các đặc trưng mới bằng cách nâng lũy thừa các đặc trưng hiện có hoặc nhân chúng với nhau. Điều này cho phép mô hình nắm bắt các mối quan hệ phi tuyến tính.
    *   *Ví dụ:* Nếu có đặc trưng $x_1$ và $x_2$, chúng ta có thể tạo ra $x_1^2$, $x_2^2$, $x_1x_2$.
    *   Đối với một đặc trưng $x$, các đặc trưng đa thức bậc $d$ sẽ bao gồm $x, x^2, \ldots, x^d$.
    
*   **Square Root Transformation (Biến đổi Căn bậc hai):** Tương tự như logarit, cũng được dùng cho các dữ liệu lệch dương, nhưng ít mạnh mẽ hơn logarit trong việc nén dữ liệu.
    $x' = \sqrt{x}$
    
*   **Reciprocal Transformation (Biến đổi Nghịch đảo):**
    $x' = 1/x$
    
*   **Box-Cox Transformation:** Là một họ các phép biến đổi năng lượng tham số hóa (power transformations), cho phép dữ liệu được biến đổi để gần với phân phối chuẩn nhất.
    $x' = \frac{x^\lambda - 1}{\lambda}$ nếu $\lambda \ne 0$
    $x' = \log(x)$ nếu $\lambda = 0$
    Trong đó $\lambda$ là một tham số được tối ưu hóa từ dữ liệu.

### b. Feature encoding: binary, one-hot, ordinal

Mã hóa đặc trưng là quá trình chuyển đổi các biến phân loại (categorical variables) thành dạng số, vì hầu hết các thuật toán học máy chỉ làm việc với dữ liệu số.

*   **Binary Encoding (Mã hóa Nhị phân):** Nếu biến phân loại chỉ có hai thể loại (ví dụ: 'Nam', 'Nữ'), chúng ta có thể mã hóa chúng thành 0 và 1.
    
*   **One-Hot Encoding:** Tạo ra các cột nhị phân mới cho mỗi thể loại duy nhất của biến phân loại. Nếu một quan sát thuộc về một thể loại, cột tương ứng sẽ có giá trị 1, các cột khác là 0. Rất phổ biến nhưng có thể dẫn đến "lời nguyền của số chiều" nếu có quá nhiều thể loại.
    *   *Ví dụ:* Biến "Màu sắc" có 'Đỏ', 'Xanh', 'Vàng'. One-Hot Encoding sẽ tạo ra 3 cột: 'Màu_Đỏ', 'Màu_Xanh', 'Màu_Vàng'.
    
*   **Ordinal Encoding (Mã hóa Thứ tự):** Nếu các thể loại của biến phân loại có một thứ tự tự nhiên (ví dụ: 'Thấp', 'Trung bình', 'Cao'), chúng ta có thể gán các giá trị số nguyên có thứ tự cho chúng (ví dụ: 0, 1, 2).
    *   *Lưu ý:* Việc gán thứ tự sai có thể gây hiểu lầm cho mô hình.
    
*   **Target Encoding / Mean Encoding:** Gán cho mỗi thể loại của biến phân loại giá trị trung bình của biến mục tiêu (target variable) tương ứng với thể loại đó. Rất hiệu quả nhưng dễ bị rò rỉ dữ liệu (data leakage) nếu không được thực hiện cẩn thận (ví dụ: sử dụng cross-validation).
    *   *Ví dụ:* Mã hóa 'Thành phố' bằng doanh số trung bình của các giao dịch tại thành phố đó.
    
*   **Hashing Encoding:** Chuyển đổi các thể loại thành các giá trị băm (hash values), sau đó gán chúng vào các cột có số lượng cố định. Giúp giảm số chiều nhưng có thể gây ra xung đột (collision) nếu hai thể loại khác nhau được băm thành cùng một giá trị.

### c. Feature scaling: standard, min-max, robust

Chuẩn hóa đặc trưng là quá trình thay đổi phạm vi của các đặc trưng độc lập (independent features) hoặc các biến dự đoán (predictor variables). Điều này là cần thiết vì nhiều thuật toán học máy (như SVM, K-Nearest Neighbors, Logistic Regression, Neural Networks) nhạy cảm với thang đo của dữ liệu và có thể hoạt động kém hiệu quả nếu các đặc trưng có các phạm vi giá trị khác nhau.

*   **Standardization (Chuẩn hóa Z-score):** Chuyển đổi dữ liệu sao cho nó có giá trị trung bình là 0 và độ lệch chuẩn là 1.
    $x' = \frac{x - \mu}{\sigma}$
    Phù hợp cho các thuật toán giả định phân phối chuẩn hoặc các thuật toán dựa trên khoảng cách. Không làm thay đổi hình dạng của phân phối.
    
*   **Min-Max Scaling (Chuẩn hóa Min-Max):** Chuyển đổi dữ liệu về một phạm vi cố định, thường là từ 0 đến 1.
    $x' = \frac{x - \text{min}(x)}{\text{max}(x) - \text{min}(x)}$
    Thích hợp khi chúng ta cần dữ liệu nằm trong một phạm vi cụ thể và không có các ngoại lai đáng kể. Rất nhạy cảm với ngoại lai.
    
*   **Robust Scaling:** Chuẩn hóa dữ liệu bằng cách sử dụng trung vị (median) và khoảng tứ phân vị (IQR) thay vì trung bình và độ lệch chuẩn. Điều này làm cho nó ít bị ảnh hưởng bởi các ngoại lai hơn.
    $x' = \frac{x - \text{median}(x)}{\text{IQR}(x)}$
    Hữu ích khi tập dữ liệu chứa nhiều ngoại lai.

