# Softmax và Stable Softmax

Trong các bài toán học máy, ta thường đo lường khả năng xảy ra một biến cố $x$ bằng cách tính tỷ lệ phần trăm giữa xác suất của $x$ với tổng xác suất của tất cả các biến cố. Ví dụ xác suất lấy được một viên bi đỏ từ hộp 10 viên bi (gồm 5 viên bi xanh và 5 viên bi đỏ) là $\frac{5}{10} \times 100 = 50\%$.

Song có những trường hợp xác suất của $x$ là một số âm. Khi đó việc tính tỷ lệ phần trăm theo cách thông thường sẽ đem lại các kết quả không đúng với thực tế.

Xét ví dụ: Mô hình dự đoán xác suất có mưa ($P_{rain}$), có nắng ($P_{sun}$), có mây ($P_{cloud}$) dựa trên các yếu tố thời tiết. Đầu ra mô hình là một dãy số:

$$z = [2.0 ; -10.0 ; 0.1]$$

Nếu tính xác suất có mưa theo cách tính tỷ lệ phần trăm thông thường thì:

$$P_{rain} = \frac{V_{rain}}{V_{rain} + V_{sun} + V_{cloud}} \times 100 = \frac{2.0}{2.0 - 10.0 + 0.1} \times 100 = -25.32\%$$

Việc tổng xác suất là một số âm khiến kết quả tính tỷ lệ phần trăm không có ý nghĩa.

Để giải quyết vấn đề này, ta sử dụng Softmax - một phép toán giúp chuyển đổi một dãy số thành một phân phối xác xuất. Bằng việc sử dụng lũy thừa của $e$, Softmax đảm bảo tất cả các xác suất đều không âm, giúp thuận tiện cho việc tính tỷ lệ phần trăm.

$$\text{Softmax}(z_i) = \frac{e^{z_i}}{\sum_{j=1}^{K} e^{z_j}}$$

Song khi sử dụng lũy thừa của $e$ lại dễ nảy sinh 2 trường hợp:
- Số mũ quá lớn gây tràn số, Python trả về `inf`.
- Số mũ quá nhỏ (<0) gây thiếu số, Python làm tròn về 0.

Vì vậy, một phiên bản cải tiến hơn của Softmax ra đời, đó là Stable Softmax.

$$\text{Stable Softmax}(z_i) = \frac{e^{z_i - \max(z)}}{\sum_{j=1}^{K} e^{z_j - \max(z)}}$$

Bằng việc thêm - $e^{max(z)}$, Stable Softmax giải quyết đồng thời 3 vấn đề:
- Ở tử, $z_i - {max(z)} <= 0$ =>  ${e^{z_i - \max(z)}} <=1 $, không thể gây tràn số.
- Ở mẫu, tổng sigma luôn tồn lại một phần tử là $e^{z_j - \max(z)} = 1$ khi $z_i = {max}(z)$. Nhờ vậy ${\sum_{j=1}^{K} e^{z_j - \max(z)}} >= 1$, không gây thiếu số dẫn đến phép chia cho 0 sai logic.
- Đồng thời việc cùng thêm - $e^{max(z)}$ ở cả tử và mẫu giúp giá trị này tự triệt tiêu lẫn nhau, ko làm thay đổi bản chất kết quả cuối cùng.
