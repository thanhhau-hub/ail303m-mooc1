# Tổng hợp Thống kê Ứng dụng trong Học máy

## 1. Ước lượng và Suy luận: 

*   **Ước lượng (Estimation):** Là việc tính toán một giá trị duy nhất để đại diện cho một đặc tính nào đó của dữ liệu.
    *   **Ví dụ:** Tính toán doanh thu trung bình của khách hàng là 150$. Đây là một **ước lượng điểm** (point estimate). Nó cung cấp một con số cụ thể nhưng không cho biết độ chắc chắn của con số đó.

*   **Suy luận Thống kê (Statistical Inference):** Là quá trình sử dụng dữ liệu mẫu để đưa ra kết luận về một tổng thể lớn hơn, bao gồm cả việc đánh giá độ không chắc chắn.
    *   **Ví dụ:** "Chúng tôi tin chắc 95% rằng doanh thu trung bình thực tế của toàn bộ khách hàng nằm trong khoảng từ 140$ đến 160$."
    *   Suy luận cung cấp một **khoảng tin cậy**, cho chúng ta biết ước lượng của mình đáng tin cậy đến mức nào. Một khoảng tin cậy hẹp cho thấy sự chắc chắn cao.

## 2. Mô hình Tham số và Phi tham số: 

*   **Mô hình Tham số (Parametric):** Giả định rằng dữ liệu của bạn tuân theo một phân phối toán học cụ thể (như phân phối chuẩn). Mô hình được định nghĩa hoàn toàn bởi một số lượng tham số cố định (ví dụ: trung bình và độ lệch chuẩn).
    *   **Ưu điểm:** Nhanh, hiệu quả khi giả định đúng.
    *   **Nhược điểm:** Kém linh hoạt, có thể cho kết quả sai nếu giả định về phân phối không chính xác.
    *   **Ví dụ:** Hồi quy tuyến tính.

*   **Mô hình Phi tham số (Non-parametric):** Không đưa ra giả định chặt chẽ về phân phối của dữ liệu. Mô hình học trực tiếp từ cấu trúc của dữ liệu.
    *   **Ưu điểm:** Rất linh hoạt, có thể nắm bắt các mối quan hệ phức tạp.
    *   **Nhược điểm:** Cần nhiều dữ liệu hơn, dễ bị quá khớp (overfitting).
    *   **Ví dụ:** Cây quyết định, K-lân cận gần nhất.

## 3. Các Phân phối Dữ liệu Phổ biến

Dữ liệu thường có những "hình dạng" đặc trưng. Việc nhận biết chúng giúp chọn đúng công cụ phân tích.

*   **Phân phối Chuẩn (Normal):** Hình chuông, đối xứng. Nhiều hiện tượng tự nhiên tuân theo quy luật này (ví dụ: chiều cao, huyết áp).
*   **Phân phối Log-chuẩn (Log-normal):** Lệch phải, thường gặp ở các đại lượng không thể âm và có thể có giá trị rất lớn (ví dụ: thu nhập, giá cổ phiếu).
*   **Phân phối Poisson:** Dùng để đếm số lần một sự kiện xảy ra trong một khoảng thời gian/không gian (ví dụ: số cuộc gọi đến tổng đài trong một giờ).
*   **Phân phối Mũ (Exponential):** Mô hình hóa thời gian chờ cho đến khi một sự kiện xảy ra (ví dụ: thời gian cho đến khi một bóng đèn bị hỏng).

## 4. Frequentist và Bayesian

*   **Frequentist:** Đây là cách tiếp cận thống kê truyền thống. Nó coi các tham số của tổng thể là các hằng số chưa biết. Mọi kết luận chỉ được rút ra từ dữ liệu đã quan sát.
*   **Bayesian:** Cách tiếp cận này linh hoạt hơn. Nó coi các tham số cũng có phân phối xác suất. Ta bắt đầu với một "niềm tin ban đầu" (prior), sau đó dùng dữ liệu để cập nhật niềm tin đó và đưa ra một "phân phối sau cùng" (posterior).
    *   **Quy trình:** `Niềm tin ban đầu` + `Bằng chứng từ dữ liệu` → `Kết luận được cập nhật`

