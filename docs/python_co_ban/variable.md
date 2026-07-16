# Tổng quan về biến trong Python

## Khai báo biến

- Cấu trúc:
    
    ```python
    variable_name = value
    ```
    
- Trong Python, kiểu biến được phần mềm tự động hiểu thông qua giá trị gán.
    - String phải khai báo trong ngoặc “ “ hoặc ‘ ‘
    - Float dùng dấu . để ngăn phần nguyên và phần thập phân
- Chú ý:
    - Ko sử dụng các keyword của Python để khai báo biến: print, return,…
    - Ko bắt đầu tên biến bằng số (1a, 2abd,..) vì máy tính dễ hiểu nhầm sang cách biểu diễn số.
    
    ⇒ Sử dụng các tên có ý nghĩa, phù hợp với mục đích code.
    

## Các phép toán cơ bản


- Tất cả các phép chia / đều nhận kết quả là float, các phép chia // và % đều nhận kết quả là int.



- Toán tử gán: giúp tối ưu code (viết gọn hơn, thực hiện nhanh hơn).
- Phép toán logic: XOR = not + and + or (A ^ B).
- Thứ tự thực hiện các phép toán: ( ) ⇒ mũ ⇒ nhân ⇒ chia ⇒ cộng ⇒ trừ.

## Mutable and Immutable

- Mutable objects: Objects that **can** be changed: list, set or dict.
- Immutable objects: Objects that **cannot** be changed: int, float, bool or string, tuple.
- Thực tế phép gán biến = trỏ đến vị trí vùng nhớ của biến đó ⇒ b = a ⇒ b trỏ đến cùng 1 vùng nhớ.
    - Cách kiểm tra vị trí bộ nhớ của 1 biến: print(id(variable))

<aside>
💡

*Lưu ý:* Python đã định nghĩa sẵn khoảng các số nguyên từ [-5, 256].

Nghĩa là: Khi một chương trình Python khởi động, tất cả các giá trị trong khoảng đó sẽ được tạo ra và lưu sẵn trong bộ nhớ. Khi chúng ta tạo một biến với giá trị trong khoảng đó, Python sẽ không cấp phát vùng mới nữa, mà chỉ đơn giản là lấy ra địa chỉ vùng nhớ đã có sẵn chứa giá trị tương ứng là được.

Ví dụ: khi chúng ta gán `x = 100` nằm trong khoảng [-5, 256], Python sẽ tìm kiếm vùng nhớ đã tạo sẵn chứa giá trị tương ứng. Khi chúng ta gán một biến nằm ngoài khoảng trên, một vùng nhớ mới được cấp phát chứa giá trị mới. 

Do đó, vị trí bộ nhớ của các biến khác nhau nhưng có cùng giá trị nằm trong khoảng [-5, 256] là **giống nhau**. Nhưng các biến khác nhau, có cùng giá trị nằm ngoài khoảng này thì vị trí bộ nhớ lại khác nhau.

</aside>

## Overflow and Underflow

(Tràn số & thiếu số)

- Inf: số lớn vô cùng ⇒ vẫn tính được.
- NaN (not a number): số ko xác định ⇒ ko tính được.
- Python chỉ lưu trữ giá trị xấp xỉ của float, ko lưu giá trị chính xác.

```python
0.1 + 0.2 == 0.3 => False
```

## Các ký hiệu đặc biệt

- _: biến tạm không dùng đến
    - Trong vòng lặp for: chỉ quan tâm đến số lần thực thi câu lệnh, ko quan tâm chỉ số.
    - Trong tuple, list: gán cho một số lượng giá trị chưa cần làm rõ.

