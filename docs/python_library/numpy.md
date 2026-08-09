# Tổng hợp Kiến thức về NumPy


## 1. Giới thiệu về NumPy

- NumPy là thư viện nền tảng cho tính toán số trong Python và là điểm khởi đầu cho hầu hết các thư viện học máy.

- NumPy xử lý dữ liệu nhanh hơn nhiều lần so với danh sách (list) thuần túy của Python (có thể nhanh hơn tới 50 lần) do lưu trữ dữ liệu trong các khối bộ nhớ liên tục.

- Đối tượng trung tâm của NumPy là mảng nhiều chiều ndarray. Các thuộc tính quan trọng bao gồm:
    
    - `shape`: Kích thước theo từng chiều.
    
    - `ndim`: Số chiều của mảng.
    
    - `size`: Tổng số phần tử.
    
    - `dtype`: Kiểu dữ liệu của các phần tử (mọi phần tử phải cùng kiểu).

Ví dụ:
```
import numpy as np
data = np.array([[1, 6, 7], [8-10]])
print(data.shape) # (2, 3)
print(data.ndim)  # 2
print(data.dtype) # int64
``` 

## 2. Tạo mảng trong NumPy
Có nhiều cách để khởi tạo một mảng:

### 2.1. Từ giá trị cho trước
*   `np.array()`: Tạo mảng từ list Python.
*   `np.arange(start, stop, step)`: Tạo dãy số tăng đều tương tự hàm range.
*   `np.linspace(start, stop, num)`: Tạo dãy số cách đều với số phần tử xác định.

### 2.2. Mảng đặc biệt
*   `np.zeros(shape)`: Mảng toàn số 0.
*   `np.ones(shape)`: Mảng toàn số 1.
*   `np.full(shape, value)`: Mảng với giá trị tùy ý.

### 2.3. Mảng ngẫu nhiên
- `np.random.random()`: Số thực trong khoảng `[0.0, 1.0)`.

- `np.random.uniform(a, b)`: Số thực trong khoảng tùy chỉnh.

- `np.random.seed()`: Cố định bộ sinh số ngẫu nhiên để kết quả có thể lặp lại.

**Ví dụ:**
```python
# Tạo dãy 5 điểm cách đều từ 0 đến 1
arr = np.linspace(0, 1, 5) # [0. 0.25 0.5 0.75 1.]
``` 

## 3. Lập chỉ mục, Cắt lát và Biến đổi hình dạng

### 3.1. Chỉ mục (Indexing) và Cắt lát (Slicing)

- Hỗ trợ cả chỉ mục xuôi (từ 0) và ngược (từ -1).

- Cú pháp cắt lát: `start:stop:step`.

**Lưu ý:** Cắt lát thông thường trả về một **khung nhìn (view)**, thay đổi trên view sẽ làm thay đổi mảng gốc.

### 3.2. Biến đổi hình dạng (Reshaping)
- `reshape(new_shape)`: Thay đổi hình dạng mà không đổi dữ liệu.
- `flatten()`: Làm phẳng mảng nhiều chiều thành mảng 1 chiều.
- `.T`: Chuyển vị ma trận (hàng thành cột và ngược lại).

## 4. Mặt nạ Boolean và Lọc dữ liệu

Đây là kỹ thuật mạnh mẽ để xử lý dữ liệu theo điều kiện mà không cần dùng vòng lặp.

- **Tạo mặt nạ:** Áp dụng các toán tử so sánh (`>`, `<`, `==`,...) lên mảng.
- **Lọc dữ liệu:** Truyền mặt nạ vào cặp ngoặc vuông `data[mask]`.
- Chọn giá trị `x` nếu điều kiện đúng, ngược lại chọn `y`: `np.where(condition, x, y)`.

**Ví dụ:**
```python
data = np.array([1, 7, 8, 10, 27, 28])
# Lấy các phần tử <= 7
filtered = data[data <= 7] # 
# Gán lại giá trị theo điều kiện: thay các số lẻ bằng -1
data[data % 2 == 1] = -1 # [-1 8 -1 4 -1 6]
```

## 5. Kết hợp và Biến đổi nhiều mảng

- `np.concatenate((a, b), axis)`: Ghép mảng theo trục dọc (`axis=0`) hoặc ngang (`axis=1`).

- `np.vstack()` / `np.hstack()`: Ghép nhanh theo chiều dọc/ngang.

- `np.repeat()`: Lặp từng phần tử.

- `np.tile()`: Lặp toàn bộ khối mảng.

## 6. Đại số tuyến tính với NumPy

### 6.1. Phép toán trên Vector

- **Độ dài Euclid (Chuẩn L2):** `np.linalg.norm(u)`.

- **Tích vô hướng (Dot product):** `u.dot(v)` hoặc dùng toán tử `@`.

- **Phép nhân Hadamard:** Nhân từng phần tử tương ứng bằng toán tử `*`.

### 6.2. Phép toán trên Ma trận

- **Nhân ma trận:** `A.dot(B)` hoặc `A @ B` (điều kiện: số cột của A phải bằng số hàng của B).

- **Cộng/Trừ/Nhân/Chia vô hướng:** Áp dụng lên từng phần tử của ma trận.

- **Broadcasting:** Cơ chế tự động mở rộng mảng nhỏ để khớp với mảng lớn hơn khi thực hiện phép toán.

**Ví dụ nhân ma trận:**
```python
A = np.array([[1, 6], [7, 8]])
B = np.array([[9, 10], [27, 28]])
result = A @ B 
# Kết quả: [[24, 25], [42, 43]]
``` 

## 7. Xác suất thống kê với NumPy

### 7.1. Các hàm tổng hợp

NumPy cung cấp các hàm để rút gọn mảng thành các giá trị đại diện:

- Tổng, trung bình, trung vị: `np.sum()`, `np.mean()`, `np.median()`.

- Phương sai và độ lệch chuẩn: `np.var()`, `np.std()`.

- Phân vị: `np.percentile()`, `np.quantile()`.

- Tính theo trục: Dùng `axis=0` để tính theo từng cột (cho ra kết quả cho mỗi đặc trưng) hoặc `axis=1` cho từng hàng.

### 7.2. Xác suất và Phân phối
- **Xác suất thực nghiệm:** Có thể ước tính bằng cách lấy trung bình (`np.mean`) của một mảng Boolean.

- **Phân phối Gaussian (Chuẩn):** Được đặc trưng bởi trung bình $\mu$ và độ lệch chuẩn $\sigma$.

- **Hình dạng phân phối của dữ liệu**: `np.histogram()`.

- **Z-score (Chuẩn hóa):** Đưa dữ liệu về trung bình bằng 0 và độ lệch chuẩn bằng 1.

$$ z = \frac{x - \mu}{\sigma}$$

**Ví dụ chuẩn hóa dữ liệu:**
```python
data = np.array([[1, 6], [7, 8], [9, 10]])
mean = data.mean(axis=0)
std = data.std(axis=0)
# Chuẩn hóa z-score bằng broadcasting
standardized_data = (data - mean) / std
```