## 5. Kiểm định Giả thuyết: Quy trình Ra quyết định Dựa trên Dữ liệu

Đây là một quy trình có cấu trúc để trả lời các câu hỏi dựa trên bằng chứng từ dữ liệu.

1.  **Phát biểu Giả thuyết:**
    *   **Giả thuyết không (H₀):** Giả định mặc định, thường là "không có hiệu ứng" hoặc "không có sự khác biệt". (Ví dụ: Thay đổi giao diện website không ảnh hưởng đến lượng truy cập).
    *   **Giả thuyết đối (H₁):** Điều chúng ta muốn chứng minh. (Ví dụ: Thay đổi giao diện website có ảnh hưởng đến lượng truy cập).

2.  **Thu thập Bằng chứng:**
    *   **Giá trị P (p-value):** Là xác suất quan sát được kết quả hiện tại (hoặc cực đoan hơn), nếu giả thuyết H₀ là đúng.
        *   **Diễn giải đơn giản:** P-value càng nhỏ, bằng chứng chống lại H₀ càng mạnh. Nó cho thấy kết quả của chúng ta khó có thể xảy ra do ngẫu nhiên.

3.  **Ra Quyết định:**
    *   Chúng ta so sánh p-value với một **mức ý nghĩa (α)** được xác định trước (thường là 0.05).
    *   Nếu `p-value < α`: Chúng ta bác bỏ H₀. Có đủ bằng chứng để tin vào H₁.
    *   Nếu `p-value ≥ α`: Chúng ta không đủ bằng chứng để bác bỏ H₀.

### Các loại Lỗi trong Kiểm định
*   **Lỗi Loại I:** Bác bỏ H₀ trong khi nó thực sự đúng (báo động nhầm). Xác suất mắc lỗi này chính là **α**.
*   **Lỗi Loại II:** Không bác bỏ H₀ trong khi nó thực sự sai (bỏ sót một phát hiện quan trọng).

**Lưu ý về Kiểm định Bội:** Khi thực hiện nhiều kiểm định cùng lúc, khả năng bạn gặp phải ít nhất một Lỗi Loại I (kết quả dương tính giả) sẽ tăng lên đáng kể. Các phương pháp như **hiệu chỉnh Bonferroni** được dùng để kiểm soát vấn đề này bằng cách làm cho ngưỡng α trở nên nghiêm ngặt hơn.

## 6. Tương quan và Nhân quả:

Đây là sự khác biệt quan trọng nhất cần nắm vững.

*   **Tương quan (Correlation):** Là khi hai biến có xu hướng di chuyển cùng nhau. Tương quan rất hữu ích cho việc **dự đoán**.
    *   *Ví dụ:* Doanh số bán kem và số vụ chết đuối đều tăng vào mùa hè. Chúng có tương quan dương mạnh.

*   **Nhân quả (Causation):** Là khi sự thay đổi của một biến **trực tiếp gây ra** sự thay đổi của biến kia. Nhân quả là nền tảng cho việc **can thiệp và ra quyết định**.

**Tại sao tương quan không đồng nghĩa với nhân quả?**
Khi A và B tương quan, có thể là do:
1.  **A gây ra B:** (Nhân quả thật).
2.  **B gây ra A:** (Nhân quả ngược).
3.  **Một yếu tố C (biến nhiễu) gây ra cả A và B:** Trong ví dụ trên, *nhiệt độ cao (C)* là nguyên nhân gây ra cả việc người ta ăn kem nhiều hơn (A) và đi bơi nhiều hơn, dẫn đến nhiều vụ đuối nước hơn (B).
4.  **Trùng hợp ngẫu nhiên:** (Tương quan giả).
